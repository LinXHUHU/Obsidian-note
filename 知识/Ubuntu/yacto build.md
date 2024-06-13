
 1、/usr/sbin/visudo 命令
	 对sudoer 文件提供安全的修改
	 lxh ALL = NOPASSWD: /usr/bin/apt-get 表示lxh可以无需密码就可以使用aptget指令

2、在运行source脚本的时候遇到了apt-get install python失败的问题。
	因为在新版的apt源中不包含老版本python 应该使用python3 或更新的
	在脚本路径中，