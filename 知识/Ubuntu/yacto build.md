
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

Xen Hypervisor 是一套直接运行在计算机硬件之上的软件层，它代替操作系统，从而允许计算机硬件能同时运行多个客户操作系统