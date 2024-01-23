



> [!TODO] Title
> 1、需要将spdlog 版本固定下来 1.5.0 版本
> 2、加入到第三方库的构件中去





> [!NOTE] 在安装之后，还不能自动查找到库
> 这是因为在安装之后，还么有更新连接缓存，需要使用命令更新一下
> sudo ldconfig




2024-01-17 18:26
	1.安装 dlt-viewer
		```sudo apt install dlt-view```
	2. 开启daemon 并进行测试
	3.使用dlt-viewer 连接相关ECU的IP,就会读取其中缓存的log,诊断信息 
![[Pasted image 20240117183120.png]]



- [x] 查看daemon的使用接口
- [ ] 将log连接并发送相关信息进行测试
- [ ] 重新检查LOG模块看是否需要完善相关的接口



2024-01-18 11:12
	在Log 模块的初始化函数中启动守护进程
	```const char* command = "path/to/your/executable argument1 argument2";
	int result = std::system(command);```
		 