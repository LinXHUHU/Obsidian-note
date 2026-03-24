
annotation-target::BSP/asset/Linux设备驱动开发详解_宋宝华.pdf



>%%
>```annotation-json
>{"created":"2025-09-17T06:09:32.806Z","updated":"2025-09-17T06:09:32.806Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":39710,"end":39781},{"type":"TextQuoteSelector","exact":"ICE 本身需要完全仿真CPU 的行为，可以从物理上完全替代CPU，而ICD 则只是与芯片内部提供的嵌入式ICE 单元通过JTAG 等接口互通","prefix":"示。   ICD 是一个容易与 ICE（在线仿真器）混淆的概念，","suffix":"。因此，对ICD 的硬件性能要求远低于ICE。   图2.31 "}]}]}
>```
>%%
>*%%PREFIX%%示。   ICD 是一个容易与 ICE（在线仿真器）混淆的概念，%%HIGHLIGHT%% ==ICE 本身需要完全仿真CPU 的行为，可以从物理上完全替代CPU，而ICD 则只是与芯片内部提供的嵌入式ICE 单元通过JTAG 等接口互通== %%POSTFIX%%。因此，对ICD 的硬件性能要求远低于ICE。   图2.31*
>%%LINK%%[[#^tja14ffl3bh|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^tja14ffl3bh


>%%
>```annotation-json
>{"created":"2025-09-17T06:18:04.505Z","text":"为什么内核任务被抢占能提高实时性？时间短了高优先级任务不会被block","updated":"2025-09-17T06:18:04.505Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":43430,"end":43450},{"type":"TextQuoteSelector","exact":"内核任务可以被抢占，从而提高系统的实时性","prefix":"地扩展。 2．内核抢占 在 2.6 版本的 Linux 内核中，","suffix":"。这样做最主要的优势在于可以极大地增强系统的用户交互性。 3．改"}]}]}
>```
>%%
>*%%PREFIX%%地扩展。 2．内核抢占 在 2.6 版本的 Linux 内核中，%%HIGHLIGHT%% ==内核任务可以被抢占，从而提高系统的实时性== %%POSTFIX%%。这样做最主要的优势在于可以极大地增强系统的用户交互性。 3．改*
>%%LINK%%[[#^k3fr2ma4b3|show annotation]]
>%%COMMENT%%
>为什么内核任务被抢占能提高实时性？时间短了高优先级任务不会被block
>%%TAGS%%
>
^k3fr2ma4b3


>%%
>```annotation-json
>{"created":"2025-09-17T06:24:34.957Z","text":"虚拟内存的大小是一个由**操作系统、处理器架构（CPU位数）和系统配置**共同决定的概念。它指的是每个进程所能使用的**虚拟地址空间的大小**，而不是物理内存（RAM）的实际容量。\n\n下面我们从几个层面来详细解析“虚拟内存的大小”。\n\n---\n\n### 一、虚拟内存 vs 物理内存\n\n| 概念 | 说明 |\n|------|------|\n| **物理内存（Physical Memory）** | 实际安装的 RAM，比如 8GB、16GB。 |\n| **虚拟内存（Virtual Memory）** | 每个进程“看到”的独立地址空间，由操作系统和MMU（内存管理单元）管理。 |\n\n> ✅ 虚拟内存可以**远大于**物理内存，因为它不仅使用RAM，还使用**硬盘上的交换空间（Swap）**来扩展。\n\n---\n\n### 二、虚拟内存大小的决定因素\n\n#### 1. **CPU架构（位数）**\n\n这是决定虚拟地址空间上限的**硬件因素**。\n\n| 架构 | 地址总线宽度 | 理论最大虚拟地址空间 |\n|------|----------------|------------------------|\n| **32位系统** | 32位 | 2³² = **4 GB** |\n| **64位系统** | 64位 | 2⁶⁴ = 16 EB（Exabytes） |\n\n> ⚠️ 注意：虽然64位理论上支持16EB，但目前的处理器和操作系统并未使用全部64位地址。\n\n- 实际上，x86-64 架构通常使用 **48位虚拟地址**（部分支持57位）。\n- 因此，**64位系统的虚拟内存大小通常是 2⁴⁸ = 256 TB**。\n\n","updated":"2025-09-17T06:24:34.957Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":43705,"end":43712},{"type":"TextQuoteSelector","exact":"虚拟内存的变化","prefix":".embedu.org  最大可以到2000000000。 4．","suffix":" 从虚拟内存的角度来看，新内核融合了 r-map（反向映射）技术"}]}]}
>```
>%%
>*%%PREFIX%%.embedu.org  最大可以到2000000000。 4．%%HIGHLIGHT%% ==虚拟内存的变化== %%POSTFIX%%从虚拟内存的角度来看，新内核融合了 r-map（反向映射）技术*
>%%LINK%%[[#^yigwafu0vze|show annotation]]
>%%COMMENT%%
>虚拟内存的大小是一个由**操作系统、处理器架构（CPU位数）和系统配置**共同决定的概念。它指的是每个进程所能使用的**虚拟地址空间的大小**，而不是物理内存（RAM）的实际容量。
>
>下面我们从几个层面来详细解析“虚拟内存的大小”。
>
>---
>
>### 一、虚拟内存 vs 物理内存
>
>| 概念 | 说明 |
>|------|------|
>| **物理内存（Physical Memory）** | 实际安装的 RAM，比如 8GB、16GB。 |
>| **虚拟内存（Virtual Memory）** | 每个进程“看到”的独立地址空间，由操作系统和MMU（内存管理单元）管理。 |
>
>> ✅ 虚拟内存可以**远大于**物理内存，因为它不仅使用RAM，还使用**硬盘上的交换空间（Swap）**来扩展。
>
>---
>
>### 二、虚拟内存大小的决定因素
>
>#### 1. **CPU架构（位数）**
>
>这是决定虚拟地址空间上限的**硬件因素**。
>
>| 架构 | 地址总线宽度 | 理论最大虚拟地址空间 |
>|------|----------------|------------------------|
>| **32位系统** | 32位 | 2³² = **4 GB** |
>| **64位系统** | 64位 | 2⁶⁴ = 16 EB（Exabytes） |
>
>> ⚠️ 注意：虽然64位理论上支持16EB，但目前的处理器和操作系统并未使用全部64位地址。
>
>- 实际上，x86-64 架构通常使用 **48位虚拟地址**（部分支持57位）。
>- 因此，**64位系统的虚拟内存大小通常是 2⁴⁸ = 256 TB**。
>
>
>%%TAGS%%
>
^yigwafu0vze


>%%
>```annotation-json
>{"created":"2025-09-17T06:40:14.737Z","text":"正向映射：你知道“虚拟地址 A 对应哪个物理页”。\n反向映射：你知道“物理页 P 被哪些虚拟地址使用。\n\n可以解决的问题：\n1. 页面回收（Page Reclaim）\n当系统内存紧张，需要将某个物理页面换出到交换分区（swap）时，必须：\n\n找到所有映射了这个页面的进程\n更新它们的页表（标记为“不在内存”）\n减少引用计数\n如果没有反向映射，内核只能遍历所有进程的所有页表，效率极低（O(n) 复杂度）。\n\n2. 写时复制（Copy-on-Write, COW）\n多个进程共享同一物理页面（如 fork() 后）。当某个进程试图写入时，必须：\n\n拷贝该页面\n更新所有映射此页的页表项为只读或断开共享\n需要知道哪些虚拟地址映射了这个页面。\n\n3. 内存迁移（Memory Migration）\n在 NUMA 系统或多处理器系统中，为了性能优化，可能需要将页面从一个内存节点迁移到另一个节点，也需要更新所有映射。","updated":"2025-09-17T06:40:14.737Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":43731,"end":43741},{"type":"TextQuoteSelector","exact":"r-map（反向映射","prefix":"00。 4．虚拟内存的变化 从虚拟内存的角度来看，新内核融合了 ","suffix":"）技术，显著改善虚拟内存在一定程度负载下的性能。 5．文件系统 "}]}]}
>```
>%%
>*%%PREFIX%%00。 4．虚拟内存的变化 从虚拟内存的角度来看，新内核融合了%%HIGHLIGHT%% ==r-map（反向映射== %%POSTFIX%%）技术，显著改善虚拟内存在一定程度负载下的性能。 5．文件系统*
>%%LINK%%[[#^d6fki0dy0lt|show annotation]]
>%%COMMENT%%
>正向映射：你知道“虚拟地址 A 对应哪个物理页”。
>反向映射：你知道“物理页 P 被哪些虚拟地址使用。
>
>可以解决的问题：
>1. 页面回收（Page Reclaim）
>当系统内存紧张，需要将某个物理页面换出到交换分区（swap）时，必须：
>
>找到所有映射了这个页面的进程
>更新它们的页表（标记为“不在内存”）
>减少引用计数
>如果没有反向映射，内核只能遍历所有进程的所有页表，效率极低（O(n) 复杂度）。
>
>2. 写时复制（Copy-on-Write, COW）
>多个进程共享同一物理页面（如 fork() 后）。当某个进程试图写入时，必须：
>
>拷贝该页面
>更新所有映射此页的页表项为只读或断开共享
>需要知道哪些虚拟地址映射了这个页面。
>
>3. 内存迁移（Memory Migration）
>在 NUMA 系统或多处理器系统中，为了性能优化，可能需要将页面从一个内存节点迁移到另一个节点，也需要更新所有映射。
>%%TAGS%%
>
^d6fki0dy0lt


>%%
>```annotation-json
>{"created":"2025-09-17T06:46:45.664Z","updated":"2025-09-17T06:46:45.664Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":45538,"end":45609},{"type":"TextQuoteSelector","exact":"Linux 内核主要由进程调度（SCHED）、内存管理（MM）、虚拟文件系统（VFS）、网络接口（NET）和进程间通信（IPC）等5 个子系统","prefix":"3.3.2    Linux 内核的组成部分 如图3.1 所示，","suffix":"组成。 1．进程调度 精度调度控制系统中的多个进程对CPU 的访"}]}]}
>```
>%%
>*%%PREFIX%%3.3.2    Linux 内核的组成部分 如图3.1 所示，%%HIGHLIGHT%% ==Linux 内核主要由进程调度（SCHED）、内存管理（MM）、虚拟文件系统（VFS）、网络接口（NET）和进程间通信（IPC）等5 个子系统== %%POSTFIX%%组成。 1．进程调度 精度调度控制系统中的多个进程对CPU 的访*
>%%LINK%%[[#^emvu1cub8il|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^emvu1cub8il


>%%
>```annotation-json
>{"created":"2025-09-17T06:50:07.383Z","updated":"2025-09-17T06:50:07.383Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":46034,"end":46046},{"type":"TextQuoteSelector","exact":"Linux 进程状态转换","prefix":"别在于可被打断的睡眠在收到信号的时候会醒来。  图3.2    ","suffix":" 在设备驱动编程中，当请求的资源不能得到满足时，驱动一般会调度其"}]}]}
>```
>%%
>*%%PREFIX%%别在于可被打断的睡眠在收到信号的时候会醒来。  图3.2%%HIGHLIGHT%% ==Linux 进程状态转换== %%POSTFIX%%在设备驱动编程中，当请求的资源不能得到满足时，驱动一般会调度其*
>%%LINK%%[[#^wfpwaceh1ar|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^wfpwaceh1ar


>%%
>```annotation-json
>{"created":"2025-09-17T07:04:08.337Z","text":"内核线程（Kernel Thread）和普通线程（通常指用户线程，User Thread）是操作系统中两种不同类型的执行流，它们在**运行环境、权限、用途、调度方式**等方面有本质区别。\n\n下面从多个维度详细解析它们的区别：\n\n---\n\n### 一、基本定义\n\n| 类型 | 定义 |\n|------|------|\n| **内核线程（Kernel Thread）** | 运行在**内核空间**的特殊线程，由内核直接创建和管理，没有独立的地址空间，只执行内核函数。 |\n| **普通线程（用户线程）** | 运行在**用户空间**的线程，属于某个用户进程，共享该进程的地址空间，执行应用程序代码。 |\n\n---\n\n### 二、核心区别对比表\n\n| 对比维度 | 内核线程（Kernel Thread） | 普通线程（用户线程） |\n|----------|----------------------------|------------------------|\n| **运行空间** | 内核空间（Kernel Space） | 用户空间（User Space） |\n| **地址空间** | 无独立地址空间，使用内核的全局地址空间 | 共享所属进程的虚拟地址空间 |\n| **创建者** | 内核自身（通过 `kernel_thread()` 或 `kthread_create()`） | 用户程序（通过 `pthread_create()` 等） |\n| **执行代码** | 内核函数（如 `kswapd`、`kthreadd`） | 用户程序代码（C/C++ 函数等） |\n| **权限级别** | 特权模式（Ring 0），可访问所有硬件和内核数据 | 用户模式（Ring 3），受权限限制 |\n| **用途** | 执行内核后台任务（如内存回收、设备轮询） | 实现程序的并发逻辑（如多任务处理） |\n| **上下文切换开销** | 较小（无需切换地址空间） | 较大（可能涉及 TLB 刷新、页表切换） |\n| **可见性** | 对用户不可见，`ps` 中以 `[ ]` 显示（如 `[kworker/0:1]`） | 对用户可见，可通过 `ps`、`htop` 查看 |\n| **调度单位** | 是，由内核调度器统一调度 | 是，现代系统中通常为 **1:1 模型**（每个用户线程对应一个内核调度实体） |\n\n---\n\n\n“每个进程的内核空间”是通往全局内核的虚拟门户，它让所有进程都能快速、统一地访问内核服务，同时保持用户空间的隔离性。\n","updated":"2025-09-17T07:04:08.337Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":46123,"end":46151},{"type":"TextQuoteSelector","exact":"设备驱动中，如果需要几个并发执行的任务，可以启动内核线程","prefix":"入睡眠状态，直到它请求的资源被释放，才会被唤醒而进入就绪状态。 ","suffix":"，启动内核线程的函数为： int kernel_thread(i"}]}]}
>```
>%%
>*%%PREFIX%%入睡眠状态，直到它请求的资源被释放，才会被唤醒而进入就绪状态。%%HIGHLIGHT%% ==设备驱动中，如果需要几个并发执行的任务，可以启动内核线程== %%POSTFIX%%，启动内核线程的函数为： int kernel_thread(i*
>%%LINK%%[[#^azdlkoqrhxw|show annotation]]
>%%COMMENT%%
>内核线程（Kernel Thread）和普通线程（通常指用户线程，User Thread）是操作系统中两种不同类型的执行流，它们在**运行环境、权限、用途、调度方式**等方面有本质区别。
>
>下面从多个维度详细解析它们的区别：
>
>---
>
>### 一、基本定义
>
>| 类型 | 定义 |
>|------|------|
>| **内核线程（Kernel Thread）** | 运行在**内核空间**的特殊线程，由内核直接创建和管理，没有独立的地址空间，只执行内核函数。 |
>| **普通线程（用户线程）** | 运行在**用户空间**的线程，属于某个用户进程，共享该进程的地址空间，执行应用程序代码。 |
>
>---
>
>### 二、核心区别对比表
>
>| 对比维度 | 内核线程（Kernel Thread） | 普通线程（用户线程） |
>|----------|----------------------------|------------------------|
>| **运行空间** | 内核空间（Kernel Space） | 用户空间（User Space） |
>| **地址空间** | 无独立地址空间，使用内核的全局地址空间 | 共享所属进程的虚拟地址空间 |
>| **创建者** | 内核自身（通过 `kernel_thread()` 或 `kthread_create()`） | 用户程序（通过 `pthread_create()` 等） |
>| **执行代码** | 内核函数（如 `kswapd`、`kthreadd`） | 用户程序代码（C/C++ 函数等） |
>| **权限级别** | 特权模式（Ring 0），可访问所有硬件和内核数据 | 用户模式（Ring 3），受权限限制 |
>| **用途** | 执行内核后台任务（如内存回收、设备轮询） | 实现程序的并发逻辑（如多任务处理） |
>| **上下文切换开销** | 较小（无需切换地址空间） | 较大（可能涉及 TLB 刷新、页表切换） |
>| **可见性** | 对用户不可见，`ps` 中以 `[ ]` 显示（如 `[kworker/0:1]`） | 对用户可见，可通过 `ps`、`htop` 查看 |
>| **调度单位** | 是，由内核调度器统一调度 | 是，现代系统中通常为 **1:1 模型**（每个用户线程对应一个内核调度实体） |
>
>---
>
>
>“每个进程的内核空间”是通往全局内核的虚拟门户，它让所有进程都能快速、统一地访问内核服务，同时保持用户空间的隔离性。
>
>%%TAGS%%
>
^azdlkoqrhxw



>%%
>```annotation-json
>{"created":"2025-09-17T07:10:31.520Z","updated":"2025-09-17T07:10:31.520Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":46621,"end":46627},{"type":"TextQuoteSelector","exact":"虚拟文件系统","prefix":"du.org   图3.3    Linux 进程地址空间 3．","suffix":" 如图3.4 所示，Linux 虚拟文件系统（VFS）隐藏各种了"}]}]}
>```
>%%
>*%%PREFIX%%du.org   图3.3    Linux 进程地址空间 3．%%HIGHLIGHT%% ==虚拟文件系统== %%POSTFIX%%如图3.4 所示，Linux 虚拟文件系统（VFS）隐藏各种了*
>%%LINK%%[[#^6m8mall5it6|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^6m8mall5it6


>%%
>```annotation-json
>{"created":"2025-09-17T07:10:41.209Z","updated":"2025-09-17T07:10:41.209Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":46637,"end":46681},{"type":"TextQuoteSelector","exact":"Linux 虚拟文件系统（VFS）隐藏各种了硬件的具体细节，为所有的设备提供了统一的接口","prefix":" Linux 进程地址空间 3．虚拟文件系统 如图3.4 所示，","suffix":"。而且，它独立于各个具体的文件系统，是对各种文件系统的一个抽象，"}]}]}
>```
>%%
>*%%PREFIX%%Linux 进程地址空间 3．虚拟文件系统 如图3.4 所示，%%HIGHLIGHT%% ==Linux 虚拟文件系统（VFS）隐藏各种了硬件的具体细节，为所有的设备提供了统一的接口== %%POSTFIX%%。而且，它独立于各个具体的文件系统，是对各种文件系统的一个抽象，*
>%%LINK%%[[#^3qbgsrm3381|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^3qbgsrm3381


>%%
>```annotation-json
>{"created":"2025-09-17T07:15:36.584Z","updated":"2025-09-17T07:15:36.584Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":47698,"end":47715},{"type":"TextQuoteSelector","exact":"ARM 处理器有以下7 种工作模式","prefix":"空间 现代CPU 内部往往实现了不同的操作模式（级别）。 例如，","suffix":"。 l 用户模式（usr）：大多数的应用程序运行在用户模式下，当"}]}]}
>```
>%%
>*%%PREFIX%%空间 现代CPU 内部往往实现了不同的操作模式（级别）。 例如，%%HIGHLIGHT%% ==ARM 处理器有以下7 种工作模式== %%POSTFIX%%。 l 用户模式（usr）：大多数的应用程序运行在用户模式下，当*
>%%LINK%%[[#^1dcg3t8v9g2|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^1dcg3t8v9g2


>%%
>```annotation-json
>{"created":"2025-09-17T07:16:03.127Z","updated":"2025-09-17T07:16:03.127Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":47990,"end":48022},{"type":"TextQuoteSelector","exact":"X86 处理器包含4 个不同的特权级，称为Ring0～Ring3","prefix":"指令执行时进入该模式，可用于支持硬件协处理器的软件仿真。 又如，","suffix":"。Ring0 下，可以执行特权级指令，对任何I/O 设备都有访问"}]}]}
>```
>%%
>*%%PREFIX%%指令执行时进入该模式，可用于支持硬件协处理器的软件仿真。 又如，%%HIGHLIGHT%% ==X86 处理器包含4 个不同的特权级，称为Ring0～Ring3== %%POSTFIX%%。Ring0 下，可以执行特权级指令，对任何I/O 设备都有访问*
>%%LINK%%[[#^hefkmjttmbe|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^hefkmjttmbe


>%%
>```annotation-json
>{"created":"2025-09-17T07:16:22.855Z","updated":"2025-09-17T07:16:22.855Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":48224,"end":48256},{"type":"TextQuoteSelector","exact":"Linux 系统充分利用CPU 的这一硬件特性，但它只使用了两级","prefix":" 嵌入式学院—华清远见旗下品牌：www.embedu.org  ","suffix":"。在 Linux 系统中，内核可进行任何操作，而应用程序则被禁止"}]}]}
>```
>%%
>*%%PREFIX%%嵌入式学院—华清远见旗下品牌：www.embedu.org%%HIGHLIGHT%% ==Linux 系统充分利用CPU 的这一硬件特性，但它只使用了两级== %%POSTFIX%%。在 Linux 系统中，内核可进行任何操作，而应用程序则被禁止*
>%%LINK%%[[#^jd466v6f9no|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^jd466v6f9no


>%%
>```annotation-json
>{"created":"2025-09-17T07:16:54.349Z","updated":"2025-09-17T07:16:54.349Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":48395,"end":48433},{"type":"TextQuoteSelector","exact":"Linux 系统只能通过系统调用和硬件中断完成从用户空间到内核空间的控制转移","prefix":"名词被用来区分程序执行的这两种不同状态，它们使用不同的地址空间。","suffix":"。   Linux 内核的编译及加载  3.4.1    Lin"}]}]}
>```
>%%
>*%%PREFIX%%名词被用来区分程序执行的这两种不同状态，它们使用不同的地址空间。%%HIGHLIGHT%% ==Linux 系统只能通过系统调用和硬件中断完成从用户空间到内核空间的控制转移== %%POSTFIX%%。   Linux 内核的编译及加载  3.4.1    Lin*
>%%LINK%%[[#^ge0fqqev1j9|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^ge0fqqev1j9


>%%
>```annotation-json
>{"created":"2025-09-17T07:26:34.299Z","updated":"2025-09-17T07:26:34.299Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":56827,"end":56892},{"type":"TextQuoteSelector","exact":"nitrd（Bootloader  initialized  RAM  disk）是指由  Bootloader 初始化的内存盘。","prefix":"同时下载程序包device-mapper 和程序包lvm2。 i","suffix":"在Linux 内核启动前，Bootloader 会将存储介质中的"}]}]}
>```
>%%
>*%%PREFIX%%同时下载程序包device-mapper 和程序包lvm2。 i%%HIGHLIGHT%% ==nitrd（Bootloader  initialized  RAM  disk）是指由  Bootloader 初始化的内存盘。== %%POSTFIX%%在Linux 内核启动前，Bootloader 会将存储介质中的*
>%%LINK%%[[#^0kgswtbu0vsj|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^0kgswtbu0vsj


>%%
>```annotation-json
>{"created":"2025-09-17T09:39:13.138Z","updated":"2025-09-17T09:39:13.138Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":62294,"end":62319},{"type":"TextQuoteSelector","exact":"了y、m 以外的obj-x 形式的目标都不会被编译","prefix":"o 并连接进内核，而 obj-m 则表示该文件要作为模块编译。除","suffix":"。 而更常见的做法是根据.config 文件的 CONFIG_变"}]}]}
>```
>%%
>*%%PREFIX%%o 并连接进内核，而 obj-m 则表示该文件要作为模块编译。除%%HIGHLIGHT%% ==了y、m 以外的obj-x 形式的目标都不会被编译== %%POSTFIX%%。 而更常见的做法是根据.config 文件的 CONFIG_变*
>%%LINK%%[[#^llav9bikqa8|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^llav9bikqa8


>%%
>```annotation-json
>{"created":"2025-09-17T09:46:56.780Z","updated":"2025-09-17T09:46:56.780Z","document":{"title":"第1章、设备驱动概述","link":[{"href":"urn:x-pdf:b16385bd3cb87f499cbf86efd0a30b0d"},{"href":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf"}],"documentFingerprint":"b16385bd3cb87f499cbf86efd0a30b0d"},"uri":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","target":[{"source":"vault:/BSP/asset/Linux%E8%AE%BE%E5%A4%87%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E8%AF%A6%E8%A7%A3_%E5%AE%8B%E5%AE%9D%E5%8D%8E.pdf","selector":[{"type":"TextPositionSelector","start":68497,"end":68582},{"type":"TextQuoteSelector","exact":"不过在X86  PC 上有一个从BIOS（基本输入/输出系统）转移到Bootloader 的过程，如图3.10 所示，而嵌入式系统往往复位后就直接运行Bootloader","prefix":" 内核的过程和引导嵌入式系统上的Linux 内核的过程基本类似。","suffix":"。 Administrator2010/10/22，15:20:"}]}]}
>```
>%%
>*%%PREFIX%%内核的过程和引导嵌入式系统上的Linux 内核的过程基本类似。%%HIGHLIGHT%% ==不过在X86  PC 上有一个从BIOS（基本输入/输出系统）转移到Bootloader 的过程，如图3.10 所示，而嵌入式系统往往复位后就直接运行Bootloader== %%POSTFIX%%。 Administrator2010/10/22，15:20:*
>%%LINK%%[[#^54acr1uwl4m|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^54acr1uwl4m
