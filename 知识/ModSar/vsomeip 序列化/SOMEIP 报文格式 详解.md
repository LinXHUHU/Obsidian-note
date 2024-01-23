

[vsomeip —— 10分钟快速了解 vsomeip （vsomeip wiki 文档翻译）_Aliven888的博客-CSDN博客](https://blog.csdn.net/Aliven888/article/details/123333466)



原文

[vsomeip in 10 minutes · COVESA/vsomeip Wiki (github.com)](https://github.com/COVESA/vsomeip/wiki/vsomeip-in-10-minutes)



```
export LD_LIBRARY_PATH=../:${LD_LIBRARY_PATH}

export VSOMEIP_APPLICATION_NAME=client-sample

export VSOMEIP_APPLICATION_NAME=service-sample
service-sample



env VSOMEIP_CONFIGURATION=../../config/vsomeip-udp-client.json VSOMEIP_APPLICATION_NAME=client-sample ./subscribe-sample


```



# 10分钟了解vsomeip
## 简介

三个主要部分
- on-wire format 
- protocol
- SD



ff ff 81 00 00 00 00 4c 00 00 00 01 01 01 02 00 c0 00 00 00 00 00 00 20 01 00 00 10 a0 42 00 01 01 00 00 0a 00 00 00 00 01 01 00 10 73 82 00 01 01 00 00 0a 00 00 00 00 00 00 00 18 00 09 04 00 00 11 77 27 00 09 04 00 ac 14 03 04 00 11 77 27


[vector autosar someip与vsomeip对接经验总结 - oy182104619 - 博客园 (cnblogs.com)](https://www.cnblogs.com/ouyshy/p/15225302.html)
主要是遇到的几个问题



>[!Bug]- 测试callout
>1. 阿松大
>2. 阿松大
>3. 阿松大
>4. 阿迪斯
>5. 大师
>6. 阿松大


> [!info] 自定义标题
> 包裹的内容
> 可以是多行的内容


我们<u title="其实是一个奇怪的东西，不知道怎么使用，使用起来不是很方便">咖啡豆</u>喜欢的obsidian







```
notify 发送的sd报文，几秒钟发一次
ffff8100
00000030
00000015
01010200
c0000000
00000010
01000010
12345678
00000003
00000000
0000000c
00090400
ac140369
0006772d

ffff8100
00000030
00000ee5
01010200
c0000000
00000010
01000010
90150001
0100000a
00000000
0000000c
00090400
ac140304
00117727



 ffff8100
 00000024
 00000002
 01010200
 c0000000
 00000010
 00000000
 12345678
 ffffffff
 ffffffff
 00000000        


ffff8100
00000030
00000001
01010200
c0000000
00000010
06000010
90150001
01000003
00007001
0000000c
00900400
ac140307
001176c6
```