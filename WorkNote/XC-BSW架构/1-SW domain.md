![[WorkNote/XC-BSW架构/asset/Pasted image 20250715180442.png]]


[SWAD Mid Trim — BOSCH (China) ADCC BSW documentation](http://rb-xccp-documentation.apac.bosch.com/middletrim_xccn/jetour_d01/latest_release/architecture/swad/swad_index.html)


---

## 🧱 一、总体结构概览（Three Domains）

| 域名                | 中文名称        | CPU 核心                    | 主要功能                    |
| ----------------- | ----------- | ------------------------- | ----------------------- |
| **MCU Domain**    | 微控制器域 / 实时域 | R Core                    | 安全关键型任务（启动、电源管理、CAN通信等） |
| **Secure Domain** | 安全域         | A Core (Secure World)     | 提供安全服务（加密、签名、密钥管理等）     |
| **Main Domain**   | 主域          | A Core (Non-Secure World) | 运行 QNX 系统及自动驾驶应用        |

---

## 🔍 二、详细解析每个域的功能

### ✅ 6.2.1 MCU Domain（微控制器域）

- 又称：**Vehicle Domain**
- 使用：**R Core**
- 遵循标准：**AUTOSAR Classic Platform**
- 功能职责：
  - ✅ **系统安全启动（Secure Boot）**
    - 控制整个系统的启动流程，确保只运行可信代码。
  - ✅ **电源状态管理**
    - 管理整车的上电、下电、休眠、唤醒等操作。
  - ✅ **车辆数据收发（CAN/CANFD）**
    - 与车身其他 ECU 通信，获取车速、档位、方向盘角度等信息。
  - ✅ **监控主域开关机和复位**
    - 监控 A Core 是否正常启动或崩溃，并做出响应。
  - ✅ **系统生命周期管理**
    - 支持 OTA 升级、激活、去激活等状态转换。
  - ✅ **功能安全监控与防护**
    - 符合 ISO 26262 功能安全要求，检测并处理故障。
  - ✅ **热管理**
    - 监测芯片温度，防止过热导致系统异常。
  - ✅ **系统时间同步**
    - 维护统一的时间基准，用于日志记录和事件分析。

> 🔹 文档重点标注为蓝色的部分，就是指这些在 MCU Domain 中实现的关键子系统和组件。

---

### ✅ 6.2.2 Secure Domain（安全域）

- 使用：**A Core（Secure World）**
- 架构基础：**ARM TrustZone** [[WorkNote/XC-BSW架构/TrustZone|TrustZone]]
  - 区分两个世界：Secure World（安全世界） 和 Non-Secure World（非安全世界）
- 功能职责：
  - ✅ **数字签名与验证**
    - 保证固件/软件来源合法、未被篡改。
  - ✅ **加密与解密**
    - 支持 AES、RSA、ECC 等算法。
  - ✅ **安全存储**
    - 存储敏感数据如私钥、证书等，不暴露给外部。
  - ✅ **证书验证**
    - 用于身份认证，确保通信双方可信。

#### ⚙️ 运行环境说明
- 根据 Bosch 内部规则，必须使用 **Global Platform 团队定义的 API** 来开发该域的应用。
- 运行环境简单，**没有调度器**，只能运行“受信任应用”（Trusted Applications），由其它域来调度执行。
- 在 **Jetour D01 项目** 中，这个==环境是由 Horizon 提==供的，叫做 **OP-TEE（Open Portable Trusted Execution Environment）**

#### 🔒 更新机制
- Secure Domain 的更新必须集成进整个系统的 **软件更新流程**（Software Update Process）中，==不能单独更新。==


---

### ✅ 6.2.3 Main Domain（主域）

- 使用：**A Core（Non-Secure World）**
- 是 Secure World 的“对端”，用于运行复杂应用。
- 启动流程：
  - 从 **U-Boot** 开始启动
  - 加载 **QNX 实时操作系统**
  - 部署 BSP（Board Support Package）和设备驱动

#### 📦 子域划分

##### 1. Adaptive AUTOSAR Sub-Domain
- 提供运行环境支持：
  - ✅ 软件更新（Software Update）
  - ✅ 诊断服务（Diagnostics）
  - ✅ 进程健康监控（Processes Health Management）
- 适用于需要高灵活性、可扩展性的 Base-Tech 软件模块。

##### 2. AOS Sub-Domain
- AOS = ==Autonomous Operating System==
- 提供运行环境用于部署：
  - ✅ Midtrim 级别的驾驶员辅助系统应用（Driver Assistance System）
  - 如感知、融合、路径规划等模块


> J6x 平台将智能驾驶系统的软件划分为三个关键域：  
> - **MCU Domain（R Core）** 负责实时控制与安全相关任务；  
> - **Secure Domain（A Core Secure World）** 提供硬件级别的安全保障；  
> - **Main Domain（A Core Non-Secure World）** 负责运行高级操作系统 QNX 和自动驾驶应用。  

这三个域相互配合，构建了一个既安全又强大的智能驾驶系统架构。

---

[[WorkNote/XC-BSW架构/跨域关键功能|跨域关键功能]]

[[WorkNote/XC-BSW架构/什么是HSM|什么是HSM]]


## 🧱 一、MCU Domain 子模块划分   autosar cp

MCU Domain 是基于 R Core 实现的，运行的是 AUTOSAR Classic Platform，主要用于实现车辆控制、电源管理、安全启动等关键任务。它由以下子模块组成：

| 子模块                    | 英文全称                                | 中文含义          | 功能说明                                 |
| ---------------------- | ----------------------------------- | ------------- | ------------------------------------ |
| **HSM**                | Hardware Security Module            | 硬件安全模块        | 提供硬件级加密服务，支持 Secure Boot、密钥管理、签名验证等  |
| **Secure Boot**        | Secure Boot                         | 安全启动          | 确保只有经过签名认证的代码才能在 R Core 和 A Core 上运行 |
| **CUBAS OS & Service** | Cubas Operating System and Services | CUBAS 操作系统及服务 | 实现 AUTOSAR 操作系统层（OS），提供任务调度、中断管理等功能  |
| **DADDY RTE**          | Runtime Environment                 | 运行时环境         | 实现 AUTOSAR 的 RTE 层，连接应用 SWC 和基础软件模块  |
| **CDDs**               | Complex Device Drivers              | 复杂设备驱动        | 提供特定外设的复杂驱动支持，满足客户定制需求               |
| **MCAL**               | Microcontroller Abstraction Layer   | 微控制器抽象层       | 提供芯片底层寄存器访问接口，如 CAN、ADC、GPIO 等       |
| **Base Service Layer** | Base Services                       | 基础服务层         | 包括通信栈（CAN/CANFD）、网络管理、看门狗、错误处理等      |
| **RTE**                | Runtime Environment                 | 运行时环境         | AUTOSAR 架构中负责组件间通信与调度的核心中间件          |
| **SWC**                | Software Component                  | 软件组件          | 应用逻辑单元，例如电源状态机、CAN报文收发组件等            |

[[AP和CP中RTE的区别分析]]


> ✅ **总结一句话：**
> MCU Domain 是整个系统的“安全大脑”，通过多个子模块协同工作，确保系统安全启动、稳定运行、车辆通信正常以及功能安全达标。

---

## 🔒 二、Secure Domain 子模块划分

Secure Domain 是基于 A Core 的 **Secure World** 实现的，用于提供硬件级别的安全保障机制。

| 子模块                             | 英文全称                | 中文含义   | 功能说明                                                                           |
| ------------------------------- | ------------------- | ------ | ------------------------------------------------------------------------------ |
| **Security Monitor**            | Security Monitor    | 安全监控模块 | 利用 ==ARM TrustZone== 技术实现对安全世界的管理和切换[[WorkNote/XC-BSW架构/TrustZone\|TrustZone]] |
| **Trust App (Bosch Extension)** | Trusted Application | 可信应用   | 在 OP-TEE 环境中运行的可信应用，用于满足客户的定制化安全需求                                             |

> ✅ **总结一句话：**
> Secure Domain 是系统的“安全守护者”，利用 TrustZone 技术构建安全执行环境，保护敏感数据、执行安全操作，并为其他域提供安全服务。

---

## 🚗 三、Main Domain 子模块划分

Main Domain 是基于 A Core 的 **Non-Secure World** 实现的，运行 QNX 实时操作系统，是自动驾驶算法、感知融合、路径规划等高级功能的主要承载区域。

| 子模块 | 英文全称 | 中文含义 | 功能说明 |
|--------|-----------|----------|----------|
| **U-Boot** | Universal Boot Loader | 通用引导程序 | 系统最开始运行的程序，用于加载 QNX 操作系统 |
| **BSP & Driver** | Board Support Package & Drivers | 板级支持包和驱动 | 初始化硬件设备，提供底层驱动支持 |
| **Hobot Library & Service** | Hobot Libraries and Services | 地平线库与服务 | Horizon 提供的基础库和服务，用于图像处理、AI加速等 |
| **Vendor & System Library** | Vendor/System Libraries | 供应商/系统库 | 第三方库或系统级库（如 libc、OpenCV、TensorFlow Lite 等） |
| **Adaptive AUTOSAR** | Adaptive AUTOSAR | 自适应 AUTOSAR | 提供面向服务的架构（SOA），支持软件更新、诊断、健康管理等 |
| **AOS** | Autonomous Operating System? | 自动驾驶操作系统？ | Horizon 提供的操作系统环境，部署 Midtrim 驾驶辅助系统 |
| **ASW** | Application Software | 应用软件 | 实际部署在 AOS 中的 Midtrim 驾驶辅助应用程序，如感知、融合、决策等 |

> ✅ **总结一句话：**
> Main Domain 是系统的“计算大脑”，承载着自动驾驶核心算法和应用，提供高性能计算能力，支持各种智能驾驶功能。

---


## ✅ 总结一句话：

> 整个 J6x 平台的软件架构是一个高度分层、多域协同的系统：
> - **MCU Domain** 负责实时控制与安全；
> - **Secure Domain** 提供安全执行环境；
> - **Main Domain** 支撑高级别自动驾驶应用；
> - 各个域之间通过跨域功能（如日志、事件、升级、诊断）紧密协作，共同实现一个高安全、高性能、可扩展的智能驾驶系统。




# 日志存储服务
[[WorkNote/XC-BSW架构/Bosch Logging|Bosch Logging]]

# 时间同步功能
[[WorkNote/XC-BSW架构/时间同步|时间同步]]

