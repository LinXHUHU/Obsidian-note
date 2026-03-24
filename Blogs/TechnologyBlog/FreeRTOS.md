# FreeRTOS

[Mastering-the-FreeRTOS-Real-Time-Kernel.v1.1.0.pdf](Blogs/TechnologyBlog/assets/Mastering-the-FreeRTOS-Real-Time-Kernel.v1.1.0-20250403075857-8diwf3g.pdf)

# RTOS 基础知识

实时操作系统 (RTOS) 是一种**体积小巧、确定性强**的计算机操作系统。 RTOS 通常用于需要在**严格时间**限制内对外部事件做出反应的嵌入式系统，如医疗设备和汽车电子控制单元 (ECU)。

‍

# 多任务处理

rtos中没有虚拟内存，线程和进程没有区别，所以只有任务概念

多内核并行

单内核并发

![C0A6D812-088E-4789-AA50-2CA64B742A33](Blogs/TechnologyBlog/assets/C0A6D812-088E-4789-AA50-2CA64B742A33-20250403063902-qhogf2y.png)

‍

# 调度策略

很多，属于操作系统知识

## 实时调度

实时操作系统 (RTOS) 利用与通用（非实时）系统相同**的原理来实现多任务处理**， 但两者的目标截然不同：差异主要体现在调度策略

RTOS 调度策略必须确保遵守这些截止时间要求。

实现方式：分配优先级， 同等优先级公平

‍
