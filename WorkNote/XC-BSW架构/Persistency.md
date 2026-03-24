![[WorkNote/XC-BSW架构/asset/Pasted image 20250717100043.png]]


## 📌 一、整体架构概览

该系统中，**持久化存储模块的核心是 `Exe_VariantServer` 和 `Exe_EinServer`**，它们负责接收来自不同来源的数据，并通过底层接口（如 ARA_PER）将数据写入非易失性存储分区（Nor Flash、UFS 等）。


## 🧱 二、持久化存储模块的作用详解

### ✅ 1. **统一存储接口**
- 提供统一的接口供多个模块访问持久化数据。
- 隐藏底层硬件细节（如 Nor Flash、UFS、eMMC），实现逻辑分区抽象。

### ✅ 2. **数据写入与同步**
- 接收来自 Calibration、OTA、Camera Server 等模块的数据。
- 将数据写入指定的存储分区（partition），并保证一致性。

### ✅ 3. **数据缓存与管理**
- 支持内存缓存机制，提升读写性能。
- 支持脏数据标记、延迟写入、断电恢复等机制。

### ✅ 4. **分区管理**
- 数据按逻辑分区组织：
  - 校准参数区（外部参数、内部参数）
  - OTA 版本信息
  - 诊断日志区
  - 配置字（Configuration Words）

---

## 🔗 三、主要参与模块及其职责

| 模块                                 | 职责                               |
| ---------------------------------- | -------------------------------- |
| **Exe_VariantServer**              | 持久化数据的主服务模块，提供读写接口，管理逻辑分区        |
| **Exe_EinServer / Exe_EincServer** | R-Core 到 A-Core 的配置数据通道，用于写入配置字等 |
| **ARA_PER**                        | AUTOSAR 标准持久化接口模块，调用底层驱动完成实际写入   |
| **ARACOM_Gateway**                 | 通信网关，负责在不同模块之间转发消息               |
| **Calibration 模块**                 | 生产线上写入车辆标定数据（如相机外参）              |
| **Camera Server**                  | 写入相机内参                           |
| **Exe_OTAClient**                  | 读取版本号等元信息用于升级验证                  |
| **Exe_MDiag**                      | 读写诊断相关数据（如 DTC、诊断日志）             |

---

## ⚙️ 四、典型工作流程解析

### ✅ 场景 1：校准数据写入流程（Production Line Calibration）

```plaintext
[Step 1] Calibration 模块生成校准数据（如相机外参）
[Step 2] 通过 ARACOM_Gateway 发送至 Exe_VariantServer
[Step 3] Exe_VariantServer 调用 ARA_PER 接口
[Step 4] ARA_PER 将数据写入 Nor Flash 或 UFS 的指定 partition
[Step 5] 存储成功后返回状态码给 Calibration 模块
```

---

### ✅ 场景 2：R-Core 向 A-Core 发送配置字

```plaintext
[Step 1] R-Core 生成配置字（Configuration Words）
[Step 2] 通过 Variant 模块封装
[Step 3] 经 INC Wrapper 包装成 IPC 消息
[Step 4] 发送到 Exe_EincServer（A-Core 端）
[Step 5] Exe_EincServer 转发到 Exe_EinServer
[Step 6] EinServer 可选择将数据缓存或直接写入存储
```

---

### ✅ 场景 3：其他模块读写数据

```plaintext
[Step 1] Exe_OTAClient 请求读取版本号
[Step 2] 调用 Exe_VariantServer 接口
[Step 3] VariantServer 从指定 partition 中加载数据
[Step 4] 返回版本号信息

[Step 1] Exe_MDiag 需要记录诊断事件
[Step 2] 调用 VariantServer 接口写入日志
[Step 3] VariantServer 调用 ARA_PER 完成写入
```

---

## 📦 五、持久化数据分区设计建议

| 分区名称 | 数据类型 | 来源模块 | 更新频率 | 是否可变 |
|----------|-----------|------------|------------|-------------|
| Calibration_Ext_Params | 相机外参 | Calibration 模块 | 仅一次（产线） | ❌ 不可变 |
| Calibration_Int_Params | 相机内参 | Camera Server | 产线或售后更新 | ✅ 可变 |
| OTA_Meta_Info | 版本号、签名等 | Exe_OTAClient | 升级时更新 | ✅ 可变 |
| Diag_Logs | 诊断日志、DTC | Exe_MDiag | 实时写入 | ✅ 可变 |
| Config_Words | 系统配置参数 | R-Core | 开机动态设置 | ✅ 可变 |

---

## 🔐 六、安全与可靠性设计要点

| 设计点 | 说明 |
|--------|------|
| **数据完整性校验** | 每个分区写入前进行 CRC 或 SHA-256 校验 |
| **写保护机制** | 对只读分区（如 Calibration_Ext_Params）设置写保护 |
| **掉电恢复机制** | 支持断电后恢复未完成的写入操作 |
| **权限控制** | 不同模块只能访问授权的分区 |
| **双备份机制** | 关键数据支持双份存储，防止单点损坏 |

---

## ✅ 七、总结

你所描述的持久化存储模块是一个典型的 **车载系统中的统一配置与校准数据管理中心**，其作用包括但不限于：

- **统一接口管理**：为多个模块提供统一的读写接口
- **数据集中存储**：将校准参数、配置字、诊断日志、OTA信息等统一管理
- **跨核通信支持**：通过 INC Wrapper、ARACOM_Gateway 实现 R-Core 与 A-Core 的数据互通
- **安全性保障**：支持校验、权限、写保护、掉电恢复等机制
- **生命周期适配**：支持产线一次性写入、运行时动态更新等多种模式


