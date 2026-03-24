# 安装运行
跑不起来，白搭

# 架构整理
有点混乱，一会linux 一会windows的，混乱


someip的实现是自己写的一套协议栈，组包发包
可以跟linux中vsomeip相互通信
有sd组件
有someip method 组件， 服务订阅都可以
总结：someip协议栈完善，基于doip
基于can通信也可以

有一套使用socket模拟can总线的软件，没有硬件也可以跑得起来



# FATAL
缺少DcmMemmap gen脚本
导致 usd相关的东西跑不起来。。。 
去掉之后加一个空的头文件能 编译成功，运行失败，需要继续调试看看


# 配置工具
配置工具基于 pyqt5 实现的UI，非常简陋，没有错误处理机制
而且只是配置json文件，不涉及arxml文件
根据json文件使用 python脚本实现代码的生成


arm模拟是哟个的 quem，没跑起来， 怪怪的
