

export LD_LIBRARY_PATH=“/home/lxh/workspace/modsar-middleware/generated_thirdparty/x86/lib:$LD_LIBRARY_PATH”



---
**dds 方法请求和回复数据量达到 1k的时候

	平均响应时间为1ms

![[Pasted image 20231116161739.png]]


--- 
**当数据量达到1M的时候

	出现bug，导致请求失败，偶发性，暂时不知原因(可能是底层dds的问题，最高可以达到500K)




# 1K数据测试结果（请求1K   回复1K）

---
测试设备列表：
1、s32G
2、千兆TPlink 路由器，wifi连接
3、网线
4、PC端虚拟机Zbook
5、请求时间间隔 200ms 一次

测试结果：
请求方式                                               平均请求时延                        请求次数
s32G请求-PC虚拟机回复                     4179 微秒                               1000
s32G请求-s32G回复                             1200 微秒                               1000
PC请求-S32G回复                                4713 微秒                               1000
PC请求-PC回复                                    811 微秒                                1000

---
测试设备列表：
1、s32G
2、千兆TPlink 路由器，网线直连
3、网线
4、PC端虚拟机Zbook

测试结果：
请求方式                                              平均请求时延                      请求次数
s32G请求-PC虚拟机回复                      1358 微妙                                   1000 
s32G请求-s32G回复                             1535 微秒                                  1000
PC请求-S32G回复                                 3085 微妙                                    1000
PC请求-PC回复                                     1899 微秒                                    1000

---
测试设备列表：
1、s32G
2、网线直连s32G（无路由器）
3、网线
4、PC端虚拟机Zbook

测试结果：
请求方式                                              平均请求时延                       请求次数
s32G请求-PC虚拟机回复                     2400                                      1000 
s32G请求-s32G回复                             1302                                        1000
PC请求-S32G回复                                2567                                       1000
PC请求-PC回复                                    1714                                          1000




DNU_BTIA_ZNI6WX
AwRB1gZJ9jeA