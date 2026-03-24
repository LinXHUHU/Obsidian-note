![[WorkNote/XC-BSW架构/asset/Pasted image 20250717101905.png]]



## 📌 一、整体架构概览

整个 Lifecycle Management 系统由多个子模块组成，分布在 **MCU Domain** 和 **Main Domain（Application Domain）** 中，实现从芯片级（SoC）到系统级（应用、功能组）的完整生命周期控制。

```
[MCU Domain]
   ├─ Service.PowerManager       → 控制外设电源上下电顺序
   ├─ Service.PowerStateController → 控制 SoC 的启动/关机、健康状态管理
   └─ Service.EcuModeManager     → 管理 ECU 模式（如 RUN、SHUTDOWN）、看门狗管理

[Main Domain]
   ├─ rb-exmd (Execution Management)    → 控制应用启动/关闭、依赖管理
   ├─ rb-stm (State Management)         → 管理 ECU 及组件状态（如 Function Group）
   └─ rb-phmd (Platform Health Management) → 应用健康监控、异常响应

[跨域通信]
   └─ INC Communication（Inter-Nuclei Communication）：用于 R-Core 与 A-Core 之间的通信协调
```

---

## 🧱 二、MCU Domain 模块详解

### ✅ 1. **Service.PowerManager（电源管理服务）**
- **职责**：
  - 控制 SoC 外设的上电与下电顺序。
  - 确保电源管理符合硬件时序要求（如先上电 VDD，再使能时钟）。
- **典型功能**：
  - 外设电源使能/关闭
  - 时钟管理
  - 低功耗模式切换（如 Standby、Sleep）

---

### ✅ 2. **Service.PowerStateController（电源状态控制器）**
- **职责**：
  - 控制 SoC 的启动与关机流程。
  - 管理 SoC 的运行状态（如 Alive、Reset、Power Down）。
  - 与 LCM（Life Cycle Manager）进行 INC 通信。
- **核心功能**：
  - SoC 上电复位控制
  - 系统关机流程管理
  - 状态同步（SoC 状态 → LCM）
  - 接收 LCM 的控制命令（如请求进入特定状态）

---

### ✅ 3. **Service.EcuModeManager（ECU 模式管理器）**
- **职责**：
  - 实现 AUTOSAR ECUM（ECU State Manager）相关的回调函数（callouts）。
  - 管理 ECU 的运行模式（如 BOOT、RUN、POST_RUN、SHUTDOWN）。
  - 看门狗（WDG）监督 ECUM 状态。
- **接口功能**：
  - `EcuM_ModeSwitch()`：模式切换接口
  - `EcuM_WdgMCheck()`：看门狗状态检查
  - `EcuM_Shutdown()`：执行关机逻辑

---

## 🧱 三、Main Domain 模块详解

### ✅ 1. **rb-exmd（Execution Management）**
- **职责**：
  - 负责系统执行管理的各个方面，包括：
    - 平台初始化（Platform Initialization）
    - 应用程序的启动与关闭
    - 启动顺序控制（依赖关系管理）
- **典型功能**：
  - 启动顺序控制（如先启动 OS，再启动 BSW，最后启动 SWC）
  - 应用依赖管理（如某个应用必须在某个服务启动后才能运行）
  - 关机流程管理（确保所有应用安全退出）

---

### ✅ 2. **rb-stm（State Management）**
- **职责**：
  - 管理 ECU 及其组件的运行状态（如 Function Group 状态、Machine State）。
  - 根据环境与内部条件（如诊断请求、电源状态）切换状态。
  - 与 Execution Management 协作控制状态切换。
- **状态类型**：
  - Function Group State（FGS）：控制功能组的启用/禁用
  - Machine State（MS）：控制整个系统的运行状态（如 Active、Standby）
- **典型交互**：
  - 接收外部事件（如诊断请求、电源变化）
  - 请求 Execution Management 执行状态切换
  - 更新内部状态机

---

### ✅ 3. **rb-phmd（Platform Health Management）**
- **职责**：
  - 监控应用程序的执行状态。
  - 提供基于规则的评估与响应机制。
  - 在异常发生时触发相应动作（如重启、进入安全状态）。
- **核心能力**：
  - 应用健康状态监控（Alive Check、Watchdog）
  - 异常检测与响应（如应用崩溃 → 重启）
  - 规则引擎（Rule-based）：根据预设策略执行动作
  - 与 STM 协作进行状态管理


## ⚙️ 五、典型生命周期流程（从上电到运行）

```plaintext
[Step 1] SoC 上电 → Service.PowerStateController 初始化
[Step 2] Service.PowerManager 控制外设电源顺序
[Step 3] rb-exmd 启动平台初始化流程
[Step 4] 启动 BSW 服务（如 OS、Com、Diag）
[Step 5] 启动 SWC 应用（根据依赖关系）
[Step 6] rb-stm 进入 RUN 状态
[Step 7] rb-phmd 开始监控应用健康状态
[Step 8] 若发生异常 → rb-phmd 触发恢复动作
[Step 9] 用户请求关机 → rb-stm 发起关机流程
[Step 10] rb-exmd 关闭所有应用 → Service.PowerManager 关闭电源
```

---

## 🔐 六、功能安全（FUSA）设计要点

| 安全目标       | 实现方式                      |
| ---------- | ------------------------- |
| **状态一致性**  | STM 与 PSC 协同管理 SoC 与平台状态  |
| **异常恢复机制** | PHMD 实现应用异常自动恢复           |
| **看门狗监督**  | EcuModeManager 监督 ECUM 状态 |
| **掉电保护**   | ==所有写入操作在关机前完成==          |
| **权限控制**   | 模式切换需授权，防止非法操作            |

---

## ✅ 七、总结

你描述的这套 **Lifecycle Management 架构** 是一个**高度模块化、分层明确、功能完备的系统生命周期管理方案**，具备以下核心优势：

| 特性 | 说明 |
|------|------|
| **模块化设计** | 各模块职责清晰，便于维护与扩展 |
| **跨核支持** | 支持 A-Core 与 R-Core 的协同工作 |
| **功能完整** | 包含从上电、运行到关机的全流程控制 |
| **安全可靠** | 支持看门狗、异常恢复、状态一致性等机制 |
| **可配置性强** | 支持多种运行模式、状态切换策略 |

