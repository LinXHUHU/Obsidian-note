
# 1 配置文件解析


- [ ] 为vsomeip 添加e2e 流程
- [ ] 为 method 和 event 添加 e2e初始化信息，并且为所有的someip协议添加初始化信息
```
src/ara/com/internal/adapter/skeleton/skeleton_adapter.cpp

- InitializeEventInfo
- InitializeMethodInfo
- InitializeFieldInfo

src/ara/com/internal/proxy/proxy.cpp

- GetEventProtocalInfo
- GetMethodProtocalInfo
- GetFieldProtocalInfo
```


11338

# 2 工作流程


> [!NOTE] 2024.1.8
> 	今天为dds的 event 添加了配置文件解析的内容
> 	需要运行测试，解析完成之后，调用handler执行protect即可 以及check 即可



> [!warning] Title
> 中间遇到一个问题，vsomeip中的 command 在中间起到什么作用，在message序列化之后，为什么还需要command 的头？




> [!NOTE] 学习
> 在编译的时候出现了多次包含的错误，
> 原因是在包含function.h 文件的时候，头文件中包含定义，每个源文件会出现一个函数定义
> 定义为inline 之后，就会在每个编译单元中出现一个副本，从而避免多次定义


> [!BUG] 拷贝构造/ 移动构造的错误bug
> 在samptr中，父类有一个属性，子类的移动构造没有主动调用父类的移动构造函数，导致数据不能对应的上



> [!DONE] E2E
> 	今天完成了关于 dds event 状态机的 编码 以及测试


> [!TODO] Title
> 	1、首先需要完成dds method
> 	2、someip event
> 	3、someip method
> 	4、合并分支
> 	5、filed 相关的



> [!TODO] Title
> FIELD暂时还没有完成徐奥合并之后再添加接口


![[e2e 开发过程日志 2024-01-10 14.16.31.excalidraw]]


> [!DONE] Title
> 实现e2e错误处理函数的注册，注册到了 skeleton中，通过 calle2ehandler 进行调用。
> 通过  EncapsulateAndRegisterMethod 注册进入另外一个回调函数中



> [!TODO] Title
> 昨天已经找到了应该在创建 Msg的时候就进行E2eCheck的的过程。
> std::make_shared.MethodMsg.
> 今天需要完成一下
> 之后还要找到是否需要在发送Reply数据的时候加上E2E的头
> TriggerCallbackAndSend  中，在SerializeAndSendReply 之前就获取到了 res的东西，最后就在
> ReplyData(ara::com::internal 中进行了序列化，需要在这里加上回复头
> 不知道在 proxy 方 是否需要申请 E2E SM


Go GUI开发框架


> [!TODO] Title
> 	在config 初始化的时候需要新增 souceid的添加 、、 
> 	
> 	今天完成了 服务端 method 的check 方法调用，但是底层的检查逻辑 是需要继续完善的，
> 	
> 	需要继续完成服务端  method的protect方法。
> 	
> 	还需要再加上一个，不需要加 ，每一个profile 是跟 methodinfo 绑定在一起的，所以不会出现event的情况，
> 	
> 	后面如果要做demo的时候，需要在继续修改配置文件。
> 在服务端，e2e 处理的地方塞到 driver 层的method handler中。 忽略driver层的差异
> 在客户端，e2e 的处理应该放在哪里呢？ 需要进一步确定一下。

**确定一下，现在是在做DDS的method 的demo**



> [!TODO] Title
> 新的想法：
> ~~e2e check 是在创建msg 对象之前， 去掉头，避免多次拷贝~~
> ~~e2e  protect  刚刚申请内存之后，加上头， 避免多次拷贝~~


底层e2e 需要添加一个check 接口，分别在服务端和客户端进行check，之后再加
- 服务端需要把解析出来的source 加入到checkifno中，checkinfo' 需要全程引用传递



遇到了尴尬的地方，服务端和 客户端收到消息  check的时候，好像都需要在driver层调用 chenck 如何区分是 proxy 还是skeleton？
~~解决方案：在 增加一个回调函数，用来处理e2e Check的东西~~



2024.1.12
下面需要对 method中的 proxy端的  protect 端的 config文件进行读取 在初始化的时候，

~~读取完之后需要进行 加密protect~~




> [!ERROR] Title
> event_info->GetInstanceId(); 为什么会变成 65535 而不是1  
> 答案：
> 应该是初始化的顺序问题，还没有往eventid 中加入 instance信息，需要往下移动


> [!BUG] 
> 确定是e2e 在protect的时候 出现了问题
> 定位到是因为sourceid 应该是28位的，前面的四位必须是0，所以出错，但是在计算hash的时候导致的错误
> its_source_id & 0x0FFFFFFF




> [!bug] Title
> 上一个bug解决之后，出现了反序列化失败的问题，定位一下
> 最后是因为 e2e 回调没有返回值的原因，导致headersize =0




> [!TODO] method的 smachie
> method的只剩下状态机的调试了，加油




> [!TODO] Title
> 下一步进行vsomeip的  e2e 的测试







> [!DONE] 完成
> 完成结束，下一步进行代码合并
> 合并之后，继续field的 保护


2024-01-17 16:34
	tmp分支合并测试完成

2024-01-17 16:32

	1、someip method 测试完成

2024-01-17 16:33

	dds method 测试完成

 2024-01-17 16:37
	dds event测试完成
	
> [!BUG] DDS event中会有第一帧收不到
> 永远是一样的结果
> 	解决方法：
> 		建立通信需要时间，在publish 第一帧的时候，等待一段时间
> 	在field 中，有field的数据在， offer之前会发布一次数据，为什么要这样实现？
> 	


2024-01-17 17:04
	someip event测试完成

---
- [ ] json配置文件,添加field相关的信息 
- [ ] 添加field的config
- [ ] e2e field 相关的参数初始化
- [ ] 位field 添加e2e 保护
- [ ] Event场景，E2E保护失败，CM不发送该数据，并输出对应error日志
- [ ] 需要对照华为的e2e 文档,逐渐完善需求




> [!BUG] DDS Event BUG
> ![[Pasted image 20240119144655.png]]
> 10次之后，底层收到消息，但是不会上传给上层
> 	解决方法：
> 		某个地方没有释放，消息slot 不释放了



---
field 测试

2024-01-19 16:56 
	完成，dds field event 测试
	完成dds field getter测试
	完成dds field setter测试

接下来测试 someip的field
1、配置文件


---

# 3 继续开发其他的profile


> [!TODO] 后续可能要开发的东西
>1. 对于异步接收event数据的时候，无法进行超时检测，当后续开发同步接收接口的时候，需要考虑加上超时检测的功能。
>2. 



根据调查，可以猜测，任何profile都支持 event 和 method，所以都要事先这三个  check和  protect接口，但是当单独实现，但是需要符合method的检查流程

每个profile 也需要有 protect xm接口


## 3.1 完成一个  profile 05  并且进行单元测试



