
# Problems

 1、/usr/sbin/visudo 命令
	 对sudoer 文件提供安全的修改
	 lxh ALL = NOPASSWD: /usr/bin/apt-get 表示lxh可以无需密码就可以使用aptget指令

2、在运行source脚本的时候遇到了apt-get install python失败的问题。
	因为在新版的apt源中不包含老版本python 应该使用python3 或更新的
	在脚本路径中，/home/lxh/workspace/yocto/sources/meta-alb/scripts/host-prepare-ubuntu-mint-debian.sh  中去掉python的安装  【实际上是因为脚本是针对使用18.04 设计的，所以说在18.04中运行是正常的 】
	![[Pasted image 20240613112746.png]]


# Build Yacto

# Build Ubuntu




# 名词解释

OP-TEE-Enabled： 可信运行环境，在嵌入式中保护数据的软件

---

Xen Hypervisor 是一套直接运行在计算机硬件之上的软件层，它代替操作系统，从而允许计算机硬件能同时运行多个客户操作系统[Xen虚拟化基本原理详解 - stardsd - 博客园 (cnblogs.com)](https://www.cnblogs.com/sddai/p/5931201.html)

---

ARM Trusted Firmware（简称ATF）是一种开源的软件组件，它在ARM架构的系统中扮演着至关重要的角色，提供安全启动和运行环境。
- ATF主要由几个关键组件组成，包括Secure Monitor（SM）、BL1（Boot Loader Stage 1）、BL2（Boot Loader Stage 2）和BL3x（其中x表示不同的引导阶段，如BL31、BL32、BL33等）。
- 这些组件在启动过程中扮演着不同的角色，共同确保系统的安全启动。
- - 在系统启动时，首先执行的是BL1，它负责基本的硬件初始化和安全环境的建立。
- 接着，BL1会跳转到BL2，BL2进一步执行硬件初始化，并加载和验证BL3x组件。
- BL31是Secure Monitor，它在系统完全启动后管理安全和非安全世界之间的交互。
- BL32和BL33分别是Trusted OS（如OP-TEE）和常规操作系统的引导加载程序（如U-Boot）
- ATF支持TrustZone技术，将系统的硬件和软件资源划分为安全世界和非安全世界，确保敏感数据和关键操作的安全性。
- 它还提供了安全启动的规范（TBBR），确保从硬件启动到操作系统加载的每一个环节都是经过验证和安全的。


---
设备树编译器（DTC，全称Device Tree Compiler）在Linux系统中扮演着至关重要的角色。以下是关于DTC的作用的详细解释：

1. **设备树源码编译**：
    - DTC的主要作用是将设备树的源码文件（.dts文件）编译为Linux内核可以识别的二进制文件（.dtb文件）。这些.dts文件通常包含了硬件设备的描述信息，如设备的类型、地址、中断等。
2. **语法检查和验证**：
    - 在编译过程中，DTC会对.dts文件进行语法检查和验证，以确保它们符合Linux内核的要求。这包括检查各个节点以及属性的正确性，确保设备树信息的准确性和一致性。
3. **支持内核启动**：
    - 编译生成的.dtb文件是Linux内核在启动时所需的重要文件之一。内核会读取.dtb文件中的设备树信息，从而了解系统的硬件配置，并据此初始化硬件设备和驱动程序。
4. **简化硬件描述**：
    - 通过使用设备树，Linux内核可以更加简洁、灵活地描述硬件配置信息。与传统的硬编码方式相比，设备树提供了一种更加灵活、可扩展的硬件描述方法。
5. **支持多平台和架构**：
    - DTC可以处理多种处理器架构和平台的设备树文件，如ARM、MIPS、X86等。这使得Linux内核可以在不同的硬件平台上运行，并轻松地适应各种硬件配置。
6. **源代码位置**：
    - DTC的源代码通常位于Linux内核源代码树的`/scripts/dtc/`目录下。在编译Linux内核时，DTC也会被一起编译，并生成一个可执行程序供后续使用。
7. **使用方式**：
    - 在Linux内核源代码的顶层目录下，可以使用`make ARCH=xxx CROSS_COMPILE=xxx- dtbs`命令来编译生成.dtb文件。其中，`ARCH`指定目标架构，`CROSS_COMPILE`指定交叉编译工具链的前缀。

归纳起来，设备树编译器DTC的主要作用是将设备树的源码文件编译为Linux内核可以识别的二进制文件，支持内核启动，简化硬件描述，支持多平台和架构，并在Linux内核的编译和启动过程中发挥着重要的作用。


---

