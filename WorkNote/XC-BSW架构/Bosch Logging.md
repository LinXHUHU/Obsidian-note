![[WorkNote/XC-BSW架构/asset/Pasted image 20250715165840.png]]


会存储整个系统的所有日志，包括MCU的日志，ASW日志， 系统日志（qnx 和 linux）
系统日志： VRTE中实现linux 和 qnx 系统日志子模块，会将klogd, syslog, slogger2 日志转化为 dlt



[[klogd-syslogd-rsyslogd]]

[[什么是UFS]]

[[影子模式（Shadow Mode）]]

[[DLT日志]]






![[WorkNote/XC-BSW架构/asset/Pasted image 20250715175258.png]]
![[WorkNote/XC-BSW架构/asset/Pasted image 20250715175525.png]]
FSI转发给logserver ，logserver 转发给rbdlt

# 需求
1. MCU的日志需要存储在Acore
	1. 通过以太网dlt日志传给dltd 进程存储
	2. 
2. FSI日志需要存储在Acore， [[WorkNote/XC-BSW架构/FSI功能安全岛|FSI功能安全岛]]
3. 需要存储qnx 或者linux 系统日志，slogger， syslogd，
	1. 需要一个进程将日志格式改为dlt可存储的格式

## 📦 核心模块介绍

### 1. **Exe_LogService**
- 它是整个日志功能的**核心模块**。
- 相当于一个“日志总管”，负责协调和控制日志的生成与输出。

---

### 2. **DLT Daemon（DLT Demon）**
- 全称是：**Diagnostic Log and Trace Daemon**
- 它是一个后台服务程序，作用是：
  - 收集来自不同模块的日志（AutoSAR、AOS、VRTE 等）
  - 把这些日志统一格式化
  - 存储到磁盘中（持久化保存）

你可以把它看作是“日志仓库管理员”。

---

### 3. **DLT Viewer**
- 是一个图形化工具（GUI），用来查看 DLT 日志。
- 可以连接到 DLT Daemon 或直接读取日志文件，展示日志内容。
- 帮助开发者分析问题、调试系统。

---

## 📡 不同平台/核心的日志如何发送？

系统中有几个不同的核心或平台，它们各自有不同的方式把日志发给 DLT Daemon：

---

### ✅ R Core（Real-time Core）
- 使用 **非冗余模式（non-verbose）** 输出日志（即只输出关键信息，减少干扰）
- 日志通过 **以太网（ETH）** 发送到 `rb_dltd`（也就是 DLT Daemon 的接收端）

📌 小贴士：R Core 通常是实时性要求高的部分，比如底盘控制、刹车系统等。

---

### ✅ A Core（Application Core）
- 负责运行应用程序
- 使用一个叫 **librb-alt.so** 的库来发送日志
- 同样发送到 `rb_dltd`

📌 librb-alt.so 是一个共享库，相当于“日志快递员”，帮助 App 快速发送日志。

---

### ✅ Horizon（UI 系统） 和 Linux/QNX 系统
- 这些系统本身产生的日志不是 DLT 格式
- 所以需要使用工具：
  - `dlt-linux-system`（用于 Linux）
  - `dlt-qnx-system`（用于 QNX）
- 这些工具会把系统日志**转换成 DLT 格式**，再发送给 `rb_dltd`

📌 类似于“翻译官”，把其他语言翻译成统一语言（DLT）后再上交。

## ✅ 总结一句话：

> 这个日志系统通过 Exe_LogService 控制，使用 DLT Daemon 统一收集来自 R Core、A Core、Horizon、Linux/QNX 等多个平台的日志，并通过 DLT Viewer 查看，确保日志的集中管理与高效分析。




## 🧍‍♂️ 什么是 Shadow LogServer（影子日志服务器）？

在软件系统中，我们通常会有一个**主日志服务器（Main LogServer）**，用来接收和保存系统的各种日志信息。

而 **Shadow LogServer（影子日志服务器）** 就像是这个主日志服务器的“影子”或者“备份小弟”。

---

## 🎯 它的主要作用是什么？

1. **备份数据**
   - 主日志服务器如果出问题了（比如宕机、网络断了），它能临时顶上去，不让日志丢失。

2. **减轻压力**
   - 当日志太多时，它可以帮忙分担一部分工作，让系统运行更顺畅。

3. **验证日志是否正确**
   - 它收到的日志和主服务器一样，可以用来检查主服务器有没有漏掉或弄错日志。

4. **用于测试**
   - 开发人员可以在它上面做实验，不会影响到正在使用的主服务器。

