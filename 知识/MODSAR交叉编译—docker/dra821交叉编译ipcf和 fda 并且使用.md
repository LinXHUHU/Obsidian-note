
底层 fda
获取到数据之后，上传给skeleton，skeleton发布数据
只需要在pc虚拟机上跑一个，proxy



- [ ] 编译ipcf
- [x] 编译libdiag_shm   
- [ ] 编译fda  库 + 二进制



在proxy中  接收之后 是string 类型的数据  需要将其转化为  void  类型的指针数据的时候出错

解决，将string 转化为 void*  不能使用取地址 转化，会乱码，需要使用 string.data()  然后将char*  转化为 void*





