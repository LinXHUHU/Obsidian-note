---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
ffff8100 ^5YLj3hWc

00000030 ^BKTn4d8K

00000015 ^G8S5d1kQ

01010200 ^zDDC7QX1

c0000000 ^eHPgLDS4

00000010 ^HAKDVgRh

01000010 ^SPSIFq9w

12345678 ^5QfR3kWn

00000003 ^VHPf70Xc

00000000 ^vOQ87Kty

0000000c ^cL16dO2d

00090400 ^qikQVbYc

ac140369 ^mEMJ1JjV

0006772d ^66RPKJBR

service id
SD 固定 ^AsnqSIgB

method id
SD 固定
 ^hKJUBkse

剩余数据的长度 ^NfgAaqvq

client id ^6Wlb3eza

Session id ^Na6HjBbC

这些是固定下来的SD 报文的特殊的地方 ^kDiWDYw7

Flag ^FwrKIddm

Entries的长度，此时为16字节   一个entry为 16字节   所以只有一个eentry ^DZjpwuP2

entry 1 ^fWeG4W7Y

Service Entry 用于服务发现 ^ux5yO4iw

Offer ^h4DmpXXn

service id ^xRAeCenZ

instance id ^trmRH1pC

ffff8100 ^UDOtPUxS

00000030 ^i4bNbpCU

00000ee5 ^F8bhXvc6

01010200 ^gM8sYbQZ

c0000000 ^F4GyqJg6

00000010 ^iGSw8wJ6

01000010 ^GjgUqUYA

90150001 ^PrbuYlI4

0100000a ^Hur7guEd

00000000 ^yJX94yYA

0000000c ^RLHi0pTZ

00090400 ^ZFgCL5pb

ac140304 ^QjtqCsnm

00117727 ^eXCV7mRp

ffff8100 ^yAgTIzPi

00000024 ^pclIIdph

00000002 ^anAYAsT3

01010200 ^S9nwtV8S

c0000000 ^cXRKsItg

00000010 ^0YSCWSK5

00000000 ^mgkzBhv2

12345678 ^eKwKXi1e

ffffffff ^wFvV7QR3

ffffffff ^7wfhTDt8

00000000 ^iWvg51tR

长度为16 byte ^0X0XIPPV

find servoce ^T1Ut309A

option array ^6MRhbMd8

option array len = 12 字节 ^iJgU9UBM

长度 ^qteMDo92

type ipv4 ^SZmvT1a6

保留 ^wTyEWpQf

ip 地址 172.20.3.105 ^eAewVCi9

端口号 30509 ^pTr2X7VF

subscribe 发送的SD 报文 ^OauwLNGe

notify 发送的SD 报文 ^484V0ODu

板子 发送的SD 报文，退测就是notify的 ^fuiZ1YJt

ffff8100 ^yl8lUszY

00000030 ^1xqsVllJ

00000001 ^9fZodvWZ

01010200 ^sWC3Sp49

c0000000 ^LXLDoZVb

00000010 ^MRqS736a

06000010 ^8DVTAsXS

90150001 ^7UpzE76S

01000003 ^ZueW8TAE

00007001 ^bcjKtQSQ

0000000c ^UEm5jdtS

00900400 ^cyyQG7df

ac140307 ^t0te6rL2

001176c6 ^aXw5xsA9

事件组 ^9Xsf8ZNl

Subscribe ^yMj4777c

Event Group id ^E182yYPi

这里应该是一个SD的订阅报文 ^0qk0J0Z4

表示发出此报文的source地址，172.20.3.7
目的地址是172.20.3.4 ^FZ4i8Bje

[[任务看板.canvas]] ^AIsMWF9t

现在的问题：没有发送订阅报文， 但是已经  on_available了，说明服务成功解析了SD报文，但是没有发出订阅报文，这是个问题

还有 对方的ARp协议不能使用，导致ping 不通
    

是因为arp导致的吗？ 程序中是否先发送了 icmp报文 看目标是否通？
解决思路：搜索底层的程序实现，找问题所在 ^hLtAgYx5

这里是  订阅过程的源码详细解释，明天按照这个打 log ^5eVnV173

ff  ff  81  00 
00  00  00  40  
00  00  00  04  
01  01  02  00  
c0  00  00  00  
00  00  00  20  
06  00  00  10  
90  15  00  01  
01  00  00  00 
 00  00  70  01 
 06  00  00  10  
90  15  00  01  
01  00  00  03  
00  00  70  01 
 00  00  00  0c 
 00  09  04  00 
 ac  14  03  02 
 00  11  9c  40  ^OJ9VuPdK

d ^RDuFHf0m

  aa bb cc dd ee 03 
aa bb cc dd ee 01 
08 00 45 00
  00 54
 45 e5 
40 00 40 11 
96 85 
ac 14 03 02 ac 14
  03 04 77 1a 77 1a 00 40 17 fd ff ff 81 00 00 00
  00 30 00 00 00 26 01 01 02 00 c0 00 00 00 00 00
  00 10 06 00 00 10 90 15 00 01 01 00 00 00 00 00
  70 01 00 00 00 0c 00 09 04 00 ac 14 03 02 00 11
  9c 40 ^AZTcnChN

DC 65 ^0TIXiiwW

FFFF8100
00000024
0000004d
01010200
c0000000
00000010
07000000
19050001
01000000
00000001
00000000 ^ghotJYdO

长度 16 ^a44bAtVN

TTL 有问题 ^k3st6Mlp

排除TTL的问题 ^wyYH4Cud

因为ttl为0  所以断定是一个 subscribe_nack ^BA6YTTjo

今日收获：
    1、解决了由于防火墙导致的收不到组播报文的问题
    2、查找到返回的ack报文是属于nack类型的，由ttl 和 type字段共同决定
    3、SD的on_message方法是处理这个的

后续工作：
    1、查找为什么导致的返回nack，是否跟订阅报文的东西，ttl有关？

    2、从配置文件中找问题，查看vsomeip.json 中的client 中的部分，需要有相关信息的。很重要 ^NjcaFLmO

FFFF8100
00000040
00000005
01010200
c0000000
00000020
06000010
19050001
01000000
00000001
06000010
19050001
01000064
00000001
0000000c
00090400
ac140369
0011ae26 ^ms7diM9G

对于Offer/ StopOfferService、Subscribe/ StopSubscribe和SubscribeAck/ Nack，
每一组Entries都共用了相同的Type值，但通过TTL字段可以识别究竟是提供服务还是
停止提供服务，是订阅事件还是取消订阅，是订阅成功应答还是订阅失败应答：当TTL = 0时，
表示报文对应的服务实例不再有效，此时对应的Type类型分别就是停止提供服务、停止订阅事件
以及订阅失败应答。 ^YyLIArUo

版本号 ^i8LCbEo2

ttl 为0 表示STOP订阅？ ^Vqh1AITl

FFFF8100
00000030
00000001
01010200
c0000000
00000010
06000010
19050001
01000064
00000001
0000000c
00090400
ac140369
00119c40 ^CuWJIjNh

这里是先发送了 正常的订阅报文，
然后订阅失败，给出了nack报文

然后我这里重新发布了订阅报文，表示先取消订阅，然后重新订阅，2个entry ^auhzV99P

到这里，最后的一个方法是完全模拟，对方的ip，报文完全一致，再试试看

订阅失败的原因
    1、服务不可用------应该不会   现在是1905  0001，   0001
    2、第二种是订阅权限的问题？
    3、其他未知问题！ ^rVi5VeUT

确定是不是因为端口的问题，是因为 ip 和mac地址的权限问题 ^hsS398DA

修改 ip 为 172.20.3.7
修改 mac 为 aa:bb:cc:dd:ee:06 ^i8xuG2BG

单独修改ip之后，返回的mac 地址为 aabbccddee06 能抓包成功，但是程序不能收到，奇怪吧 ^GlHtuNvd

19059012
00000015
000059d1
01010200
payload ^8Hu2lj8V

19059012
00000015
000059d2
01010200
payload ^almZxgsC

19059013
00000015
000059d2
01010200
payload ^8UFJbINr

19059013
00000015
000059d2
01010200
payload ^POtTlWtV

修改ip  和mac 成功 解决了

出现新的问题： 只能接收到 一次 的 notify 报文，其他 的报文都被抛弃掉，定位原因 ^ULtjSrEK

原因： 在 routing_manager_impl.cpp：2452附近， its_subscribers 大小为0.  
打印出来的为 1
没能打印出来的为0

查找为什么这个 会变成 0 ^Co0pugU7

原因是 被过滤掉了， 过滤原因  在app 的地方在  request event的时候  类型写成了  field 导致 被过滤掉 

为什么要有这种机制 是未知的， 条件是 因为 三个
1、type 是 field
2、不是强制执行的
3、payload 没有改变 ^Zgcim9O7

发现端口也必须一致 必须为30406  ，所以比较严格
 ^lzl4AEPn


# Embedded files
2d2d6ddb25345372017c49b7bcdb05e01488791f: [[Pasted Image 20240104135615_232.png]]

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.0.2",
	"elements": [
		{
			"type": "text",
			"version": 94,
			"versionNonce": 843736905,
			"isDeleted": false,
			"id": "5YLj3hWc",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": -886.8365743903476,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 231.69554138183594,
			"height": 66.4888840828306,
			"seed": 1245155583,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626448,
			"fontFamily": 1,
			"text": "ffff8100",
			"rawText": "ffff8100",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ffff8100",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 996756935,
			"isDeleted": false,
			"id": "BKTn4d8K",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": -793.7521366743847,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 292.3853759765625,
			"height": 66.4888840828306,
			"seed": 1132806769,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626448,
			"fontFamily": 1,
			"text": "00000030",
			"rawText": "00000030",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000030",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 82875945,
			"isDeleted": false,
			"id": "G8S5d1kQ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": -700.6676989584219,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 266.8541564941406,
			"height": 66.4888840828306,
			"seed": 339417375,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626448,
			"fontFamily": 1,
			"text": "00000015",
			"rawText": "00000015",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000015",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 1890188519,
			"isDeleted": false,
			"id": "zDDC7QX1",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": -607.583261242459,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 249.6737823486328,
			"height": 66.4888840828306,
			"seed": 863358033,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626448,
			"fontFamily": 1,
			"text": "01010200",
			"rawText": "01010200",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "01010200",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 1152248073,
			"isDeleted": false,
			"id": "eHPgLDS4",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": -514.4988235264962,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 282.8643493652344,
			"height": 66.4888840828306,
			"seed": 1087937855,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.191107266264474,
			"fontFamily": 1,
			"text": "c0000000",
			"rawText": "c0000000",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "c0000000",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 115,
			"versionNonce": 340248583,
			"isDeleted": false,
			"id": "HAKDVgRh",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": -421.4143858105333,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 270.57745361328125,
			"height": 66.4888840828306,
			"seed": 1283070513,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626448,
			"fontFamily": 1,
			"text": "00000010",
			"rawText": "00000010",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000010",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 184410089,
			"isDeleted": false,
			"id": "SPSIFq9w",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": -328.32994809457045,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 248.397216796875,
			"height": 66.4888840828306,
			"seed": 1668324703,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626448,
			"fontFamily": 1,
			"text": "01000010",
			"rawText": "01000010",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "01000010",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 339685159,
			"isDeleted": false,
			"id": "5QfR3kWn",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": -235.2455103786076,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 258.769287109375,
			"height": 66.48888408283061,
			"seed": 1064938513,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626449,
			"fontFamily": 1,
			"text": "12345678",
			"rawText": "12345678",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "12345678",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 904657609,
			"isDeleted": false,
			"id": "VHPf70Xc",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": -142.16107266264476,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 292.3853454589844,
			"height": 66.4888840828306,
			"seed": 1330878847,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626448,
			"fontFamily": 1,
			"text": "00000003",
			"rawText": "00000003",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000003",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 1794945607,
			"isDeleted": false,
			"id": "vOQ87Kty",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": -49.07663494668196,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 292.7576904296875,
			"height": 66.4888840828306,
			"seed": 879493617,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626448,
			"fontFamily": 1,
			"text": "00000000",
			"rawText": "00000000",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000000",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 1444133289,
			"isDeleted": false,
			"id": "cL16dO2d",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": 44.007802769280886,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 282.86431884765625,
			"height": 66.4888840828306,
			"seed": 432148895,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.191107266264474,
			"fontFamily": 1,
			"text": "0000000c",
			"rawText": "0000000c",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "0000000c",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 291295591,
			"isDeleted": false,
			"id": "qikQVbYc",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": 137.0922404852437,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 286.0025634765625,
			"height": 66.4888840828306,
			"seed": 1750637521,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626448,
			"fontFamily": 1,
			"text": "00090400",
			"rawText": "00090400",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00090400",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 1554029705,
			"isDeleted": false,
			"id": "mEMJ1JjV",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": 230.17667820120656,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 249.8865509033203,
			"height": 66.4888840828306,
			"seed": 1542227391,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626448,
			"fontFamily": 1,
			"text": "ac140369",
			"rawText": "ac140369",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ac140369",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 816581767,
			"isDeleted": false,
			"id": "66RPKJBR",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.25,
			"y": 323.2611159171694,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 269.19451904296875,
			"height": 66.48888408283061,
			"seed": 190249393,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 53.19110726626449,
			"fontFamily": 1,
			"text": "0006772d",
			"rawText": "0006772d",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "0006772d",
			"lineHeight": 1.25,
			"baseline": 46
		},
		{
			"type": "freedraw",
			"version": 38,
			"versionNonce": 156115817,
			"isDeleted": false,
			"id": "1cWPdxAQ41CTULN-Ijemf",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -23.9203132857657,
			"y": -1017.5414325958608,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 1232066239,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 62,
			"versionNonce": 346481575,
			"isDeleted": false,
			"id": "b-lQgYC7nhhjjHDQSGoxY",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -151.65127890157612,
			"y": -830.775146737449,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 98.74999022398788,
			"height": 2.146738917912785,
			"seed": 1558297375,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.146738917912785,
					0
				],
				[
					6.440216753738355,
					0
				],
				[
					12.88043350747671,
					0
				],
				[
					20.3940197201714,
					1.0733694589564493
				],
				[
					25.760867014953305,
					1.0733694589564493
				],
				[
					33.27445322764811,
					2.146738917912785
				],
				[
					37.56793106347368,
					2.146738917912785
				],
				[
					41.86140889929925,
					2.146738917912785
				],
				[
					47.228256194081155,
					2.146738917912785
				],
				[
					52.59510348886306,
					2.146738917912785
				],
				[
					57.96195078364508,
					2.146738917912785
				],
				[
					64.40216753738343,
					2.146738917912785
				],
				[
					69.76901483216534,
					2.146738917912785
				],
				[
					71.91575375007812,
					2.146738917912785
				],
				[
					75.13586212694736,
					2.146738917912785
				],
				[
					78.35597050381648,
					2.146738917912785
				],
				[
					83.72281779859838,
					2.146738917912785
				],
				[
					85.86955671651117,
					2.146738917912785
				],
				[
					91.23640401129319,
					2.146738917912785
				],
				[
					93.38314292920597,
					2.146738917912785
				],
				[
					94.45651238816231,
					2.146738917912785
				],
				[
					96.6032513060751,
					2.146738917912785
				],
				[
					97.67662076503154,
					2.146738917912785
				],
				[
					98.74999022398788,
					2.146738917912785
				],
				[
					98.74999022398788,
					2.146738917912785
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 66,
			"versionNonce": 409456201,
			"isDeleted": false,
			"id": "ujJalFw1dhNpu3JIN1Q2c",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -23.9203132857657,
			"y": -826.4816689016234,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 106.26357643668268,
			"height": 3.2201083768691205,
			"seed": 1652190847,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-1.0733694589564493
				],
				[
					5.3668472947819055,
					-2.146738917912785
				],
				[
					11.80706404852026,
					-3.2201083768691205
				],
				[
					18.247280802258615,
					-3.2201083768691205
				],
				[
					21.46738917912785,
					-3.2201083768691205
				],
				[
					24.68749755599697,
					-3.2201083768691205
				],
				[
					27.90760593286609,
					-3.2201083768691205
				],
				[
					33.27445322764811,
					-3.2201083768691205
				],
				[
					37.56793106347368,
					-3.2201083768691205
				],
				[
					46.15488673512482,
					-3.2201083768691205
				],
				[
					50.44836457095039,
					-3.2201083768691205
				],
				[
					54.741842406775845,
					-3.2201083768691205
				],
				[
					60.108689701557864,
					-3.2201083768691205
				],
				[
					65.47553699633977,
					-3.2201083768691205
				],
				[
					71.91575375007812,
					-3.2201083768691205
				],
				[
					75.13586212694736,
					-3.2201083768691205
				],
				[
					79.42933996277281,
					-3.2201083768691205
				],
				[
					81.5760788806856,
					-3.2201083768691205
				],
				[
					82.64944833964205,
					-3.2201083768691205
				],
				[
					86.94292617546762,
					-3.2201083768691205
				],
				[
					89.0896650933804,
					-3.2201083768691205
				],
				[
					92.30977347024952,
					-3.2201083768691205
				],
				[
					95.52988184711876,
					-2.146738917912785
				],
				[
					99.82335968294433,
					-2.146738917912785
				],
				[
					101.97009860085711,
					-2.146738917912785
				],
				[
					104.1168375187699,
					-1.0733694589564493
				],
				[
					105.19020697772623,
					-1.0733694589564493
				],
				[
					106.26357643668268,
					-1.0733694589564493
				],
				[
					106.26357643668268,
					-1.0733694589564493
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 50,
			"versionNonce": 1568265927,
			"isDeleted": false,
			"id": "6z0R1lI8E6CRlloevlIYW",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -151.65127890157612,
			"y": -898.3974226517015,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 266.19562582118476,
			"height": 53.66847294781951,
			"seed": 717870687,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-6.440216753738355,
					-2.146738917912785
				],
				[
					-22.540758638084185,
					-5.3668472947819055
				],
				[
					-46.15488673512482,
					-9.660325130607475
				],
				[
					-69.76901483216534,
					-16.10054188434583
				],
				[
					-104.1168375187699,
					-24.68749755599697
				],
				[
					-157.7853104665893,
					-35.421192145560894
				],
				[
					-193.2065026121502,
					-41.861408899299136
				],
				[
					-220.04073908605994,
					-47.228256194081155
				],
				[
					-242.58149772414413,
					-50.448364570950275
				],
				[
					-257.6086701495336,
					-52.595103488863174
				],
				[
					-264.048886903272,
					-53.66847294781951
				],
				[
					-266.19562582118476,
					-53.66847294781951
				],
				[
					-266.19562582118476,
					-53.66847294781951
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 50,
			"versionNonce": 818486569,
			"isDeleted": false,
			"id": "gQnJzGtc16audHtSAFxrk",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -409.25994905110974,
			"y": -967.0930680249105,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 16.10054188434583,
			"height": 28.98097539182254,
			"seed": 282138687,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-2.146738917912785,
					0
				],
				[
					-6.440216753738355,
					3.2201083768692342
				],
				[
					-11.80706404852026,
					5.366847294782019
				],
				[
					-15.027172425389494,
					7.513586212694804
				],
				[
					-16.10054188434583,
					8.58695567165114
				],
				[
					-16.10054188434583,
					9.660325130607589
				],
				[
					-16.10054188434583,
					12.88043350747671
				],
				[
					-9.660325130607475,
					20.3940197201714
				],
				[
					-5.3668472947819055,
					23.614128097040634
				],
				[
					-2.146738917912785,
					26.83423647390987
				],
				[
					0,
					27.907605932866204
				],
				[
					0,
					28.98097539182254
				],
				[
					0,
					28.98097539182254
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 94,
			"versionNonce": 1908499943,
			"isDeleted": false,
			"id": "AsnqSIgB",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -572.412106812481,
			"y": -990.707196121951,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 91.97990417480469,
			"height": 50,
			"seed": 2104186399,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "service id\nSD 固定",
			"rawText": "service id\nSD 固定",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "service id\nSD 固定",
			"lineHeight": 1.25,
			"baseline": 43
		},
		{
			"type": "freedraw",
			"version": 53,
			"versionNonce": 299733001,
			"isDeleted": false,
			"id": "_AfKmQ0WpHvIkWOO9vTHa",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 88.78347990465522,
			"y": -886.5903586031811,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 132.024443451636,
			"height": 93.38314292920609,
			"seed": 1052019167,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-1.0733694589564493
				],
				[
					3.2201083768691205,
					-4.29347783582557
				],
				[
					16.10054188434583,
					-9.660325130607589
				],
				[
					47.22825619408127,
					-28.98097539182254
				],
				[
					65.47553699633977,
					-42.9347783582557
				],
				[
					76.20923158590381,
					-50.44836457095039
				],
				[
					106.26357643668257,
					-74.06249266799091
				],
				[
					119.14400994415928,
					-81.57607888068571
				],
				[
					125.58422669789775,
					-85.86955671651128
				],
				[
					127.73096561581042,
					-89.08966509338052
				],
				[
					128.80433507476687,
					-90.16303455233685
				],
				[
					129.87770453372332,
					-91.23640401129319
				],
				[
					130.95107399267954,
					-92.30977347024964
				],
				[
					132.024443451636,
					-92.30977347024964
				],
				[
					132.024443451636,
					-93.38314292920609
				],
				[
					132.024443451636,
					-93.38314292920609
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 52,
			"versionNonce": 814354695,
			"isDeleted": false,
			"id": "UiMuvublipDHkTg2XTshp",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 205.78075093090183,
			"y": -984.2669793682128,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 27.90760593286609,
			"height": 31.127714309735325,
			"seed": 1950695455,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					3.2201083768691205,
					-1.0733694589563356
				],
				[
					8.58695567165114,
					-2.1467389179126712
				],
				[
					16.10054188434583,
					-3.2201083768691205
				],
				[
					24.68749755599697,
					-4.293477835825456
				],
				[
					25.76086701495342,
					-5.3668472947819055
				],
				[
					26.83423647390964,
					-5.3668472947819055
				],
				[
					27.90760593286609,
					-2.1467389179126712
				],
				[
					27.90760593286609,
					1.0733694589564493
				],
				[
					27.90760593286609,
					5.366847294782019
				],
				[
					25.76086701495342,
					11.807064048520374
				],
				[
					23.61412809704052,
					18.24728080225873
				],
				[
					22.54075863808407,
					23.614128097040748
				],
				[
					22.54075863808407,
					25.76086701495342
				],
				[
					23.61412809704052,
					24.687497555997084
				],
				[
					23.61412809704052,
					24.687497555997084
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 57,
			"versionNonce": 27305705,
			"isDeleted": false,
			"id": "hKJUBkse",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 265.8894406324596,
			"y": -1002.5142601704713,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 92.99990844726562,
			"height": 75,
			"seed": 68552255,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "method id\nSD 固定\n",
			"rawText": "method id\nSD 固定\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "method id\nSD 固定\n",
			"lineHeight": 1.25,
			"baseline": 68
		},
		{
			"type": "freedraw",
			"version": 87,
			"versionNonce": 1666209831,
			"isDeleted": false,
			"id": "mUMkHz2RnQJDikdwD-9ir",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -147.35780106575055,
			"y": -740.6121121851122,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 295.1766012130073,
			"height": 6.4402167537384685,
			"seed": 608909663,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					5.3668472947819055,
					0
				],
				[
					11.80706404852026,
					1.0733694589564493
				],
				[
					19.320650261215064,
					1.0733694589564493
				],
				[
					24.68749755599697,
					2.1467389179128986
				],
				[
					30.054344850778875,
					2.1467389179128986
				],
				[
					36.49456160451723,
					2.1467389179128986
				],
				[
					42.934778358255585,
					2.1467389179128986
				],
				[
					50.448364570950275,
					2.1467389179128986
				],
				[
					65.47553699633977,
					3.2201083768692342
				],
				[
					74.06249266799091,
					3.2201083768692342
				],
				[
					83.72281779859838,
					3.2201083768692342
				],
				[
					93.38314292920597,
					4.29347783582557
				],
				[
					100.89672914190066,
					5.366847294782019
				],
				[
					111.63042373146459,
					5.366847294782019
				],
				[
					120.21737940311573,
					5.366847294782019
				],
				[
					126.65759615685397,
					5.366847294782019
				],
				[
					136.31792128746156,
					5.366847294782019
				],
				[
					147.05161587702548,
					5.366847294782019
				],
				[
					155.6385715486765,
					5.366847294782019
				],
				[
					165.2988966792841,
					5.366847294782019
				],
				[
					171.73911343302245,
					6.4402167537384685
				],
				[
					178.1793301867607,
					6.4402167537384685
				],
				[
					182.47280802258626,
					6.4402167537384685
				],
				[
					185.6929163994555,
					5.366847294782019
				],
				[
					186.76628585841183,
					5.366847294782019
				],
				[
					188.91302477632462,
					3.2201083768692342
				],
				[
					191.0597636942374,
					3.2201083768692342
				],
				[
					193.2065026121502,
					2.1467389179128986
				],
				[
					197.49998044797576,
					1.0733694589564493
				],
				[
					206.0869361196269,
					1.0733694589564493
				],
				[
					212.52715287336525,
					1.0733694589564493
				],
				[
					220.04073908605994,
					1.0733694589564493
				],
				[
					229.70106421666753,
					1.0733694589564493
				],
				[
					240.43475880623134,
					1.0733694589564493
				],
				[
					252.2418228547516,
					1.0733694589564493
				],
				[
					267.2689952801412,
					1.0733694589564493
				],
				[
					271.5624731159668,
					2.1467389179128986
				],
				[
					275.85595095179235,
					2.1467389179128986
				],
				[
					279.0760593286615,
					3.2201083768692342
				],
				[
					281.22279824657414,
					3.2201083768692342
				],
				[
					283.36953716448704,
					3.2201083768692342
				],
				[
					284.44290662344326,
					3.2201083768692342
				],
				[
					286.58964554135616,
					3.2201083768692342
				],
				[
					287.6630150003126,
					3.2201083768692342
				],
				[
					288.73638445926883,
					3.2201083768692342
				],
				[
					289.8097539182253,
					3.2201083768692342
				],
				[
					291.9564928361382,
					3.2201083768692342
				],
				[
					294.10323175405085,
					3.2201083768692342
				],
				[
					295.1766012130073,
					3.2201083768692342
				],
				[
					295.1766012130073,
					3.2201083768692342
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 47,
			"versionNonce": 2057167305,
			"isDeleted": false,
			"id": "oC93caokINs1YXsmSPTUn",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 175.72640608012284,
			"y": -765.2996097411092,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 182.47280802258638,
			"height": 11.807064048520374,
			"seed": 2032580575,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					15.027172425389494,
					-1.0733694589563356
				],
				[
					32.201083768691774,
					-1.0733694589563356
				],
				[
					61.182059160514314,
					-1.0733694589563356
				],
				[
					91.23640401129319,
					2.1467389179128986
				],
				[
					122.3641183210284,
					6.4402167537384685
				],
				[
					151.34509371285094,
					9.660325130607589
				],
				[
					177.10596072780436,
					10.733694589564038
				],
				[
					181.39943856362993,
					10.733694589564038
				],
				[
					182.47280802258638,
					10.733694589564038
				],
				[
					182.47280802258638,
					10.733694589564038
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 52,
			"versionNonce": 1879096135,
			"isDeleted": false,
			"id": "7IGICj8oyjsFdJTt-PXwd",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 345.3187805952325,
			"y": -769.5930875769347,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 22.5407586380843,
			"height": 24.68749755599697,
			"seed": 49987935,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.1467389179126712,
					0
				],
				[
					5.366847294782019,
					3.2201083768692342
				],
				[
					9.660325130607589,
					6.4402167537384685
				],
				[
					13.953802966433159,
					9.660325130607589
				],
				[
					18.24728080225873,
					11.807064048520374
				],
				[
					20.3940197201714,
					12.88043350747671
				],
				[
					21.46738917912785,
					12.88043350747671
				],
				[
					22.5407586380843,
					12.88043350747671
				],
				[
					21.46738917912785,
					15.027172425389608
				],
				[
					17.17391134330228,
					19.320650261215064
				],
				[
					13.953802966433159,
					21.46738917912785
				],
				[
					10.733694589563811,
					23.614128097040634
				],
				[
					9.660325130607589,
					24.68749755599697
				],
				[
					8.58695567165114,
					24.68749755599697
				],
				[
					8.58695567165114,
					24.68749755599697
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 68,
			"versionNonce": 435208361,
			"isDeleted": false,
			"id": "NfgAaqvq",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 400.06062300200847,
			"y": -768.5197181179783,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 140,
			"height": 25,
			"seed": 1552867199,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "剩余数据的长度",
			"rawText": "剩余数据的长度",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "剩余数据的长度",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 75,
			"versionNonce": 1257749095,
			"isDeleted": false,
			"id": "mxY9xpauNgOTfPQkxnXD_",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -148.43117052470689,
			"y": -650.4490776327754,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 136.31792128746144,
			"height": 5.3668472947819055,
			"seed": 796168113,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.146738917912785,
					-1.0733694589563356
				],
				[
					3.2201083768691205,
					-2.146738917912785
				],
				[
					9.660325130607475,
					-3.2201083768692342
				],
				[
					15.02717242538938,
					-4.29347783582557
				],
				[
					20.3940197201714,
					-5.3668472947819055
				],
				[
					24.68749755599697,
					-5.3668472947819055
				],
				[
					31.12771430973521,
					-5.3668472947819055
				],
				[
					34.347822686604445,
					-5.3668472947819055
				],
				[
					39.71466998138635,
					-5.3668472947819055
				],
				[
					46.154886735124705,
					-5.3668472947819055
				],
				[
					51.521734029906725,
					-5.3668472947819055
				],
				[
					59.035320242601415,
					-4.29347783582557
				],
				[
					65.47553699633977,
					-3.2201083768692342
				],
				[
					69.76901483216534,
					-3.2201083768692342
				],
				[
					77.28260104486003,
					-3.2201083768692342
				],
				[
					80.50270942172926,
					-3.2201083768692342
				],
				[
					84.79618725755472,
					-3.2201083768692342
				],
				[
					89.08966509338029,
					-3.2201083768692342
				],
				[
					93.38314292920586,
					-2.146738917912785
				],
				[
					98.74999022398788,
					-2.146738917912785
				],
				[
					103.04346805981345,
					-2.146738917912785
				],
				[
					108.41031535459535,
					-2.146738917912785
				],
				[
					111.63042373146448,
					-2.146738917912785
				],
				[
					115.92390156729005,
					-2.146738917912785
				],
				[
					119.14400994415928,
					-3.2201083768692342
				],
				[
					121.29074886207206,
					-3.2201083768692342
				],
				[
					123.43748777998485,
					-3.2201083768692342
				],
				[
					124.51085723894118,
					-3.2201083768692342
				],
				[
					126.65759615685397,
					-3.2201083768692342
				],
				[
					126.65759615685397,
					-4.29347783582557
				],
				[
					127.73096561581042,
					-4.29347783582557
				],
				[
					128.80433507476675,
					-4.29347783582557
				],
				[
					130.95107399267954,
					-4.29347783582557
				],
				[
					132.024443451636,
					-4.29347783582557
				],
				[
					133.09781291059232,
					-4.29347783582557
				],
				[
					135.2445518285051,
					-4.29347783582557
				],
				[
					136.31792128746144,
					-4.29347783582557
				],
				[
					136.31792128746144,
					-4.29347783582557
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 45,
			"versionNonce": 1296352137,
			"isDeleted": false,
			"id": "pM6pS8o5_n95PhnL3Xbte",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -165.60508186800917,
			"y": -671.9164668119031,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 107.33694589563902,
			"height": 7.513586212694804,
			"seed": 130091697,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-4.29347783582557,
					0
				],
				[
					-15.027172425389494,
					1.0733694589563356
				],
				[
					-36.49456160451723,
					1.0733694589563356
				],
				[
					-64.40216753738343,
					1.0733694589563356
				],
				[
					-95.52988184711876,
					-1.0733694589564493
				],
				[
					-106.26357643668263,
					-6.4402167537384685
				],
				[
					-107.33694589563902,
					-6.4402167537384685
				],
				[
					-107.33694589563902,
					-6.4402167537384685
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 51,
			"versionNonce": 687986055,
			"isDeleted": false,
			"id": "Ix948QuagLDNPAnp0P1hH",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -279.38224451738654,
			"y": -693.3838559910309,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 23.614128097040577,
			"height": 36.49456160451723,
			"seed": 875729265,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-1.0733694589563925,
					0
				],
				[
					-4.29347783582557,
					2.1467389179126712
				],
				[
					-13.953802966433045,
					8.58695567165114
				],
				[
					-19.320650261215008,
					11.80706404852026
				],
				[
					-21.467389179127792,
					13.953802966433045
				],
				[
					-22.540758638084185,
					16.10054188434583
				],
				[
					-22.540758638084185,
					18.247280802258615
				],
				[
					-23.614128097040577,
					18.247280802258615
				],
				[
					-22.540758638084185,
					18.247280802258615
				],
				[
					-13.953802966433045,
					25.76086701495342
				],
				[
					-7.513586212694747,
					30.054344850778875
				],
				[
					-2.146738917912785,
					34.347822686604445
				],
				[
					0,
					36.49456160451723
				],
				[
					0,
					36.49456160451723
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 69,
			"versionNonce": 1087728233,
			"isDeleted": false,
			"id": "7Ezs4vPR31yl53v2k2tTQ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 11.500878859795193,
			"y": -645.0822303379935,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 90.16303455233674,
			"height": 1.0733694589564493,
			"seed": 413732721,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					3.2201083768691205,
					0
				],
				[
					9.660325130607475,
					0
				],
				[
					17.17391134330228,
					0
				],
				[
					28.98097539182254,
					0
				],
				[
					36.49456160451723,
					0
				],
				[
					40.7880394403428,
					0
				],
				[
					45.08151727616837,
					0
				],
				[
					47.228256194081155,
					0
				],
				[
					51.521734029906725,
					0
				],
				[
					53.66847294781951,
					0
				],
				[
					55.815211865732294,
					0
				],
				[
					57.96195078364508,
					0
				],
				[
					61.1820591605142,
					0
				],
				[
					64.40216753738343,
					0
				],
				[
					66.54890645529622,
					0
				],
				[
					67.62227591425255,
					0
				],
				[
					68.695645373209,
					0
				],
				[
					69.76901483216534,
					0
				],
				[
					70.84238429112179,
					0
				],
				[
					72.98912320903457,
					0
				],
				[
					75.13586212694736,
					0
				],
				[
					76.2092315859037,
					0
				],
				[
					78.35597050381648,
					0
				],
				[
					79.42933996277281,
					0
				],
				[
					81.5760788806856,
					0
				],
				[
					82.64944833964205,
					0
				],
				[
					84.79618725755483,
					1.0733694589564493
				],
				[
					85.86955671651117,
					1.0733694589564493
				],
				[
					88.01629563442395,
					1.0733694589564493
				],
				[
					89.0896650933804,
					1.0733694589564493
				],
				[
					90.16303455233674,
					1.0733694589564493
				],
				[
					90.16303455233674,
					1.0733694589564493
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 66,
			"versionNonce": 1901825191,
			"isDeleted": false,
			"id": "-aN3g_qev7bobcRAU6vjl",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 152.11227798308232,
			"y": -661.1827722223393,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 188.91302477632462,
			"height": 4.29347783582557,
			"seed": 1400415025,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.0733694589563356,
					0
				],
				[
					6.440216753738355,
					-1.0733694589564493
				],
				[
					26.834236473909755,
					-1.0733694589564493
				],
				[
					49.37499511199394,
					-1.0733694589564493
				],
				[
					70.84238429112168,
					-1.0733694589564493
				],
				[
					92.30977347024952,
					-1.0733694589564493
				],
				[
					112.70379319042092,
					0
				],
				[
					121.29074886207206,
					0
				],
				[
					127.73096561581042,
					0
				],
				[
					130.95107399267954,
					0
				],
				[
					135.2445518285051,
					0
				],
				[
					138.46466020537434,
					0
				],
				[
					142.7581380411999,
					0
				],
				[
					150.2717242538945,
					0
				],
				[
					153.49183263076384,
					0
				],
				[
					161.00541884345853,
					0
				],
				[
					164.22552722032765,
					0
				],
				[
					166.37226613824055,
					0
				],
				[
					167.44563559719677,
					0
				],
				[
					168.51900505615322,
					0
				],
				[
					171.73911343302234,
					1.0733694589564493
				],
				[
					172.8124828919788,
					1.0733694589564493
				],
				[
					174.95922180989146,
					1.0733694589564493
				],
				[
					178.1793301867608,
					1.0733694589564493
				],
				[
					181.39943856362993,
					2.146738917912785
				],
				[
					185.6929163994555,
					3.2201083768691205
				],
				[
					187.83965531736817,
					3.2201083768691205
				],
				[
					188.91302477632462,
					3.2201083768691205
				],
				[
					188.91302477632462,
					3.2201083768691205
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 56,
			"versionNonce": 225326409,
			"isDeleted": false,
			"id": "gG2nFBGqCgUVZT_TDwr6K",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 335.6584554646249,
			"y": -676.2099446477287,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 42.93477835825547,
			"height": 51.52173402990661,
			"seed": 639299921,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.0733694589564493,
					3.2201083768691205
				],
				[
					4.29347783582557,
					7.51358621269469
				],
				[
					6.4402167537384685,
					12.880433507476596
				],
				[
					8.58695567165114,
					16.10054188434583
				],
				[
					10.733694589564038,
					19.32065026121495
				],
				[
					12.88043350747671,
					21.467389179127736
				],
				[
					15.027172425389608,
					22.54075863808407
				],
				[
					16.10054188434583,
					22.54075863808407
				],
				[
					16.10054188434583,
					23.61412809704052
				],
				[
					16.10054188434583,
					25.760867014953305
				],
				[
					15.027172425389608,
					26.83423647390964
				],
				[
					11.80706404852026,
					31.12771430973521
				],
				[
					7.513586212694918,
					33.27445322764811
				],
				[
					0,
					36.49456160451723
				],
				[
					-5.366847294781792,
					39.71466998138635
				],
				[
					-16.10054188434583,
					44.00814781721192
				],
				[
					-21.467389179127622,
					48.30162565303749
				],
				[
					-26.83423647390964,
					51.52173402990661
				],
				[
					-26.83423647390964,
					51.52173402990661
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 102,
			"versionNonce": 1873895367,
			"isDeleted": false,
			"id": "6Wlb3eza",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -428.58059931232475,
			"y": -689.0903781552054,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 77.01992797851562,
			"height": 25,
			"seed": 880344241,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "client id",
			"rawText": "client id",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "client id",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "text",
			"version": 46,
			"versionNonce": 644523049,
			"isDeleted": false,
			"id": "Na6HjBbC",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 410.7943175915723,
			"y": -664.4028805992084,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 95.37989807128906,
			"height": 25,
			"seed": 1321233343,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Session id",
			"rawText": "Session id",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Session id",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 46,
			"versionNonce": 1176489703,
			"isDeleted": false,
			"id": "ZXqhmSsYFVzDdW25XPjW7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -144.13769268888143,
			"y": -547.4056095729619,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 44.008147817212034,
			"height": 2.146738917912785,
			"seed": 1633035281,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					4.29347783582557,
					-1.0733694589563356
				],
				[
					18.24728080225873,
					-1.0733694589563356
				],
				[
					28.98097539182254,
					-1.0733694589563356
				],
				[
					35.421192145560894,
					-1.0733694589563356
				],
				[
					40.788039440342914,
					-2.146738917912785
				],
				[
					41.86140889929925,
					-2.146738917912785
				],
				[
					42.9347783582557,
					-2.146738917912785
				],
				[
					44.008147817212034,
					-2.146738917912785
				],
				[
					44.008147817212034,
					-2.146738917912785
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 56,
			"versionNonce": 129382153,
			"isDeleted": false,
			"id": "ZhAQMmqLVIMD5lmq7N-yz",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -78.66215569254155,
			"y": -549.5523484908747,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 27.90760593286609,
			"height": 1.0733694589564493,
			"seed": 319090865,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.146738917912785,
					0
				],
				[
					6.440216753738355,
					0
				],
				[
					8.586955671651026,
					0
				],
				[
					11.80706404852026,
					0
				],
				[
					12.880433507476596,
					0
				],
				[
					13.953802966433045,
					0
				],
				[
					15.02717242538938,
					0
				],
				[
					16.10054188434583,
					-1.0733694589564493
				],
				[
					17.173911343302166,
					-1.0733694589564493
				],
				[
					18.247280802258615,
					-1.0733694589564493
				],
				[
					19.32065026121495,
					-1.0733694589564493
				],
				[
					20.3940197201714,
					-1.0733694589564493
				],
				[
					21.467389179127736,
					-1.0733694589564493
				],
				[
					22.540758638084185,
					-1.0733694589564493
				],
				[
					23.61412809704052,
					-1.0733694589564493
				],
				[
					25.760867014953305,
					-1.0733694589564493
				],
				[
					26.834236473909755,
					0
				],
				[
					27.90760593286609,
					0
				],
				[
					27.90760593286609,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 57,
			"versionNonce": 523459079,
			"isDeleted": false,
			"id": "jp15E7w_VJ4RfVhCgKsIE",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -23.9203132857657,
			"y": -555.992565244613,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 39.714669981386464,
			"height": 1.0733694589563356,
			"seed": 594845713,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299015,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.0733694589564493,
					0
				],
				[
					2.146738917912785,
					0
				],
				[
					3.2201083768692342,
					0
				],
				[
					4.29347783582557,
					0
				],
				[
					5.3668472947819055,
					0
				],
				[
					11.80706404852026,
					1.0733694589563356
				],
				[
					12.88043350747671,
					1.0733694589563356
				],
				[
					21.46738917912785,
					1.0733694589563356
				],
				[
					24.68749755599697,
					1.0733694589563356
				],
				[
					26.834236473909755,
					1.0733694589563356
				],
				[
					27.907605932866204,
					1.0733694589563356
				],
				[
					28.98097539182254,
					1.0733694589563356
				],
				[
					31.127714309735325,
					1.0733694589563356
				],
				[
					32.20108376869166,
					1.0733694589563356
				],
				[
					33.27445322764811,
					1.0733694589563356
				],
				[
					34.347822686604445,
					1.0733694589563356
				],
				[
					36.49456160451723,
					1.0733694589563356
				],
				[
					38.641300522430015,
					1.0733694589563356
				],
				[
					39.714669981386464,
					1.0733694589563356
				],
				[
					39.714669981386464,
					1.0733694589563356
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 54,
			"versionNonce": 600600041,
			"isDeleted": false,
			"id": "UXx0BgrFz_BKscxoMwsK2",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 52.28891830013799,
			"y": -546.3322401140056,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 50.44836457095039,
			"height": 5.3668472947819055,
			"seed": 1299864913,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.146738917912785,
					0
				],
				[
					7.51358621269469,
					0
				],
				[
					13.953802966433045,
					-1.0733694589563356
				],
				[
					25.76086701495342,
					-3.2201083768691205
				],
				[
					33.27445322764811,
					-4.29347783582557
				],
				[
					37.56793106347368,
					-4.29347783582557
				],
				[
					41.86140889929925,
					-5.3668472947819055
				],
				[
					42.934778358255585,
					-5.3668472947819055
				],
				[
					44.008147817212034,
					-5.3668472947819055
				],
				[
					45.08151727616837,
					-5.3668472947819055
				],
				[
					46.15488673512482,
					-5.3668472947819055
				],
				[
					47.228256194081155,
					-5.3668472947819055
				],
				[
					48.301625653037604,
					-5.3668472947819055
				],
				[
					49.37499511199394,
					-5.3668472947819055
				],
				[
					50.44836457095039,
					-5.3668472947819055
				],
				[
					50.44836457095039,
					-4.29347783582557
				],
				[
					50.44836457095039,
					-4.29347783582557
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 162,
			"versionNonce": 535331111,
			"isDeleted": false,
			"id": "MF9Kr5gvr0QUiq6hOQKgP",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 590.0470172372895,
			"y": -889.8104669800504,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 74.06249266799091,
			"height": 343.4782268660448,
			"seed": 1557246193,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					8.58695567165114,
					1.0733694589563356
				],
				[
					11.80706404852026,
					1.0733694589563356
				],
				[
					20.3940197201714,
					5.3668472947819055
				],
				[
					24.68749755599697,
					7.51358621269469
				],
				[
					25.76086701495319,
					7.51358621269469
				],
				[
					25.76086701495319,
					10.733694589563925
				],
				[
					24.68749755599697,
					12.880433507476596
				],
				[
					24.68749755599697,
					15.027172425389494
				],
				[
					22.54075863808407,
					18.247280802258615
				],
				[
					20.3940197201714,
					21.467389179127736
				],
				[
					19.32065026121495,
					25.760867014953305
				],
				[
					18.2472808022585,
					27.907605932866204
				],
				[
					17.173911343302052,
					32.201083768691774
				],
				[
					17.173911343302052,
					36.494561604517344
				],
				[
					17.173911343302052,
					38.641300522430015
				],
				[
					17.173911343302052,
					42.934778358255585
				],
				[
					16.10054188434583,
					46.154886735124705
				],
				[
					15.02717242538938,
					49.37499511199394
				],
				[
					15.02717242538938,
					53.66847294781951
				],
				[
					15.02717242538938,
					56.888581324688744
				],
				[
					15.02717242538938,
					61.182059160514314
				],
				[
					15.02717242538938,
					63.328798078426985
				],
				[
					15.02717242538938,
					67.62227591425255
				],
				[
					15.02717242538938,
					71.91575375007812
				],
				[
					15.02717242538938,
					75.13586212694725
				],
				[
					15.02717242538938,
					78.35597050381648
				],
				[
					15.02717242538938,
					84.79618725755483
				],
				[
					15.02717242538938,
					90.16303455233674
				],
				[
					15.02717242538938,
					94.45651238816231
				],
				[
					15.02717242538938,
					97.67662076503154
				],
				[
					15.02717242538938,
					101.97009860085711
				],
				[
					15.02717242538938,
					105.19020697772623
				],
				[
					16.10054188434583,
					109.4836848135518
				],
				[
					16.10054188434583,
					114.85053210833382
				],
				[
					17.173911343302052,
					116.9972710262465
				],
				[
					18.2472808022585,
					121.29074886207206
				],
				[
					18.2472808022585,
					122.36411832102851
				],
				[
					20.3940197201714,
					126.65759615685408
				],
				[
					22.54075863808407,
					129.8777045337232
				],
				[
					24.68749755599697,
					132.024443451636
				],
				[
					30.05434485077876,
					135.24455182850522
				],
				[
					33.27445322764811,
					137.3912907464179
				],
				[
					38.6413005224299,
					138.46466020537434
				],
				[
					42.93477835825547,
					139.5380296643308
				],
				[
					48.30162565303749,
					141.68476858224346
				],
				[
					53.66847294781951,
					142.7581380411999
				],
				[
					56.88858132468863,
					143.83150750015625
				],
				[
					59.0353202426013,
					144.90487695911258
				],
				[
					60.10868970155775,
					144.90487695911258
				],
				[
					52.59510348886306,
					144.90487695911258
				],
				[
					46.15488673512459,
					145.97824641806903
				],
				[
					39.71466998138635,
					149.19835479493815
				],
				[
					33.27445322764811,
					152.4184631718074
				],
				[
					30.05434485077876,
					154.56520208972017
				],
				[
					27.90760593286609,
					156.71194100763296
				],
				[
					26.83423647390964,
					158.85867992554574
				],
				[
					26.83423647390964,
					159.9320493845022
				],
				[
					26.83423647390964,
					163.1521577613713
				],
				[
					27.90760593286609,
					165.2988966792841
				],
				[
					28.98097539182254,
					167.44563559719688
				],
				[
					30.05434485077876,
					171.73911343302245
				],
				[
					31.12771430973521,
					174.95922180989157
				],
				[
					32.20108376869166,
					178.1793301867607
				],
				[
					32.20108376869166,
					181.39943856362993
				],
				[
					33.27445322764811,
					187.83965531736828
				],
				[
					34.34782268660433,
					192.13313315319385
				],
				[
					34.34782268660433,
					198.5733499069321
				],
				[
					34.34782268660433,
					209.30704449649613
				],
				[
					34.34782268660433,
					216.82063070919082
				],
				[
					34.34782268660433,
					225.40758638084196
				],
				[
					34.34782268660433,
					237.21465042936222
				],
				[
					34.34782268660433,
					243.65486718310058
				],
				[
					35.42119214556078,
					250.09508393683893
				],
				[
					36.49456160451723,
					256.5353006905772
				],
				[
					36.49456160451723,
					261.9021479853592
				],
				[
					36.49456160451723,
					266.19562582118476
				],
				[
					36.49456160451723,
					271.56247311596667
				],
				[
					36.49456160451723,
					276.9293204107487
				],
				[
					38.6413005224299,
					285.5162760823997
				],
				[
					38.6413005224299,
					290.88312337718173
				],
				[
					38.6413005224299,
					293.0298622950945
				],
				[
					38.6413005224299,
					297.3233401309201
				],
				[
					38.6413005224299,
					300.5434485077892
				],
				[
					38.6413005224299,
					302.690187425702
				],
				[
					37.56793106347368,
					304.8369263436148
				],
				[
					37.56793106347368,
					308.057034720484
				],
				[
					37.56793106347368,
					310.2037736383967
				],
				[
					37.56793106347368,
					311.27714309735313
				],
				[
					37.56793106347368,
					313.4238820152659
				],
				[
					37.56793106347368,
					315.5706209331787
				],
				[
					37.56793106347368,
					317.7173598510915
				],
				[
					37.56793106347368,
					320.9374682279606
				],
				[
					37.56793106347368,
					323.0842071458734
				],
				[
					37.56793106347368,
					325.2309460637862
				],
				[
					37.56793106347368,
					326.3043155227426
				],
				[
					36.49456160451723,
					327.37768498169896
				],
				[
					36.49456160451723,
					328.4510544406554
				],
				[
					36.49456160451723,
					329.52442389961175
				],
				[
					35.42119214556078,
					329.52442389961175
				],
				[
					35.42119214556078,
					330.5977933585682
				],
				[
					33.27445322764811,
					332.744532276481
				],
				[
					32.20108376869166,
					333.8179017354373
				],
				[
					30.05434485077876,
					335.9646406533501
				],
				[
					27.90760593286609,
					337.03801011230644
				],
				[
					26.83423647390964,
					338.1113795712629
				],
				[
					25.76086701495319,
					339.1847490302192
				],
				[
					24.68749755599697,
					340.2581184891757
				],
				[
					23.61412809704052,
					340.2581184891757
				],
				[
					22.54075863808407,
					340.2581184891757
				],
				[
					20.3940197201714,
					340.2581184891757
				],
				[
					17.173911343302052,
					341.331487948132
				],
				[
					15.02717242538938,
					342.40485740708846
				],
				[
					11.80706404852026,
					342.40485740708846
				],
				[
					9.660325130607362,
					342.40485740708846
				],
				[
					6.440216753738241,
					342.40485740708846
				],
				[
					4.29347783582557,
					342.40485740708846
				],
				[
					0,
					342.40485740708846
				],
				[
					-2.1467389179128986,
					342.40485740708846
				],
				[
					-6.4402167537384685,
					342.40485740708846
				],
				[
					-9.660325130607589,
					342.40485740708846
				],
				[
					-10.733694589564038,
					342.40485740708846
				],
				[
					-12.88043350747671,
					342.40485740708846
				],
				[
					-13.953802966433159,
					342.40485740708846
				],
				[
					-13.953802966433159,
					343.4782268660448
				],
				[
					-13.953802966433159,
					343.4782268660448
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 90,
			"versionNonce": 297322697,
			"isDeleted": false,
			"id": "kDiWDYw7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 695.2372242150157,
			"y": -753.4925456925888,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 357.7599792480469,
			"height": 25,
			"seed": 1293101841,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "这些是固定下来的SD 报文的特殊的地方",
			"rawText": "这些是固定下来的SD 报文的特殊的地方",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "这些是固定下来的SD 报文的特殊的地方",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 50,
			"versionNonce": 430687303,
			"isDeleted": false,
			"id": "ytWf-dRB811SMdgd7YRvH",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -142.88708481358628,
			"y": -455.56792662001436,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 52.90714786159356,
			"height": 0,
			"seed": 842114943,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.2024351786725447,
					0
				],
				[
					7.2146110720354955,
					0
				],
				[
					16.834092501416194,
					0
				],
				[
					25.251138752124234,
					0
				],
				[
					32.46574982415973,
					0
				],
				[
					36.07305536017748,
					0
				],
				[
					38.47792571752268,
					0
				],
				[
					40.88279607486777,
					0
				],
				[
					43.28766643221297,
					0
				],
				[
					46.89497196823072,
					0
				],
				[
					49.29984232557581,
					0
				],
				[
					51.70471268292101,
					0
				],
				[
					52.90714786159356,
					0
				],
				[
					52.90714786159356,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 37,
			"versionNonce": 2065090473,
			"isDeleted": false,
			"id": "Y2WAY1EPrGTcXugjhuCTU",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -291.9890469689865,
			"y": -480.8190653721386,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 431180159,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 88,
			"versionNonce": 2086249319,
			"isDeleted": false,
			"id": "FwrKIddm",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -266.73790821686225,
			"y": -488.03367644417415,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 40.0999755859375,
			"height": 25,
			"seed": 1890967167,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Flag",
			"rawText": "Flag",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Flag",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 56,
			"versionNonce": 1242688137,
			"isDeleted": false,
			"id": "ZbMIntd7ZfEsrDvOuSmYK",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -156.11387177898467,
			"y": -472.40201912143056,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 52.907147861593614,
			"height": 6.012175893362894,
			"seed": 911409599,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-1.2024351786726015,
					0
				],
				[
					-3.6073055360177477,
					-1.2024351786725447
				],
				[
					-6.012175893362951,
					-1.2024351786725447
				],
				[
					-10.821916608053243,
					-2.404870357345146
				],
				[
					-14.429222144070991,
					-2.404870357345146
				],
				[
					-18.03652768008874,
					-2.404870357345146
				],
				[
					-22.846268394779088,
					-2.404870357345146
				],
				[
					-25.251138752124234,
					-2.404870357345146
				],
				[
					-28.858444288141982,
					-2.404870357345146
				],
				[
					-31.263314645487185,
					-2.404870357345146
				],
				[
					-33.66818500283233,
					-2.404870357345146
				],
				[
					-36.07305536017748,
					-1.2024351786725447
				],
				[
					-38.47792571752262,
					-1.2024351786725447
				],
				[
					-39.680360896195225,
					0
				],
				[
					-42.08523125354037,
					0
				],
				[
					-45.69253678955812,
					0
				],
				[
					-48.09740714690332,
					1.2024351786726015
				],
				[
					-49.29984232557587,
					1.2024351786726015
				],
				[
					-51.70471268292107,
					2.404870357345203
				],
				[
					-52.907147861593614,
					3.6073055360177477
				],
				[
					-52.907147861593614,
					3.6073055360177477
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 54,
			"versionNonce": 138321543,
			"isDeleted": false,
			"id": "OwhFfQQqVguHGjdcQDqf_",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -198.19910303252504,
			"y": -489.2361116228467,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 16.834092501416137,
			"height": 40.88279607486783,
			"seed": 1243127967,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-2.404870357345203,
					1.2024351786726015
				],
				[
					-3.6073055360177477,
					4.809740714690349
				],
				[
					-7.2146110720354955,
					8.417046250708097
				],
				[
					-9.619481429380699,
					12.024351786725845
				],
				[
					-12.024351786725845,
					15.631657322743592
				],
				[
					-12.024351786725845,
					18.03652768008874
				],
				[
					-14.429222144070991,
					19.23896285876134
				],
				[
					-14.429222144070991,
					21.643833216106486
				],
				[
					-14.429222144070991,
					22.846268394779088
				],
				[
					-14.429222144070991,
					26.453573930796836
				],
				[
					-13.226786965398446,
					30.060879466814583
				],
				[
					-10.821916608053243,
					32.46574982415973
				],
				[
					-8.417046250708097,
					36.07305536017748
				],
				[
					-3.6073055360177477,
					37.27549053885008
				],
				[
					-1.2024351786726015,
					38.47792571752262
				],
				[
					-1.2024351786726015,
					39.680360896195225
				],
				[
					0,
					39.680360896195225
				],
				[
					2.404870357345146,
					40.88279607486783
				],
				[
					2.404870357345146,
					40.88279607486783
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 36,
			"versionNonce": 392540521,
			"isDeleted": false,
			"id": "bSjVEl0au2ujmaigQpyao",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 770.9636509775762,
			"y": -378.61207518496917,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 1331920703,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 420,
			"versionNonce": 1075262887,
			"isDeleted": false,
			"id": "lU7hmAUGU-k97RNUOMLU7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -486.78354591394486,
			"y": -427.911917510545,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 4235.52507069308,
			"height": 2.6213397889941894,
			"seed": 451169073,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					-3.6073055360177477
				],
				[
					12.630790469263664,
					-3.6073055360177477
				],
				[
					113.67711422337297,
					-3.6073055360177477
				],
				[
					218.93370146723686,
					-3.6073055360177477
				],
				[
					332.6108156906096,
					-3.6073055360177477
				],
				[
					454.70845689349164,
					-3.6073055360177477
				],
				[
					559.9650441373556,
					-3.6073055360177477
				],
				[
					703.1140027890102,
					-3.6073055360177477
				],
				[
					749.4269011763105,
					-3.6073055360177477
				],
				[
					867.3142788894379,
					-3.6073055360177477
				],
				[
					938.888758215265,
					-3.6073055360177477
				],
				[
					1018.8837645206019,
					-3.6073055360177477
				],
				[
					1090.458243846429,
					-3.6073055360177477
				],
				[
					1170.4532501517658,
					-3.6073055360177477
				],
				[
					1237.8174659878387,
					-3.6073055360177477
				],
				[
					1322.0227357829297,
					-3.6073055360177477
				],
				[
					1376.7561611497385,
					-3.6073055360177477
				],
				[
					1423.0690595370388,
					-3.6073055360177477
				],
				[
					1477.8024849038477,
					-2.7335256063530458
				],
				[
					1528.3256467809024,
					-2.7335256063530458
				],
				[
					1587.2693356374662,
					-2.7335256063530458
				],
				[
					1637.7924975145208,
					-2.7335256063530458
				],
				[
					1700.9464498608393,
					-2.7335256063530458
				],
				[
					1797.7825101251942,
					-2.7335256063530458
				],
				[
					1869.3569894510213,
					-2.7335256063530458
				],
				[
					1953.5622592461127,
					-2.7335256063530458
				],
				[
					2020.926475082185,
					-2.7335256063530458
				],
				[
					2088.2906909182584,
					-2.7335256063530458
				],
				[
					2176.706224203104,
					-2.7335256063530458
				],
				[
					2235.649913059667,
					-2.7335256063530458
				],
				[
					2290.3833384264767,
					-2.7335256063530458
				],
				[
					2370.378344731813,
					-2.7335256063530458
				],
				[
					2441.9528240576406,
					-1.8597456766882605
				],
				[
					2521.947830362977,
					-1.8597456766882605
				],
				[
					2622.994154117086,
					-1.8597456766882605
				],
				[
					2707.1994239121777,
					-1.8597456766882605
				],
				[
					2791.4046937072685,
					-1.8597456766882605
				],
				[
					2926.1331253794137,
					-1.8597456766882605
				],
				[
					3010.338395174506,
					-1.8597456766882605
				],
				[
					3102.964191949105,
					-1.8597456766882605
				],
				[
					3199.8002522134607,
					-1.8597456766882605
				],
				[
					3284.0055220085515,
					-1.8597456766882605
				],
				[
					3351.3697378446245,
					-1.8597456766882605
				],
				[
					3410.313426701188,
					-1.8597456766882605
				],
				[
					3469.2571155577516,
					-1.8597456766882605
				],
				[
					3494.5186964962786,
					-1.8597456766882605
				],
				[
					3523.990540924561,
					-1.8597456766882605
				],
				[
					3553.4623853528433,
					-1.8597456766882605
				],
				[
					3574.513702801615,
					-1.8597456766882605
				],
				[
					3603.9855472298977,
					-1.8597456766882605
				],
				[
					3633.457391658179,
					-1.8597456766882605
				],
				[
					3650.2984456171976,
					-1.8597456766882605
				],
				[
					3667.1394995762157,
					-1.8597456766882605
				],
				[
					3683.9805535352334,
					-1.8597456766882605
				],
				[
					3692.401080514743,
					-1.8597456766882605
				],
				[
					3700.8216074942516,
					-1.8597456766882605
				],
				[
					3709.242134473761,
					-1.8597456766882605
				],
				[
					3713.4523979635155,
					-1.8597456766882605
				],
				[
					3717.6626614532706,
					-1.8597456766882605
				],
				[
					3721.872924943025,
					-1.8597456766882605
				],
				[
					3738.713978902043,
					-1.8597456766882605
				],
				[
					3742.924242391798,
					-1.8597456766882605
				],
				[
					3747.134505881552,
					-1.8597456766882605
				],
				[
					3747.134505881552,
					-0.9859657470235584
				],
				[
					3751.344769371307,
					-0.9859657470235584
				],
				[
					3763.9755598405704,
					-0.9859657470235584
				],
				[
					3780.8166137995886,
					-0.9859657470235584
				],
				[
					3785.0268772893432,
					-0.9859657470235584
				],
				[
					3827.129512186889,
					-1.8597456766882605
				],
				[
					3852.391093125416,
					-2.7335256063530458
				],
				[
					3881.8629375536975,
					-2.7335256063530458
				],
				[
					3902.9142550024703,
					-2.7335256063530458
				],
				[
					3945.016889900016,
					-2.7335256063530458
				],
				[
					3970.278470838543,
					-2.7335256063530458
				],
				[
					3991.329788287316,
					-2.7335256063530458
				],
				[
					3999.7503152668255,
					-2.7335256063530458
				],
				[
					4003.9605787565797,
					-2.7335256063530458
				],
				[
					4012.3811057360886,
					-2.7335256063530458
				],
				[
					4016.5913692258437,
					-2.7335256063530458
				],
				[
					4020.8016327155974,
					-2.7335256063530458
				],
				[
					4033.432423184861,
					-2.7335256063530458
				],
				[
					4050.2734771438795,
					-2.7335256063530458
				],
				[
					4058.6940041233884,
					-2.7335256063530458
				],
				[
					4067.114531102898,
					-2.7335256063530458
				],
				[
					4071.3247945926523,
					-2.7335256063530458
				],
				[
					4083.9555850619163,
					-2.7335256063530458
				],
				[
					4096.586375531179,
					-2.7335256063530458
				],
				[
					4117.637692979953,
					-2.7335256063530458
				],
				[
					4134.478746938971,
					-2.7335256063530458
				],
				[
					4155.530064387744,
					-2.7335256063530458
				],
				[
					4168.1608548570075,
					-2.7335256063530458
				],
				[
					4185.001908816025,
					-1.8597456766882605
				],
				[
					4201.842962775044,
					-1.8597456766882605
				],
				[
					4210.263489754552,
					-1.8597456766882605
				],
				[
					4218.684016734062,
					-1.8597456766882605
				],
				[
					4227.104543713571,
					-1.8597456766882605
				],
				[
					4235.52507069308,
					-0.9859657470235584
				],
				[
					4235.52507069308,
					-0.9859657470235584
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 57,
			"versionNonce": 1482529865,
			"isDeleted": false,
			"id": "H8QzLWqPNh0ewMhN9C_iE",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 147.42832835344848,
			"y": -389.77159359062915,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 182.47280802258638,
			"height": 4.29347783582557,
			"seed": 650250769,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					4.29347783582557,
					0
				],
				[
					12.88043350747671,
					0
				],
				[
					22.540758638084185,
					1.0733694589563925
				],
				[
					34.34782268660456,
					1.0733694589563925
				],
				[
					54.74184240677596,
					1.0733694589563925
				],
				[
					71.91575375007824,
					2.146738917912785
				],
				[
					85.86955671651128,
					2.146738917912785
				],
				[
					101.97009860085711,
					3.2201083768691774
				],
				[
					113.77716264937737,
					4.29347783582557
				],
				[
					122.36411832102851,
					4.29347783582557
				],
				[
					128.80433507476687,
					4.29347783582557
				],
				[
					132.024443451636,
					4.29347783582557
				],
				[
					133.09781291059244,
					4.29347783582557
				],
				[
					136.31792128746156,
					3.2201083768691774
				],
				[
					138.46466020537434,
					3.2201083768691774
				],
				[
					142.7581380411999,
					3.2201083768691774
				],
				[
					149.19835479493827,
					3.2201083768691774
				],
				[
					155.63857154867662,
					3.2201083768691774
				],
				[
					165.2988966792841,
					3.2201083768691774
				],
				[
					170.66574397406612,
					3.2201083768691774
				],
				[
					176.03259126884802,
					3.2201083768691774
				],
				[
					179.25269964571714,
					3.2201083768691774
				],
				[
					182.47280802258638,
					3.2201083768691774
				],
				[
					182.47280802258638,
					3.2201083768691774
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 47,
			"versionNonce": 454027463,
			"isDeleted": false,
			"id": "qwa5uhCUunb1zBjbmfklQ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 325.6076585402093,
			"y": -400.505288180193,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 16.10054188434583,
			"height": 33.27445322764805,
			"seed": 610899665,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.146738917912785,
					3.2201083768691205
				],
				[
					5.3668472947819055,
					5.3668472947819055
				],
				[
					8.58695567165114,
					8.586955671651083
				],
				[
					11.80706404852026,
					10.733694589563868
				],
				[
					15.027172425389494,
					12.880433507476653
				],
				[
					16.10054188434583,
					12.880433507476653
				],
				[
					16.10054188434583,
					13.953802966433045
				],
				[
					15.027172425389494,
					16.10054188434583
				],
				[
					13.953802966433045,
					20.3940197201714
				],
				[
					10.733694589563925,
					24.68749755599697
				],
				[
					5.3668472947819055,
					30.054344850778875
				],
				[
					2.146738917912785,
					33.27445322764805
				],
				[
					0,
					33.27445322764805
				],
				[
					0,
					33.27445322764805
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 179,
			"versionNonce": 1289038633,
			"isDeleted": false,
			"id": "DZjpwuP2",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 380.34950094698513,
			"y": -406.9455049339314,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 685.3997802734375,
			"height": 25,
			"seed": 1736004817,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Entries的长度，此时为16字节   一个entry为 16字节   所以只有一个eentry",
			"rawText": "Entries的长度，此时为16字节   一个entry为 16字节   所以只有一个eentry",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Entries的长度，此时为16字节   一个entry为 16字节   所以只有一个eentry",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 141,
			"versionNonce": 1992636391,
			"isDeleted": false,
			"id": "yQs1vNa3rxiVxYuxUZQnI",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 139.9147421407538,
			"y": -311.4156230868127,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 37.56793106347368,
			"height": 317.71735985109143,
			"seed": 447174417,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.146738917912785,
					0
				],
				[
					4.29347783582557,
					0
				],
				[
					5.3668472947819055,
					1.0733694589563925
				],
				[
					6.440216753738355,
					1.0733694589563925
				],
				[
					8.58695567165114,
					1.0733694589563925
				],
				[
					9.660325130607475,
					1.0733694589563925
				],
				[
					11.80706404852026,
					1.0733694589563925
				],
				[
					13.953802966433045,
					1.0733694589563925
				],
				[
					15.027172425389494,
					1.0733694589563925
				],
				[
					16.10054188434583,
					1.0733694589563925
				],
				[
					18.247280802258615,
					1.0733694589563925
				],
				[
					19.320650261215064,
					1.0733694589563925
				],
				[
					19.320650261215064,
					3.2201083768691774
				],
				[
					19.320650261215064,
					6.440216753738355
				],
				[
					18.247280802258615,
					8.58695567165114
				],
				[
					17.17391134330228,
					12.88043350747671
				],
				[
					16.10054188434583,
					16.100541884345887
				],
				[
					15.027172425389494,
					19.320650261215008
				],
				[
					15.027172425389494,
					22.540758638084185
				],
				[
					15.027172425389494,
					26.834236473909755
				],
				[
					15.027172425389494,
					30.054344850778932
				],
				[
					15.027172425389494,
					34.3478226866045
				],
				[
					15.027172425389494,
					37.56793106347362
				],
				[
					15.027172425389494,
					41.86140889929919
				],
				[
					15.027172425389494,
					46.15488673512476
				],
				[
					15.027172425389494,
					50.44836457095033
				],
				[
					15.027172425389494,
					54.7418424067759
				],
				[
					15.027172425389494,
					62.25542861947059
				],
				[
					15.027172425389494,
					67.62227591425261
				],
				[
					16.10054188434583,
					71.91575375007818
				],
				[
					16.10054188434583,
					77.28260104486009
				],
				[
					18.247280802258615,
					81.57607888068566
				],
				[
					18.247280802258615,
					85.86955671651123
				],
				[
					18.247280802258615,
					92.30977347024958
				],
				[
					18.247280802258615,
					97.67662076503149
				],
				[
					19.320650261215064,
					100.89672914190072
				],
				[
					19.320650261215064,
					105.19020697772629
				],
				[
					20.3940197201714,
					109.48368481355175
				],
				[
					21.46738917912785,
					112.70379319042098
				],
				[
					22.540758638084185,
					115.9239015672901
				],
				[
					22.540758638084185,
					119.14400994415934
				],
				[
					22.540758638084185,
					122.36411832102846
				],
				[
					22.540758638084185,
					126.65759615685403
				],
				[
					22.540758638084185,
					129.87770453372326
				],
				[
					23.614128097040634,
					133.09781291059238
				],
				[
					24.68749755599697,
					137.39129074641795
				],
				[
					24.68749755599697,
					140.61139912328707
				],
				[
					26.834236473909755,
					144.90487695911264
				],
				[
					28.98097539182254,
					148.12498533598188
				],
				[
					28.98097539182254,
					151.345093712851
				],
				[
					31.127714309735325,
					154.56520208972023
				],
				[
					33.27445322764811,
					155.63857154867657
				],
				[
					35.421192145560894,
					157.78531046658935
				],
				[
					36.49456160451723,
					158.8586799255458
				],
				[
					37.56793106347368,
					158.8586799255458
				],
				[
					37.56793106347368,
					161.00541884345847
				],
				[
					37.56793106347368,
					162.07878830241492
				],
				[
					37.56793106347368,
					165.29889667928404
				],
				[
					37.56793106347368,
					167.44563559719683
				],
				[
					35.421192145560894,
					171.7391134330224
				],
				[
					34.347822686604445,
					174.95922180989163
				],
				[
					33.27445322764811,
					178.17933018676075
				],
				[
					33.27445322764811,
					181.39943856362999
				],
				[
					33.27445322764811,
					184.6195469404991
				],
				[
					33.27445322764811,
					189.986394235281
				],
				[
					33.27445322764811,
					193.20650261215025
				],
				[
					33.27445322764811,
					196.42661098901937
				],
				[
					33.27445322764811,
					201.79345828380139
				],
				[
					33.27445322764811,
					203.94019720171417
				],
				[
					33.27445322764811,
					209.30704449649608
				],
				[
					33.27445322764811,
					213.60052233232165
				],
				[
					33.27445322764811,
					217.89400016814722
				],
				[
					33.27445322764811,
					223.26084746292912
				],
				[
					33.27445322764811,
					230.77443367562392
				],
				[
					33.27445322764811,
					236.14128097040583
				],
				[
					33.27445322764811,
					240.4347588062314
				],
				[
					33.27445322764811,
					243.65486718310052
				],
				[
					33.27445322764811,
					246.87497555996976
				],
				[
					33.27445322764811,
					250.09508393683888
				],
				[
					33.27445322764811,
					254.38856177266445
				],
				[
					34.347822686604445,
					257.6086701495337
				],
				[
					34.347822686604445,
					260.8287785264028
				],
				[
					34.347822686604445,
					264.0488869032719
				],
				[
					34.347822686604445,
					266.1956258211847
				],
				[
					34.347822686604445,
					270.4891036570103
				],
				[
					34.347822686604445,
					273.7092120338795
				],
				[
					34.347822686604445,
					279.0760593286614
				],
				[
					34.347822686604445,
					282.29616770553065
				],
				[
					34.347822686604445,
					285.51627608239977
				],
				[
					34.347822686604445,
					288.736384459269
				],
				[
					34.347822686604445,
					294.1032317540509
				],
				[
					34.347822686604445,
					296.2499706719637
				],
				[
					33.27445322764811,
					299.4700790488328
				],
				[
					32.20108376869166,
					302.69018742570205
				],
				[
					32.20108376869166,
					305.91029580257117
				],
				[
					32.20108376869166,
					308.05703472048395
				],
				[
					32.20108376869166,
					310.20377363839674
				],
				[
					31.127714309735325,
					310.20377363839674
				],
				[
					31.127714309735325,
					311.2771430973532
				],
				[
					30.054344850778875,
					311.2771430973532
				],
				[
					30.054344850778875,
					312.3505125563095
				],
				[
					28.98097539182254,
					312.3505125563095
				],
				[
					27.907605932866204,
					314.4972514742223
				],
				[
					25.76086701495342,
					315.57062093317865
				],
				[
					24.68749755599697,
					316.6439903921351
				],
				[
					23.614128097040634,
					317.71735985109143
				],
				[
					28.98097539182254,
					316.6439903921351
				],
				[
					28.98097539182254,
					316.6439903921351
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 39,
			"versionNonce": 758636041,
			"isDeleted": false,
			"id": "fWeG4W7Y",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 216.12397372665748,
			"y": -168.65748504561276,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 64.97994995117188,
			"height": 25,
			"seed": 1370086737,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "entry 1",
			"rawText": "entry 1",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "entry 1",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "text",
			"version": 46,
			"versionNonce": 1229169415,
			"isDeleted": false,
			"id": "ux5yO4iw",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -795.9742823140579,
			"y": -293.2497649549992,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 259.619873046875,
			"height": 25,
			"seed": 1974223615,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Service Entry 用于服务发现",
			"rawText": "Service Entry 用于服务发现",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Service Entry 用于服务发现",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 50,
			"versionNonce": 411120873,
			"isDeleted": false,
			"id": "tAWJ3Hhp_Z2u5OQFQf2Pl",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -146.58575964544184,
			"y": -270.709006316915,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 42.934778358255585,
			"height": 5.366847294781962,
			"seed": 1691741681,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.0733694589563356,
					1.0733694589563925
				],
				[
					3.2201083768691205,
					1.0733694589563925
				],
				[
					6.440216753738241,
					1.0733694589563925
				],
				[
					8.586955671651026,
					1.0733694589563925
				],
				[
					12.880433507476596,
					1.0733694589563925
				],
				[
					20.3940197201714,
					1.0733694589563925
				],
				[
					23.61412809704052,
					0
				],
				[
					27.90760593286609,
					-1.0733694589563925
				],
				[
					32.20108376869166,
					-1.0733694589563925
				],
				[
					34.347822686604445,
					-1.0733694589563925
				],
				[
					35.42119214556078,
					-2.146738917912785
				],
				[
					37.567931063473566,
					-3.2201083768691774
				],
				[
					38.641300522430015,
					-3.2201083768691774
				],
				[
					40.7880394403428,
					-4.29347783582557
				],
				[
					41.861408899299136,
					-4.29347783582557
				],
				[
					42.934778358255585,
					-4.29347783582557
				],
				[
					42.934778358255585,
					-4.29347783582557
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 43,
			"versionNonce": 319269415,
			"isDeleted": false,
			"id": "h4DmpXXn",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -277.5368336381215,
			"y": -308.2769373803887,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 53.49993896484375,
			"height": 25,
			"seed": 1667646865,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Offer",
			"rawText": "Offer",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Offer",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 47,
			"versionNonce": 1111273417,
			"isDeleted": false,
			"id": "hRjpIFsZa5SGAKhUX0Neh",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -158.3928236939622,
			"y": -303.9834595445631,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 36.49456160451723,
			"height": 5.366847294781962,
			"seed": 1703183313,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-1.0733694589563356,
					0
				],
				[
					-2.146738917912785,
					0
				],
				[
					-4.29347783582557,
					0
				],
				[
					-11.80706404852026,
					1.0733694589563925
				],
				[
					-16.10054188434583,
					2.146738917912785
				],
				[
					-20.3940197201714,
					3.2201083768691774
				],
				[
					-22.540758638084185,
					3.2201083768691774
				],
				[
					-25.760867014953305,
					3.2201083768691774
				],
				[
					-28.98097539182254,
					4.29347783582557
				],
				[
					-30.054344850778875,
					4.29347783582557
				],
				[
					-32.20108376869166,
					4.29347783582557
				],
				[
					-35.421192145560894,
					5.366847294781962
				],
				[
					-36.49456160451723,
					5.366847294781962
				],
				[
					-36.49456160451723,
					5.366847294781962
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 50,
			"versionNonce": 285068615,
			"isDeleted": false,
			"id": "g8xCo6LThCvLjC-PSSoJ6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -205.62107988804337,
			"y": -316.8638930520398,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 10.733694589563925,
			"height": 36.49456160451729,
			"seed": 513425873,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-1.0733694589563356,
					0
				],
				[
					-2.146738917912785,
					3.2201083768691774
				],
				[
					-3.2201083768691205,
					8.58695567165114
				],
				[
					-4.29347783582557,
					15.027172425389494
				],
				[
					-5.3668472947819055,
					19.320650261215064
				],
				[
					-5.3668472947819055,
					24.68749755599697
				],
				[
					-5.3668472947819055,
					28.98097539182254
				],
				[
					-5.3668472947819055,
					30.054344850778932
				],
				[
					-5.3668472947819055,
					31.127714309735325
				],
				[
					-5.3668472947819055,
					33.27445322764811
				],
				[
					-3.2201083768691205,
					34.3478226866045
				],
				[
					-2.146738917912785,
					35.421192145560894
				],
				[
					1.0733694589564493,
					36.49456160451729
				],
				[
					3.2201083768692342,
					36.49456160451729
				],
				[
					4.29347783582557,
					36.49456160451729
				],
				[
					5.366847294782019,
					36.49456160451729
				],
				[
					5.366847294782019,
					36.49456160451729
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 82,
			"versionNonce": 1619381929,
			"isDeleted": false,
			"id": "7t4yN9RWP6PTXf58EVQfw",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -146.58575964544184,
			"y": -184.83944960040384,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 108.41031535459535,
			"height": 1.0733694589563925,
			"seed": 987555185,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					3.2201083768691205,
					0
				],
				[
					7.51358621269469,
					0
				],
				[
					11.80706404852026,
					0
				],
				[
					19.32065026121495,
					0
				],
				[
					26.834236473909755,
					0
				],
				[
					32.20108376869166,
					0
				],
				[
					37.567931063473566,
					0
				],
				[
					38.641300522430015,
					0
				],
				[
					39.71466998138635,
					0
				],
				[
					40.7880394403428,
					0
				],
				[
					41.861408899299136,
					0
				],
				[
					42.934778358255585,
					0
				],
				[
					46.154886735124705,
					0
				],
				[
					50.448364570950275,
					-1.0733694589563925
				],
				[
					53.66847294781951,
					-1.0733694589563925
				],
				[
					56.88858132468863,
					-1.0733694589563925
				],
				[
					59.035320242601415,
					-1.0733694589563925
				],
				[
					61.1820591605142,
					-1.0733694589563925
				],
				[
					63.328798078426985,
					-1.0733694589563925
				],
				[
					65.47553699633977,
					-1.0733694589563925
				],
				[
					69.76901483216534,
					-1.0733694589563925
				],
				[
					71.91575375007812,
					-1.0733694589563925
				],
				[
					74.06249266799091,
					-1.0733694589563925
				],
				[
					76.2092315859037,
					-1.0733694589563925
				],
				[
					77.28260104486003,
					-1.0733694589563925
				],
				[
					79.42933996277281,
					-1.0733694589563925
				],
				[
					80.50270942172926,
					-1.0733694589563925
				],
				[
					81.5760788806856,
					-1.0733694589563925
				],
				[
					83.72281779859838,
					-1.0733694589563925
				],
				[
					84.79618725755472,
					-1.0733694589563925
				],
				[
					86.9429261754675,
					-1.0733694589563925
				],
				[
					88.01629563442395,
					-1.0733694589563925
				],
				[
					89.08966509338029,
					-1.0733694589563925
				],
				[
					91.23640401129308,
					-1.0733694589563925
				],
				[
					93.38314292920586,
					-1.0733694589563925
				],
				[
					94.45651238816231,
					-1.0733694589563925
				],
				[
					95.52988184711865,
					-1.0733694589563925
				],
				[
					96.6032513060751,
					-1.0733694589563925
				],
				[
					97.67662076503143,
					-1.0733694589563925
				],
				[
					98.74999022398788,
					-1.0733694589563925
				],
				[
					100.89672914190066,
					-1.0733694589563925
				],
				[
					103.04346805981345,
					-1.0733694589563925
				],
				[
					104.11683751876978,
					-1.0733694589563925
				],
				[
					105.19020697772623,
					-1.0733694589563925
				],
				[
					106.26357643668257,
					-1.0733694589563925
				],
				[
					107.3369458956389,
					-1.0733694589563925
				],
				[
					108.41031535459535,
					-1.0733694589563925
				],
				[
					108.41031535459535,
					0
				],
				[
					108.41031535459535,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 64,
			"versionNonce": 780307559,
			"isDeleted": false,
			"id": "qj3JmXuAorysLSOxBj-fh",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -10.267838357980395,
			"y": -181.61934122353466,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 100.89672914190066,
			"height": 1.0733694589563925,
			"seed": 681699601,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					3.2201083768692342,
					0
				],
				[
					6.440216753738355,
					0
				],
				[
					11.807064048520374,
					0
				],
				[
					18.24728080225873,
					0
				],
				[
					23.614128097040634,
					0
				],
				[
					32.201083768691774,
					0
				],
				[
					34.34782268660456,
					0
				],
				[
					39.714669981386464,
					0
				],
				[
					41.86140889929925,
					0
				],
				[
					46.15488673512482,
					0
				],
				[
					49.37499511199394,
					0
				],
				[
					55.815211865732294,
					-1.0733694589563925
				],
				[
					56.888581324688744,
					-1.0733694589563925
				],
				[
					62.25542861947065,
					-1.0733694589563925
				],
				[
					64.40216753738343,
					-1.0733694589563925
				],
				[
					67.62227591425267,
					-1.0733694589563925
				],
				[
					69.76901483216545,
					-1.0733694589563925
				],
				[
					74.06249266799091,
					-1.0733694589563925
				],
				[
					76.2092315859037,
					-1.0733694589563925
				],
				[
					79.42933996277293,
					-1.0733694589563925
				],
				[
					83.7228177985985,
					-1.0733694589563925
				],
				[
					86.94292617546762,
					-1.0733694589563925
				],
				[
					88.01629563442407,
					-1.0733694589563925
				],
				[
					91.23640401129319,
					-1.0733694589563925
				],
				[
					92.30977347024964,
					-1.0733694589563925
				],
				[
					94.45651238816242,
					-1.0733694589563925
				],
				[
					95.52988184711876,
					-1.0733694589563925
				],
				[
					98.749990223988,
					-1.0733694589563925
				],
				[
					99.82335968294433,
					-1.0733694589563925
				],
				[
					100.89672914190066,
					-1.0733694589563925
				],
				[
					100.89672914190066,
					-1.0733694589563925
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 55,
			"versionNonce": 1510478217,
			"isDeleted": false,
			"id": "xRAeCenZ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -149.80586802231107,
			"y": -176.2524939287527,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 91.97990417480469,
			"height": 25,
			"seed": 295672561,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "service id",
			"rawText": "service id",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "service id",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "text",
			"version": 67,
			"versionNonce": 929195911,
			"isDeleted": false,
			"id": "trmRH1pC",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -9.194468899023946,
			"y": -178.39923284666543,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 105.29991149902344,
			"height": 25,
			"seed": 580665681,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "instance id",
			"rawText": "instance id",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "instance id",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 61,
			"versionNonce": 872347753,
			"isDeleted": false,
			"id": "LWwsV1CVUIlxpuN0aXdCM",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -146.58575964544184,
			"y": 96.38334864617036,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 62.255428619470536,
			"height": 6.440216753738355,
			"seed": 1763089489,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					4.293477835825456,
					0
				],
				[
					7.51358621269469,
					0
				],
				[
					17.173911343302166,
					-2.146738917912785
				],
				[
					21.467389179127736,
					-4.29347783582557
				],
				[
					26.834236473909755,
					-5.3668472947819055
				],
				[
					30.054344850778875,
					-6.440216753738355
				],
				[
					33.274453227647996,
					-6.440216753738355
				],
				[
					35.42119214556078,
					-6.440216753738355
				],
				[
					37.567931063473566,
					-6.440216753738355
				],
				[
					39.71466998138635,
					-6.440216753738355
				],
				[
					40.7880394403428,
					-6.440216753738355
				],
				[
					41.861408899299136,
					-6.440216753738355
				],
				[
					42.934778358255585,
					-6.440216753738355
				],
				[
					44.00814781721192,
					-6.440216753738355
				],
				[
					45.08151727616837,
					-6.440216753738355
				],
				[
					47.228256194081155,
					-6.440216753738355
				],
				[
					48.30162565303749,
					-6.440216753738355
				],
				[
					50.448364570950275,
					-4.29347783582557
				],
				[
					52.59510348886306,
					-4.29347783582557
				],
				[
					53.66847294781951,
					-4.29347783582557
				],
				[
					54.741842406775845,
					-3.2201083768691205
				],
				[
					55.81521186573218,
					-3.2201083768691205
				],
				[
					56.88858132468863,
					-3.2201083768691205
				],
				[
					59.035320242601415,
					-2.146738917912785
				],
				[
					60.10868970155775,
					-2.146738917912785
				],
				[
					62.255428619470536,
					-2.146738917912785
				],
				[
					62.255428619470536,
					-1.0733694589563356
				],
				[
					62.255428619470536,
					-1.0733694589563356
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 1239015079,
			"isDeleted": false,
			"id": "UDOtPUxS",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": -907.1883727957103,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 241.54019165039062,
			"height": 69.32328717653772,
			"seed": 216517681,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "ffff8100",
			"rawText": "ffff8100",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ffff8100",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 1077281609,
			"isDeleted": false,
			"id": "i4bNbpCU",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": -810.1357707485574,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 304.8086242675781,
			"height": 69.32328717653772,
			"seed": 1869548383,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.458629741230176,
			"fontFamily": 1,
			"text": "00000030",
			"rawText": "00000030",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000030",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 144011719,
			"isDeleted": false,
			"id": "F8bhXvc6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": -713.0831687014047,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 285.6783752441406,
			"height": 69.32328717653772,
			"seed": 1264655889,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "00000ee5",
			"rawText": "00000ee5",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000ee5",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 185119273,
			"isDeleted": false,
			"id": "gM8sYbQZ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": -616.030566654252,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 260.28228759765625,
			"height": 69.32328717653772,
			"seed": 1834239871,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "01010200",
			"rawText": "01010200",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "01010200",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 212967655,
			"isDeleted": false,
			"id": "F4GyqJg6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": -518.9779646070991,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 294.883056640625,
			"height": 69.32328717653772,
			"seed": 1989489649,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "c0000000",
			"rawText": "c0000000",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "c0000000",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 157451529,
			"isDeleted": false,
			"id": "iGSw8wJ6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": -421.92536255994634,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 282.0741271972656,
			"height": 69.32328717653772,
			"seed": 1333591967,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "00000010",
			"rawText": "00000010",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000010",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 261,
			"versionNonce": 398126087,
			"isDeleted": false,
			"id": "GjgUqUYA",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2072.6020754340348,
			"y": -324.87276051279355,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 258.95147705078125,
			"height": 69.32328717653769,
			"seed": 848006609,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.458629741230155,
			"fontFamily": 1,
			"text": "01000010",
			"rawText": "01000010",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "01000010",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 113179625,
			"isDeleted": false,
			"id": "PrbuYlI4",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": -227.8201584656407,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 250.68942260742188,
			"height": 69.32328717653772,
			"seed": 941208511,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "90150001",
			"rawText": "90150001",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "90150001",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 95277863,
			"isDeleted": false,
			"id": "Hur7guEd",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": -130.76755641848797,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 280.90966796875,
			"height": 69.32328717653772,
			"seed": 911977393,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "0100000a",
			"rawText": "0100000a",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "0100000a",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 1395234505,
			"isDeleted": false,
			"id": "yJX94yYA",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": -33.714954371335125,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 305.19677734375,
			"height": 69.32328717653772,
			"seed": 793437151,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "00000000",
			"rawText": "00000000",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000000",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 2130105927,
			"isDeleted": false,
			"id": "RLHi0pTZ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": 63.33764767581761,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 294.883056640625,
			"height": 69.32328717653772,
			"seed": 1781337489,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "0000000c",
			"rawText": "0000000c",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "0000000c",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 826135977,
			"isDeleted": false,
			"id": "ZFgCL5pb",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": 160.39024972297045,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 298.15460205078125,
			"height": 69.32328717653772,
			"seed": 1696665599,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "00090400",
			"rawText": "00090400",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00090400",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 1785886055,
			"isDeleted": false,
			"id": "QjtqCsnm",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": 257.4428517701232,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 264.8846130371094,
			"height": 69.32328717653772,
			"seed": 1161245553,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "ac140304",
			"rawText": "ac140304",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ac140304",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 69679241,
			"isDeleted": false,
			"id": "eXCV7mRp",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2068.4496452173603,
			"y": 354.4954538172759,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 235.3297576904297,
			"height": 69.32328717653772,
			"seed": 865908767,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 55.45862974123017,
			"fontFamily": 1,
			"text": "00117727",
			"rawText": "00117727",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00117727",
			"lineHeight": 1.25,
			"baseline": 48
		},
		{
			"type": "freedraw",
			"version": 45,
			"versionNonce": 527249543,
			"isDeleted": false,
			"id": "URhgd8tWCLrzqfXd_0oZw",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2073.9672598486377,
			"y": -265.04712433561417,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 53.284446092598955,
			"height": 6.950145142512838,
			"seed": 736593681,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.3167150475046583,
					0
				],
				[
					16.21700533252988,
					4.6334300950086345
				],
				[
					25.483865522547603,
					4.6334300950086345
				],
				[
					32.43401066506067,
					6.950145142512838
				],
				[
					34.75072571256442,
					6.950145142512838
				],
				[
					39.384155807573734,
					6.950145142512838
				],
				[
					41.70087085507748,
					6.950145142512838
				],
				[
					41.70087085507748,
					4.6334300950086345
				],
				[
					44.01758590258214,
					4.6334300950086345
				],
				[
					48.65101599759055,
					4.6334300950086345
				],
				[
					50.967731045095206,
					4.6334300950086345
				],
				[
					53.284446092598955,
					4.6334300950086345
				],
				[
					53.284446092598955,
					4.6334300950086345
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 61,
			"versionNonce": 1033977705,
			"isDeleted": false,
			"id": "OuYxLqeYvlyXmbMCyyS4D",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2073.9672598486377,
			"y": -158.47823215041626,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 108.88560723270257,
			"height": 2.316715047504431,
			"seed": 819876657,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					4.633430095008407,
					0
				],
				[
					6.950145142513065,
					0
				],
				[
					13.90029028502613,
					0
				],
				[
					16.21700533252988,
					0
				],
				[
					20.850435427539196,
					0
				],
				[
					25.483865522547603,
					0
				],
				[
					32.43401066506067,
					0
				],
				[
					37.067440760069076,
					0
				],
				[
					44.01758590258214,
					0
				],
				[
					46.33430095008589,
					0
				],
				[
					48.65101599759055,
					0
				],
				[
					50.967731045095206,
					0
				],
				[
					53.284446092598955,
					0
				],
				[
					57.91787618760736,
					-2.316715047504431
				],
				[
					62.55130628261668,
					-2.316715047504431
				],
				[
					64.86802133012043,
					-2.316715047504431
				],
				[
					67.18473637762509,
					-2.316715047504431
				],
				[
					76.4515965676419,
					-2.316715047504431
				],
				[
					83.40174171015497,
					-2.316715047504431
				],
				[
					88.03517180516337,
					-2.316715047504431
				],
				[
					90.35188685266803,
					-2.316715047504431
				],
				[
					94.98531694767644,
					-2.316715047504431
				],
				[
					97.3020319951811,
					-2.316715047504431
				],
				[
					99.61874704268484,
					-2.316715047504431
				],
				[
					101.9354620901895,
					-2.316715047504431
				],
				[
					104.25217713769416,
					-2.316715047504431
				],
				[
					106.56889218519791,
					-2.316715047504431
				],
				[
					108.88560723270257,
					-2.316715047504431
				],
				[
					108.88560723270257,
					-2.316715047504431
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 56,
			"versionNonce": 1470334887,
			"isDeleted": false,
			"id": "4KO7FzU58G1RrS28tzq9X",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2210.6534476513916,
			"y": -160.7949471979207,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 139.00290285025767,
			"height": 9.266860190017269,
			"seed": 1605804369,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					4.633430095008407,
					0
				],
				[
					9.266860190016814,
					0
				],
				[
					13.90029028502613,
					0
				],
				[
					18.533720380034538,
					0
				],
				[
					20.850435427538287,
					0
				],
				[
					25.483865522547603,
					0
				],
				[
					37.067440760069076,
					0
				],
				[
					50.9677310450943,
					0
				],
				[
					67.18473637762509,
					2.316715047504431
				],
				[
					92.66860190017178,
					6.950145142512838
				],
				[
					104.25217713769325,
					6.950145142512838
				],
				[
					108.88560723270166,
					9.266860190017269
				],
				[
					111.20232228020632,
					9.266860190017269
				],
				[
					113.51903732771098,
					9.266860190017269
				],
				[
					120.46918247022404,
					9.266860190017269
				],
				[
					122.78589751772779,
					9.266860190017269
				],
				[
					125.10261256523245,
					9.266860190017269
				],
				[
					127.4193276127362,
					9.266860190017269
				],
				[
					127.4193276127362,
					6.950145142512838
				],
				[
					129.73604266024086,
					6.950145142512838
				],
				[
					132.0527577077455,
					6.950145142512838
				],
				[
					136.68618780275392,
					6.950145142512838
				],
				[
					139.00290285025767,
					6.950145142512838
				],
				[
					139.00290285025767,
					6.950145142512838
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 113,
			"versionNonce": 200763977,
			"isDeleted": false,
			"id": "KWRq-EQK24P_Z_wP1dxzP",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2395.990651451735,
			"y": -302.114565095683,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 67.18473637762509,
			"height": 308.12310131807203,
			"seed": 2093981201,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					11.583575237522382,
					0
				],
				[
					20.850435427539196,
					0
				],
				[
					34.75072571256533,
					0
				],
				[
					41.70087085507748,
					2.316715047504431
				],
				[
					44.01758590258214,
					2.316715047504431
				],
				[
					46.3343009500868,
					4.6334300950086345
				],
				[
					46.3343009500868,
					6.950145142512838
				],
				[
					46.3343009500868,
					9.266860190017269
				],
				[
					46.3343009500868,
					11.583575237521472
				],
				[
					46.3343009500868,
					13.900290285025903
				],
				[
					46.3343009500868,
					16.217005332530107
				],
				[
					46.3343009500868,
					18.533720380034538
				],
				[
					46.3343009500868,
					23.167150475042945
				],
				[
					46.3343009500868,
					25.483865522547376
				],
				[
					46.3343009500868,
					27.80058057005158
				],
				[
					46.3343009500868,
					30.11729561755601
				],
				[
					46.3343009500868,
					34.750725712564645
				],
				[
					46.3343009500868,
					37.06744076006885
				],
				[
					46.3343009500868,
					39.38415580757305
				],
				[
					46.3343009500868,
					44.017585902581686
				],
				[
					46.3343009500868,
					46.33430095008612
				],
				[
					46.3343009500868,
					50.96773104509475
				],
				[
					48.65101599759055,
					53.284446092598955
				],
				[
					48.65101599759055,
					55.60116114010316
				],
				[
					50.967731045095206,
					62.551306282616224
				],
				[
					50.967731045095206,
					64.86802133012043
				],
				[
					50.967731045095206,
					69.50145142512906
				],
				[
					50.967731045095206,
					71.81816647263327
				],
				[
					53.284446092598955,
					76.4515965676419
				],
				[
					53.284446092598955,
					78.76831161514633
				],
				[
					55.60116114010361,
					83.40174171015474
				],
				[
					57.91787618760827,
					85.71845675765917
				],
				[
					60.23459123511202,
					90.3518868526678
				],
				[
					60.23459123511202,
					92.668601900172
				],
				[
					62.55130628261668,
					94.98531694767644
				],
				[
					62.55130628261668,
					97.30203199518064
				],
				[
					64.86802133012043,
					101.93546209018928
				],
				[
					67.18473637762509,
					104.25217713769348
				],
				[
					67.18473637762509,
					106.56889218519791
				],
				[
					67.18473637762509,
					111.20232228020654
				],
				[
					67.18473637762509,
					118.15246742271938
				],
				[
					67.18473637762509,
					122.78589751772802
				],
				[
					64.86802133012043,
					129.73604266024086
				],
				[
					62.55130628261668,
					139.00290285025812
				],
				[
					57.91787618760827,
					148.26976304027517
				],
				[
					53.284446092598955,
					164.48676837280527
				],
				[
					53.284446092598955,
					171.43691351531834
				],
				[
					53.284446092598955,
					180.70377370533538
				],
				[
					53.284446092598955,
					185.337203800344
				],
				[
					53.284446092598955,
					189.97063389535265
				],
				[
					53.284446092598955,
					194.60406399036128
				],
				[
					53.284446092598955,
					203.87092418037855
				],
				[
					53.284446092598955,
					208.50435427538696
				],
				[
					53.284446092598955,
					215.45449941790002
				],
				[
					55.60116114010361,
					229.3547897029257
				],
				[
					55.60116114010361,
					236.30493484543854
				],
				[
					57.91787618760827,
					243.2550799879516
				],
				[
					60.23459123511202,
					247.88851008296024
				],
				[
					62.55130628261668,
					252.52194017796865
				],
				[
					62.55130628261668,
					254.83865522547308
				],
				[
					64.86802133012043,
					257.1553702729773
				],
				[
					64.86802133012043,
					261.7888003679859
				],
				[
					64.86802133012043,
					264.10551541549034
				],
				[
					64.86802133012043,
					268.73894551049875
				],
				[
					64.86802133012043,
					271.0556605580032
				],
				[
					62.55130628261668,
					273.3723756055074
				],
				[
					62.55130628261668,
					275.6890906530118
				],
				[
					55.60116114010361,
					280.32252074802045
				],
				[
					50.967731045095206,
					282.63923579552466
				],
				[
					44.01758590258214,
					284.95595084302886
				],
				[
					39.384155807573734,
					289.5893809380375
				],
				[
					34.75072571256533,
					294.2228110330461
				],
				[
					30.11729561755601,
					294.2228110330461
				],
				[
					27.80058057005226,
					296.53952608055056
				],
				[
					23.167150475043854,
					298.85624112805476
				],
				[
					20.850435427539196,
					301.17295617555897
				],
				[
					18.533720380034538,
					303.4896712230634
				],
				[
					16.21700533253079,
					303.4896712230634
				],
				[
					16.21700533253079,
					305.8063862705676
				],
				[
					16.21700533253079,
					308.12310131807203
				],
				[
					16.21700533253079,
					308.12310131807203
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 91,
			"versionNonce": 1631713991,
			"isDeleted": false,
			"id": "93WlSg2I8MVJR08NRW7uh",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2405.257511641753,
			"y": 89.41027793254375,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 71.8181664726335,
			"height": 338.2403969356278,
			"seed": 1027875249,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.3167150475046583,
					0
				],
				[
					4.633430095008407,
					0
				],
				[
					9.266860190016814,
					-2.316715047504431
				],
				[
					18.533720380034538,
					-2.316715047504431
				],
				[
					25.483865522547603,
					-2.316715047504431
				],
				[
					30.11729561755601,
					-2.316715047504431
				],
				[
					32.43401066505976,
					0
				],
				[
					34.75072571256442,
					2.3167150475042035
				],
				[
					37.067440760069076,
					2.3167150475042035
				],
				[
					39.384155807572824,
					4.6334300950086345
				],
				[
					41.70087085507748,
					6.950145142512838
				],
				[
					41.70087085507748,
					9.266860190017269
				],
				[
					41.70087085507748,
					13.900290285025676
				],
				[
					41.70087085507748,
					18.53372038003431
				],
				[
					39.384155807572824,
					23.167150475042945
				],
				[
					34.75072571256442,
					32.434010665060214
				],
				[
					30.11729561755601,
					41.70087085507748
				],
				[
					27.800580570051352,
					46.33430095008589
				],
				[
					25.483865522547603,
					55.60116114010316
				],
				[
					25.483865522547603,
					60.23459123511179
				],
				[
					25.483865522547603,
					64.86802133012043
				],
				[
					23.167150475042945,
					74.13488152013747
				],
				[
					23.167150475042945,
					83.40174171015474
				],
				[
					23.167150475042945,
					94.98531694767621
				],
				[
					23.167150475042945,
					104.25217713769348
				],
				[
					23.167150475042945,
					113.51903732771075
				],
				[
					23.167150475042945,
					122.78589751772779
				],
				[
					23.167150475042945,
					129.73604266024086
				],
				[
					25.483865522547603,
					136.6861878027537
				],
				[
					27.800580570051352,
					141.31961789776233
				],
				[
					30.11729561755601,
					143.63633294526653
				],
				[
					34.75072571256442,
					145.95304799277096
				],
				[
					39.384155807572824,
					148.26976304027517
				],
				[
					46.33430095008589,
					148.26976304027517
				],
				[
					55.601161140102704,
					150.58647808777937
				],
				[
					62.55130628261577,
					152.9031931352838
				],
				[
					69.50145142512883,
					152.9031931352838
				],
				[
					71.8181664726335,
					152.9031931352838
				],
				[
					71.8181664726335,
					155.219908182788
				],
				[
					67.18473637762418,
					159.85333827779664
				],
				[
					57.91787618760736,
					166.80348342030948
				],
				[
					50.9677310450943,
					171.4369135153181
				],
				[
					46.33430095008589,
					178.38705865783118
				],
				[
					44.01758590258123,
					187.65391884784822
				],
				[
					39.384155807572824,
					194.60406399036128
				],
				[
					39.384155807572824,
					206.18763922788276
				],
				[
					37.067440760069076,
					213.1377843703956
				],
				[
					34.75072571256442,
					231.6715047504299
				],
				[
					32.43401066505976,
					247.88851008296
				],
				[
					32.43401066505976,
					261.7888003679859
				],
				[
					32.43401066505976,
					278.005805700516
				],
				[
					30.11729561755601,
					291.9060959855417
				],
				[
					27.800580570051352,
					303.48967122306317
				],
				[
					25.483865522547603,
					315.07324646058487
				],
				[
					23.167150475042945,
					328.97353674561055
				],
				[
					20.850435427538287,
					333.6069668406192
				],
				[
					16.21700533252988,
					335.9236818881234
				],
				[
					13.90029028502613,
					335.9236818881234
				],
				[
					13.90029028502613,
					335.9236818881234
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 48,
			"versionNonce": 1208301865,
			"isDeleted": false,
			"id": "FSqjIhEND4oiJYArbnotO",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2062.383684611116,
			"y": 128.7944337401168,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 60.23459123511202,
			"height": 2.316715047504431,
			"seed": 916638737,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.316715047504431
				],
				[
					2.3167150475046583,
					2.316715047504431
				],
				[
					9.266860190017724,
					2.316715047504431
				],
				[
					13.90029028502613,
					2.316715047504431
				],
				[
					20.850435427539196,
					2.316715047504431
				],
				[
					25.483865522547603,
					2.316715047504431
				],
				[
					27.800580570051352,
					2.316715047504431
				],
				[
					32.43401066506067,
					2.316715047504431
				],
				[
					34.75072571256442,
					2.316715047504431
				],
				[
					37.067440760069076,
					2.316715047504431
				],
				[
					41.70087085507748,
					2.316715047504431
				],
				[
					48.65101599759055,
					2.316715047504431
				],
				[
					53.284446092598955,
					2.316715047504431
				],
				[
					57.91787618760736,
					2.316715047504431
				],
				[
					60.23459123511202,
					2.316715047504431
				],
				[
					60.23459123511202,
					2.316715047504431
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 61,
			"versionNonce": 283445735,
			"isDeleted": false,
			"id": "t2HJnQIXY6nK8SPx27N7i",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2076.2839748961424,
			"y": 221.4630356402888,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 155.21990818278755,
			"height": 9.266860190017269,
			"seed": 1264548305,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-2.3167150475042035
				],
				[
					4.633430095008407,
					-2.3167150475042035
				],
				[
					16.21700533252988,
					-2.3167150475042035
				],
				[
					32.43401066505976,
					-2.3167150475042035
				],
				[
					44.01758590258123,
					-2.3167150475042035
				],
				[
					57.91787618760736,
					-2.3167150475042035
				],
				[
					67.18473637762418,
					-2.3167150475042035
				],
				[
					71.8181664726335,
					-2.3167150475042035
				],
				[
					78.76831161514565,
					-2.3167150475042035
				],
				[
					83.40174171015497,
					-4.6334300950086345
				],
				[
					92.66860190017178,
					-4.6334300950086345
				],
				[
					97.30203199518019,
					-6.950145142512838
				],
				[
					104.25217713769325,
					-6.950145142512838
				],
				[
					111.20232228020632,
					-6.950145142512838
				],
				[
					118.15246742271938,
					-9.266860190017269
				],
				[
					120.46918247022313,
					-9.266860190017269
				],
				[
					125.10261256523245,
					-9.266860190017269
				],
				[
					127.4193276127362,
					-9.266860190017269
				],
				[
					129.73604266024086,
					-9.266860190017269
				],
				[
					134.36947275524926,
					-9.266860190017269
				],
				[
					139.00290285025767,
					-9.266860190017269
				],
				[
					141.31961789776233,
					-9.266860190017269
				],
				[
					143.63633294526608,
					-9.266860190017269
				],
				[
					145.95304799277073,
					-9.266860190017269
				],
				[
					148.2697630402754,
					-9.266860190017269
				],
				[
					150.58647808777914,
					-9.266860190017269
				],
				[
					152.9031931352838,
					-9.266860190017269
				],
				[
					155.21990818278755,
					-9.266860190017269
				],
				[
					155.21990818278755,
					-9.266860190017269
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 58,
			"versionNonce": 590752777,
			"isDeleted": false,
			"id": "GUA8_PaMNbE-qBAKe6HTQ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2233.8205981264346,
			"y": 233.04661087781028,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 132.0527577077455,
			"height": 6.950145142512838,
			"seed": 1531812849,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-2.3167150475042035
				],
				[
					2.3167150475046583,
					-4.6334300950086345
				],
				[
					6.950145142513065,
					-4.6334300950086345
				],
				[
					9.266860190016814,
					-6.950145142512838
				],
				[
					16.21700533252988,
					-6.950145142512838
				],
				[
					20.850435427539196,
					-6.950145142512838
				],
				[
					27.800580570051352,
					-6.950145142512838
				],
				[
					34.75072571256442,
					-6.950145142512838
				],
				[
					41.70087085507748,
					-6.950145142512838
				],
				[
					55.60116114010361,
					-6.950145142512838
				],
				[
					62.55130628261577,
					-6.950145142512838
				],
				[
					69.50145142512883,
					-6.950145142512838
				],
				[
					78.76831161514656,
					-6.950145142512838
				],
				[
					83.40174171015497,
					-6.950145142512838
				],
				[
					92.66860190017178,
					-6.950145142512838
				],
				[
					101.9354620901895,
					-6.950145142512838
				],
				[
					106.56889218519791,
					-6.950145142512838
				],
				[
					108.88560723270257,
					-6.950145142512838
				],
				[
					111.20232228020632,
					-6.950145142512838
				],
				[
					115.83575237521472,
					-6.950145142512838
				],
				[
					118.15246742271938,
					-6.950145142512838
				],
				[
					122.78589751772779,
					-6.950145142512838
				],
				[
					127.4193276127362,
					-6.950145142512838
				],
				[
					129.73604266024086,
					-6.950145142512838
				],
				[
					132.0527577077455,
					-6.950145142512838
				],
				[
					132.0527577077455,
					-6.950145142512838
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 33,
			"versionNonce": 1939420423,
			"isDeleted": false,
			"id": "Z7APOohYKH5Lew1X-6F0D",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1585.1403848252305,
			"y": -800.2083003091075,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 969463921,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 109,
			"versionNonce": 361087721,
			"isDeleted": false,
			"id": "bKu-76BXy3G8z12ebCTKd",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -101.87819228052324,
			"y": 761.4344295743317,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 2.866273793743408,
			"height": 0,
			"seed": 1193083409,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.866273793743408,
					0
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 107,
			"versionNonce": 1088093223,
			"isDeleted": false,
			"id": "uVcdKI2S7AzugdHcYzbyl",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -142.00602539293095,
			"y": 930.5445834051927,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 0.00009505872693720059,
			"height": 0.00009505872693720059,
			"seed": 2063898481,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.00009505872693720059,
					0.00009505872693720059
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 180,
			"versionNonce": 192904649,
			"isDeleted": false,
			"id": "yAgTIzPi",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.27347780544414,
			"y": 835.9575482116605,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 252.16879272460938,
			"height": 72.37417619079872,
			"seed": 1482498321,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 57.89934095263898,
			"fontFamily": 1,
			"text": "ffff8100",
			"rawText": "ffff8100",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ffff8100",
			"lineHeight": 1.25,
			"baseline": 50
		},
		{
			"type": "text",
			"version": 180,
			"versionNonce": 211214151,
			"isDeleted": false,
			"id": "pclIIdph",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.27347780544414,
			"y": 937.2813948787787,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 317.2370910644531,
			"height": 72.37417619079869,
			"seed": 1078850687,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 57.89934095263896,
			"fontFamily": 1,
			"text": "00000024",
			"rawText": "00000024",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000024",
			"lineHeight": 1.25,
			"baseline": 50
		},
		{
			"type": "text",
			"version": 180,
			"versionNonce": 1413405865,
			"isDeleted": false,
			"id": "anAYAsT3",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.27347780544414,
			"y": 1038.605241545897,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 320.01580810546875,
			"height": 72.37417619079872,
			"seed": 723048177,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 57.89934095263897,
			"fontFamily": 1,
			"text": "00000002",
			"rawText": "00000002",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000002",
			"lineHeight": 1.25,
			"baseline": 50
		},
		{
			"type": "text",
			"version": 180,
			"versionNonce": 959012455,
			"isDeleted": false,
			"id": "S9nwtV8S",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.27347780544414,
			"y": 1139.9290882130151,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 271.735595703125,
			"height": 72.37417619079869,
			"seed": 1354304671,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 57.89934095263896,
			"fontFamily": 1,
			"text": "01010200",
			"rawText": "01010200",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "01010200",
			"lineHeight": 1.25,
			"baseline": 50
		},
		{
			"type": "text",
			"version": 180,
			"versionNonce": 1332699017,
			"isDeleted": false,
			"id": "cXRKsItg",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.27347780544414,
			"y": 1241.2529348801331,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 307.85894775390625,
			"height": 72.37417619079872,
			"seed": 2091045073,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 57.89934095263897,
			"fontFamily": 1,
			"text": "c0000000",
			"rawText": "c0000000",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "c0000000",
			"lineHeight": 1.25,
			"baseline": 50
		},
		{
			"type": "text",
			"version": 180,
			"versionNonce": 694090119,
			"isDeleted": false,
			"id": "0YSCWSK5",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.27347780544414,
			"y": 1342.5767815472514,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 294.486328125,
			"height": 72.3741761907987,
			"seed": 810295487,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 57.899340952638966,
			"fontFamily": 1,
			"text": "00000010",
			"rawText": "00000010",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000010",
			"lineHeight": 1.25,
			"baseline": 50
		},
		{
			"type": "text",
			"version": 180,
			"versionNonce": 1531741801,
			"isDeleted": false,
			"id": "mgkzBhv2",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.27347780544414,
			"y": 1443.9006282143696,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 318.62646484375,
			"height": 72.37417619079872,
			"seed": 1653771953,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 57.89934095263898,
			"fontFamily": 1,
			"text": "00000000",
			"rawText": "00000000",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000000",
			"lineHeight": 1.25,
			"baseline": 50
		},
		{
			"type": "text",
			"version": 180,
			"versionNonce": 846475431,
			"isDeleted": false,
			"id": "eKwKXi1e",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.27347780544414,
			"y": 1545.2244748814878,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 281.6347961425781,
			"height": 72.37417619079872,
			"seed": 816296159,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 57.89934095263897,
			"fontFamily": 1,
			"text": "12345678",
			"rawText": "12345678",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "12345678",
			"lineHeight": 1.25,
			"baseline": 50
		},
		{
			"type": "text",
			"version": 180,
			"versionNonce": 44159305,
			"isDeleted": false,
			"id": "wFvV7QR3",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.27347780544414,
			"y": 1646.548321548606,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 225.0762939453125,
			"height": 72.37417619079872,
			"seed": 1401917585,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 57.89934095263897,
			"fontFamily": 1,
			"text": "ffffffff",
			"rawText": "ffffffff",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ffffffff",
			"lineHeight": 1.25,
			"baseline": 50
		},
		{
			"type": "text",
			"version": 180,
			"versionNonce": 1310032839,
			"isDeleted": false,
			"id": "7wfhTDt8",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.27347780544414,
			"y": 1747.8721682157243,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 225.0762939453125,
			"height": 72.37417619079872,
			"seed": 459029759,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 57.89934095263897,
			"fontFamily": 1,
			"text": "ffffffff",
			"rawText": "ffffffff",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ffffffff",
			"lineHeight": 1.25,
			"baseline": 50
		},
		{
			"type": "text",
			"version": 180,
			"versionNonce": 1791672361,
			"isDeleted": false,
			"id": "iWvg51tR",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.27347780544414,
			"y": 1849.1960148828425,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 318.62646484375,
			"height": 72.37417619079872,
			"seed": 89216625,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"fontSize": 57.89934095263898,
			"fontFamily": 1,
			"text": "00000000",
			"rawText": "00000000",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000000",
			"lineHeight": 1.25,
			"baseline": 50
		},
		{
			"type": "freedraw",
			"version": 32,
			"versionNonce": 207581927,
			"isDeleted": false,
			"id": "DLt5KyP6uEXVxBJ-4YvOk",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 629.9021568858684,
			"y": 1053.915264265908,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 1135428689,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 183,
			"versionNonce": 28496649,
			"isDeleted": false,
			"id": "vR1yVaCy-kTGN-i5sOr2V",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -323.29339246698,
			"y": 1322.5746196083082,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 2703.606460437518,
			"height": 46.33430095008589,
			"seed": 557218289,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					9.266860190017269,
					0
				],
				[
					20.85043542753874,
					0
				],
				[
					30.117295617555897,
					0
				],
				[
					39.384155807573165,
					0
				],
				[
					50.96773104509464,
					0
				],
				[
					57.917876187607476,
					0
				],
				[
					64.86802133012043,
					0
				],
				[
					67.18473637762474,
					0
				],
				[
					76.4515965676419,
					0
				],
				[
					81.08502666265053,
					0
				],
				[
					88.03517180516337,
					0
				],
				[
					97.30203199518064,
					0
				],
				[
					111.20232228020643,
					0
				],
				[
					122.7858975177279,
					0
				],
				[
					141.31961789776233,
					0
				],
				[
					152.9031931352838,
					0
				],
				[
					164.48676837280527,
					0
				],
				[
					176.07034361032686,
					2.3167150475042035
				],
				[
					189.97063389535253,
					2.3167150475042035
				],
				[
					203.87092418037844,
					2.3167150475042035
				],
				[
					220.08792951290854,
					2.3167150475042035
				],
				[
					243.2550799879515,
					2.3167150475042035
				],
				[
					257.1553702729774,
					2.3167150475042035
				],
				[
					271.05566055800307,
					2.3167150475042035
				],
				[
					282.63923579552454,
					2.3167150475042035
				],
				[
					291.9060959855418,
					4.6334300950086345
				],
				[
					305.8063862705677,
					4.6334300950086345
				],
				[
					319.7066765555934,
					4.6334300950086345
				],
				[
					331.29025179311486,
					4.6334300950086345
				],
				[
					349.8239721731494,
					4.6334300950086345
				],
				[
					372.99112264819234,
					2.3167150475042035
				],
				[
					384.5746978857138,
					2.3167150475042035
				],
				[
					398.4749881707397,
					2.3167150475042035
				],
				[
					412.3752784557654,
					2.3167150475042035
				],
				[
					426.2755687407913,
					2.3167150475042035
				],
				[
					444.8092891208256,
					2.3167150475042035
				],
				[
					479.56001483339,
					2.3167150475042035
				],
				[
					502.7271653084332,
					2.3167150475042035
				],
				[
					528.2110308309803,
					2.3167150475042035
				],
				[
					551.3781813060235,
					2.3167150475042035
				],
				[
					572.228616733562,
					2.3167150475042035
				],
				[
					597.7124822561094,
					2.3167150475042035
				],
				[
					620.8796327311524,
					2.3167150475042035
				],
				[
					655.630358443717,
					6.950145142512838
				],
				[
					706.5980894888115,
					6.950145142512838
				],
				[
					741.3488152013759,
					6.950145142512838
				],
				[
					773.7828258664362,
					6.950145142512838
				],
				[
					813.1669816740092,
					11.583575237521472
				],
				[
					850.234422434078,
					13.900290285025903
				],
				[
					891.9352932891555,
					18.53372038003431
				],
				[
					947.5364544292587,
					23.167150475042945
				],
				[
					963.7534597617888,
					23.167150475042945
				],
				[
					1007.7710456643705,
					23.167150475042945
				],
				[
					1037.8883412819264,
					23.167150475042945
				],
				[
					1063.3722068044735,
					23.167150475042945
				],
				[
					1088.8560723270211,
					20.85043542753874
				],
				[
					1114.3399378495683,
					20.85043542753874
				],
				[
					1158.35752375215,
					18.53372038003431
				],
				[
					1179.2079591796887,
					18.53372038003431
				],
				[
					1202.3751096547317,
					18.53372038003431
				],
				[
					1225.5422601297746,
					16.217005332530107
				],
				[
					1251.0261256523218,
					13.900290285025903
				],
				[
					1276.5099911748694,
					11.583575237521472
				],
				[
					1311.2607168874338,
					11.583575237521472
				],
				[
					1348.3281576475024,
					11.583575237521472
				],
				[
					1410.8794639301186,
					11.583575237521472
				],
				[
					1459.5304799277087,
					11.583575237521472
				],
				[
					1515.1316410678119,
					11.583575237521472
				],
				[
					1570.7328022079155,
					11.583575237521472
				],
				[
					1642.5509686805485,
					11.583575237521472
				],
				[
					1668.0348342030957,
					11.583575237521472
				],
				[
					1707.418990010669,
					11.583575237521472
				],
				[
					1760.703436103268,
					11.583575237521472
				],
				[
					1797.7708768633365,
					9.266860190017269
				],
				[
					1830.2048875283967,
					6.950145142512838
				],
				[
					1860.3221831459527,
					6.950145142512838
				],
				[
					1895.0729088585172,
					4.6334300950086345
				],
				[
					1929.8236345710816,
					4.6334300950086345
				],
				[
					1985.4247957111852,
					4.6334300950086345
				],
				[
					2029.4423816137669,
					4.6334300950086345
				],
				[
					2066.5098223738355,
					4.6334300950086345
				],
				[
					2101.2605480864,
					4.6334300950086345
				],
				[
					2131.377843703956,
					2.3167150475042035
				],
				[
					2152.2282791314947,
					2.3167150475042035
				],
				[
					2184.662289796555,
					2.3167150475042035
				],
				[
					2205.5127252240936,
					2.3167150475042035
				],
				[
					2221.7297305566235,
					2.3167150475042035
				],
				[
					2233.313305794145,
					2.3167150475042035
				],
				[
					2240.263450936658,
					0
				],
				[
					2247.213596079171,
					0
				],
				[
					2256.480456269188,
					-2.3167150475042035
				],
				[
					2277.3308916967267,
					-2.3167150475042035
				],
				[
					2302.8147572192743,
					-2.3167150475042035
				],
				[
					2337.5654829318387,
					-2.3167150475042035
				],
				[
					2369.999493596899,
					0
				],
				[
					2379.266353786916,
					0
				],
				[
					2383.8997838819246,
					0
				],
				[
					2388.533213976933,
					0
				],
				[
					2395.483359119446,
					-2.3167150475042035
				],
				[
					2414.0170794994806,
					-4.6334300950086345
				],
				[
					2455.717950354558,
					-4.6334300950086345
				],
				[
					2471.934955687088,
					-4.6334300950086345
				],
				[
					2485.8352459721136,
					-4.6334300950086345
				],
				[
					2490.4686760671225,
					-2.3167150475042035
				],
				[
					2495.102106162131,
					-2.3167150475042035
				],
				[
					2499.7355362571398,
					-2.3167150475042035
				],
				[
					2513.6358265421654,
					-2.3167150475042035
				],
				[
					2536.8029770172084,
					-2.3167150475042035
				],
				[
					2555.336697397243,
					-2.3167150475042035
				],
				[
					2569.2369876822686,
					-2.3167150475042035
				],
				[
					2580.82056291979,
					-4.6334300950086345
				],
				[
					2585.4539930147985,
					-6.950145142512838
				],
				[
					2592.4041381573115,
					-11.583575237521472
				],
				[
					2601.670998347329,
					-16.217005332530107
				],
				[
					2615.5712886323545,
					-18.53372038003431
				],
				[
					2624.8381488223717,
					-18.53372038003431
				],
				[
					2652.6387293924236,
					-18.53372038003431
				],
				[
					2666.5390196774492,
					-18.53372038003431
				],
				[
					2675.8058798674665,
					-20.85043542753874
				],
				[
					2682.756025009979,
					-23.167150475042945
				],
				[
					2689.706170152492,
					-23.167150475042945
				],
				[
					2694.3396002475006,
					-23.167150475042945
				],
				[
					2703.606460437518,
					-23.167150475042945
				],
				[
					2703.606460437518,
					-23.167150475042945
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 35,
			"versionNonce": 1172209159,
			"isDeleted": false,
			"id": "T3lhp4_UkzzYwaZi1Y1oz",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1052.835345750574,
			"y": 1452.310662268549,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 2.3167150475042035,
			"height": 2.3167150475042035,
			"seed": 39486001,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.3167150475042035
				],
				[
					-2.3167150475042035,
					2.3167150475042035
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 29,
			"versionNonce": 1809156585,
			"isDeleted": false,
			"id": "u1-dLVURQ7VEUixcHTmcK",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 202.99363885066418,
			"y": 1382.3404029819933,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 1398476191,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299016,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 37,
			"versionNonce": 227484967,
			"isDeleted": false,
			"id": "ny34HWLPmsZc15yfpg2FT",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 200.67692380315998,
			"y": 1389.2905481245061,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 92.668601900172,
			"height": 2.316715047504431,
			"seed": 1463960945,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					4.633430095008407,
					0
				],
				[
					20.850435427538514,
					0
				],
				[
					41.700870855077255,
					0
				],
				[
					74.13488152013747,
					0
				],
				[
					83.40174171015474,
					2.316715047504431
				],
				[
					88.03517180516337,
					2.316715047504431
				],
				[
					90.35188685266758,
					2.316715047504431
				],
				[
					92.668601900172,
					2.316715047504431
				],
				[
					92.668601900172,
					2.316715047504431
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 33,
			"versionNonce": 842949833,
			"isDeleted": false,
			"id": "jpbWzyCBik_lpHrqDxU_4",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 314.1959611308705,
			"y": 1363.806682601959,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 16.217005332530107,
			"height": 6.950145142513065,
			"seed": 406105617,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-2.316715047504431
				],
				[
					-4.6334300950086345,
					0
				],
				[
					-16.217005332530107,
					4.6334300950086345
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 35,
			"versionNonce": 1658710087,
			"isDeleted": false,
			"id": "fmsWjpfV5lolW4FsxsGW_",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 288.71209560832335,
			"y": 1361.4899675544546,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 16.217005332530107,
			"height": 39.38415580757328,
			"seed": 1184455473,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					13.900290285025903
				],
				[
					4.6334300950086345,
					23.167150475043172
				],
				[
					11.583575237521472,
					30.11729561755601
				],
				[
					13.900290285025676,
					37.06744076006885
				],
				[
					16.217005332530107,
					37.06744076006885
				],
				[
					16.217005332530107,
					39.38415580757328
				],
				[
					16.217005332530107,
					39.38415580757328
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 35,
			"versionNonce": 814277545,
			"isDeleted": false,
			"id": "7U6hZLTjC585Tuyy25meq",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 279.4452354183061,
			"y": 1393.9239782195148,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 44.017585902581686,
			"height": 2.316715047504431,
			"seed": 1989012497,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					4.6334300950086345,
					0
				],
				[
					13.900290285025903,
					2.316715047504431
				],
				[
					27.80058057005158,
					2.316715047504431
				],
				[
					37.06744076006885,
					2.316715047504431
				],
				[
					41.70087085507748,
					2.316715047504431
				],
				[
					44.017585902581686,
					0
				],
				[
					44.017585902581686,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 70,
			"versionNonce": 598165351,
			"isDeleted": false,
			"id": "0X0XIPPV",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 376.7472674134867,
			"y": 1373.073542791976,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 129.99993896484375,
			"height": 25,
			"seed": 473004689,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "长度为16 byte",
			"rawText": "长度为16 byte",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "长度为16 byte",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 38,
			"versionNonce": 1122010761,
			"isDeleted": false,
			"id": "6UdL1baeafEsT3RFwVFAF",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -135.24675808496363,
			"y": 1505.1263004997213,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 69.50145142512906,
			"height": 4.6334300950086345,
			"seed": 98020287,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					9.266860190017269,
					-2.316715047504431
				],
				[
					30.11729561755601,
					-2.316715047504431
				],
				[
					44.017585902581686,
					-2.316715047504431
				],
				[
					53.284446092598955,
					-2.316715047504431
				],
				[
					60.23459123511179,
					-2.316715047504431
				],
				[
					62.551306282616,
					-2.316715047504431
				],
				[
					64.86802133012043,
					-4.6334300950086345
				],
				[
					67.18473637762463,
					-4.6334300950086345
				],
				[
					69.50145142512906,
					-4.6334300950086345
				],
				[
					69.50145142512906,
					-4.6334300950086345
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 48,
			"versionNonce": 1043841671,
			"isDeleted": false,
			"id": "DgIkk6_rgI-uQRScPw7t-",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -121.34646779993773,
			"y": 1609.3784776374148,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 127.41932761273642,
			"height": 6.950145142513065,
			"seed": 2046354751,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					6.950145142512838,
					0
				],
				[
					16.217005332530107,
					0
				],
				[
					34.75072571256442,
					0
				],
				[
					55.60116114010316,
					-2.316715047504431
				],
				[
					71.81816647263327,
					-2.316715047504431
				],
				[
					81.08502666265031,
					-2.316715047504431
				],
				[
					85.71845675765894,
					-2.316715047504431
				],
				[
					88.03517180516337,
					-2.316715047504431
				],
				[
					90.35188685266758,
					-2.316715047504431
				],
				[
					94.98531694767621,
					-2.316715047504431
				],
				[
					97.30203199518041,
					-4.6334300950086345
				],
				[
					101.93546209018905,
					-4.6334300950086345
				],
				[
					108.88560723270211,
					-6.950145142513065
				],
				[
					113.51903732771052,
					-6.950145142513065
				],
				[
					118.15246742271916,
					-6.950145142513065
				],
				[
					120.46918247022359,
					-6.950145142513065
				],
				[
					122.78589751772779,
					-6.950145142513065
				],
				[
					125.102612565232,
					-6.950145142513065
				],
				[
					127.41932761273642,
					-6.950145142513065
				],
				[
					127.41932761273642,
					-6.950145142513065
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 52,
			"versionNonce": 872467817,
			"isDeleted": false,
			"id": "6rWMsYewjLJUJYWzbh-xE",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 13.023004955311535,
			"y": 1618.6453378274318,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 143.63633294526653,
			"height": 16.217005332530107,
			"seed": 2015251455,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					4.6334300950086345,
					-2.3167150475042035
				],
				[
					9.266860190017269,
					-2.3167150475042035
				],
				[
					18.533720380034538,
					-4.633430095008407
				],
				[
					27.80058057005158,
					-6.950145142512838
				],
				[
					34.750725712564645,
					-6.950145142512838
				],
				[
					44.017585902581686,
					-9.266860190017042
				],
				[
					48.65101599759032,
					-11.583575237521472
				],
				[
					55.60116114010316,
					-11.583575237521472
				],
				[
					60.23459123511179,
					-13.900290285025676
				],
				[
					69.50145142512906,
					-13.900290285025676
				],
				[
					74.1348815201377,
					-13.900290285025676
				],
				[
					85.71845675765917,
					-16.217005332530107
				],
				[
					94.98531694767644,
					-16.217005332530107
				],
				[
					99.61874704268484,
					-16.217005332530107
				],
				[
					106.56889218519791,
					-16.217005332530107
				],
				[
					113.51903732771075,
					-13.900290285025676
				],
				[
					120.46918247022359,
					-11.583575237521472
				],
				[
					127.41932761273665,
					-11.583575237521472
				],
				[
					134.3694727552495,
					-9.266860190017042
				],
				[
					136.6861878027537,
					-9.266860190017042
				],
				[
					139.00290285025812,
					-9.266860190017042
				],
				[
					141.31961789776233,
					-9.266860190017042
				],
				[
					143.63633294526653,
					-9.266860190017042
				],
				[
					143.63633294526653,
					-9.266860190017042
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 67,
			"versionNonce": 592173479,
			"isDeleted": false,
			"id": "_i7owc3azuSGj8HpefFXk",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 223.84407427820292,
			"y": 1470.3755747871567,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 60.23459123511179,
			"height": 322.0233916030977,
			"seed": 1660548415,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					9.266860190017269
				],
				[
					4.6334300950086345,
					20.85043542753874
				],
				[
					6.950145142512838,
					30.11729561755601
				],
				[
					11.583575237521472,
					41.70087085507748
				],
				[
					13.900290285025676,
					53.284446092598955
				],
				[
					13.900290285025676,
					64.86802133012043
				],
				[
					18.53372038003431,
					81.08502666265053
				],
				[
					18.53372038003431,
					90.3518868526678
				],
				[
					18.53372038003431,
					99.61874704268507
				],
				[
					20.85043542753874,
					113.51903732771075
				],
				[
					23.167150475042945,
					125.10261256523222
				],
				[
					23.167150475042945,
					136.6861878027537
				],
				[
					23.167150475042945,
					155.21990818278823
				],
				[
					23.167150475042945,
					169.1201984678139
				],
				[
					23.167150475042945,
					176.07034361032674
				],
				[
					23.167150475042945,
					185.337203800344
				],
				[
					23.167150475042945,
					194.60406399036128
				],
				[
					23.167150475042945,
					201.55420913287412
				],
				[
					20.85043542753874,
					213.1377843703956
				],
				[
					18.53372038003431,
					222.40464456041286
				],
				[
					16.217005332530107,
					236.30493484543877
				],
				[
					16.217005332530107,
					245.5717950354558
				],
				[
					13.900290285025676,
					254.83865522547308
				],
				[
					11.583575237521472,
					264.10551541549034
				],
				[
					9.266860190017042,
					271.0556605580032
				],
				[
					4.6334300950086345,
					280.32252074802045
				],
				[
					0,
					284.95595084302886
				],
				[
					-2.316715047504431,
					289.5893809380375
				],
				[
					-4.6334300950086345,
					291.9060959855419
				],
				[
					-6.950145142512838,
					296.53952608055056
				],
				[
					-9.266860190017269,
					301.17295617555897
				],
				[
					-13.900290285025903,
					305.8063862705676
				],
				[
					-16.217005332530107,
					308.12310131807203
				],
				[
					-23.167150475042945,
					312.75653141308067
				],
				[
					-27.80058057005158,
					315.07324646058487
				],
				[
					-32.434010665060214,
					317.3899615080891
				],
				[
					-32.434010665060214,
					319.7066765555935
				],
				[
					-37.06744076006885,
					319.7066765555935
				],
				[
					-37.06744076006885,
					322.0233916030977
				],
				[
					-37.06744076006885,
					322.0233916030977
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 63,
			"versionNonce": 1798649929,
			"isDeleted": false,
			"id": "T1Ut309A",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -152.68381342035053,
			"y": 1505.5988162080248,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 117.73988342285156,
			"height": 25,
			"seed": 1027180159,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "find servoce",
			"rawText": "find servoce",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "find servoce",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "text",
			"version": 139,
			"versionNonce": 2014317767,
			"isDeleted": false,
			"id": "6MRhbMd8",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 624.2352140841317,
			"y": 166.646136370647,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 120.29989624023438,
			"height": 25,
			"seed": 1934431729,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "option array",
			"rawText": "option array",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "option array",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 33,
			"versionNonce": 1515800361,
			"isDeleted": false,
			"id": "42dSqA4EKRQBZZFfsz4fV",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -81.57599758002101,
			"y": 96.13029926657464,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 10,
			"height": 2,
			"seed": 417108849,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-1
				],
				[
					2,
					-1
				],
				[
					7,
					-2
				],
				[
					8,
					-2
				],
				[
					10,
					-2
				],
				[
					10,
					-2
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 72,
			"versionNonce": 136371175,
			"isDeleted": false,
			"id": "xzQpYFTyjRdBNkOYm7e5X",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -79.57599758002101,
			"y": 96.13029926657464,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 238.9999999999999,
			"height": 6,
			"seed": 242045553,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2,
					0
				],
				[
					7,
					0
				],
				[
					14,
					0
				],
				[
					23,
					0
				],
				[
					36,
					1
				],
				[
					48,
					2
				],
				[
					62.99999999999994,
					2
				],
				[
					70.99999999999994,
					2
				],
				[
					75.99999999999994,
					2
				],
				[
					78.99999999999994,
					2
				],
				[
					80.99999999999994,
					1
				],
				[
					83.99999999999994,
					1
				],
				[
					86.99999999999994,
					1
				],
				[
					90.99999999999994,
					0
				],
				[
					95.99999999999994,
					0
				],
				[
					102.99999999999994,
					0
				],
				[
					108.99999999999994,
					0
				],
				[
					113.99999999999994,
					0
				],
				[
					119.99999999999994,
					0
				],
				[
					125.99999999999994,
					0
				],
				[
					135.99999999999994,
					0
				],
				[
					142.99999999999994,
					0
				],
				[
					149.99999999999994,
					0
				],
				[
					156.99999999999994,
					1
				],
				[
					162.99999999999994,
					2
				],
				[
					172.99999999999994,
					4
				],
				[
					182.9999999999999,
					5
				],
				[
					189.9999999999999,
					5
				],
				[
					198.9999999999999,
					6
				],
				[
					203.9999999999999,
					6
				],
				[
					206.9999999999999,
					6
				],
				[
					208.9999999999999,
					6
				],
				[
					211.9999999999999,
					6
				],
				[
					214.9999999999999,
					6
				],
				[
					217.9999999999999,
					6
				],
				[
					219.9999999999999,
					6
				],
				[
					224.9999999999999,
					6
				],
				[
					226.9999999999999,
					5
				],
				[
					229.9999999999999,
					5
				],
				[
					232.9999999999999,
					4
				],
				[
					235.9999999999999,
					3
				],
				[
					236.9999999999999,
					3
				],
				[
					237.9999999999999,
					3
				],
				[
					238.9999999999999,
					3
				],
				[
					238.9999999999999,
					3
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 49,
			"versionNonce": 735607305,
			"isDeleted": false,
			"id": "-YCpqIyTWcy_sH6BS8zEi",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 200.42400241997888,
			"y": 74.13029926657464,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 103.99999999999989,
			"height": 3,
			"seed": 1835779729,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					3,
					-1
				],
				[
					15,
					-1
				],
				[
					28,
					-1
				],
				[
					42,
					-1
				],
				[
					47,
					-1
				],
				[
					51,
					-1
				],
				[
					54,
					-1
				],
				[
					57,
					-2
				],
				[
					61,
					-2
				],
				[
					65,
					-2
				],
				[
					73,
					-2
				],
				[
					80,
					-3
				],
				[
					84,
					-3
				],
				[
					87,
					-3
				],
				[
					90.99999999999989,
					-3
				],
				[
					93.99999999999989,
					-3
				],
				[
					97.99999999999989,
					-3
				],
				[
					98.99999999999989,
					-3
				],
				[
					101.99999999999989,
					-3
				],
				[
					102.99999999999989,
					-3
				],
				[
					103.99999999999989,
					-3
				],
				[
					103.99999999999989,
					-3
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 39,
			"versionNonce": 2005583623,
			"isDeleted": false,
			"id": "-aJx7vI6LhxOBgh3aJz4E",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 301.42400241997876,
			"y": 50.13029926657464,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 19,
			"height": 33,
			"seed": 1048159121,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					4,
					8
				],
				[
					7,
					12
				],
				[
					10,
					17
				],
				[
					14,
					21
				],
				[
					16,
					23
				],
				[
					18,
					25
				],
				[
					18,
					26
				],
				[
					19,
					27
				],
				[
					18,
					29
				],
				[
					13,
					31
				],
				[
					12,
					33
				],
				[
					12,
					33
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 83,
			"versionNonce": 816730345,
			"isDeleted": false,
			"id": "iJgU9UBM",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 342.2740542998616,
			"y": 56.63029926657464,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 257.83984375,
			"height": 25,
			"seed": 728825777,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "option array len = 12 字节",
			"rawText": "option array len = 12 字节",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "option array len = 12 字节",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 99,
			"versionNonce": 885673511,
			"isDeleted": false,
			"id": "UgjZbYzO3U8DVAssBWeyW",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -288.57599758002095,
			"y": 33.13029926657464,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 1386.9999999999995,
			"height": 26,
			"seed": 179795423,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1,
					0
				],
				[
					2,
					0
				],
				[
					4,
					-1
				],
				[
					10,
					-2
				],
				[
					20,
					-3
				],
				[
					32,
					-3
				],
				[
					45,
					-4
				],
				[
					63,
					-5
				],
				[
					80,
					-6
				],
				[
					98,
					-6
				],
				[
					117.99999999999997,
					-6
				],
				[
					137.99999999999997,
					-6
				],
				[
					169.99999999999994,
					-6
				],
				[
					191.99999999999994,
					-6
				],
				[
					211.99999999999994,
					-6
				],
				[
					228.99999999999994,
					-6
				],
				[
					250.99999999999994,
					-6
				],
				[
					282.9999999999999,
					-6
				],
				[
					304.9999999999999,
					-6
				],
				[
					331.9999999999999,
					-6
				],
				[
					356.9999999999999,
					-6
				],
				[
					380.9999999999999,
					-6
				],
				[
					406.99999999999983,
					-6
				],
				[
					431.99999999999983,
					-6
				],
				[
					458.99999999999983,
					-7
				],
				[
					495.99999999999983,
					-10
				],
				[
					521.9999999999998,
					-12
				],
				[
					558.9999999999998,
					-17
				],
				[
					571.9999999999998,
					-19
				],
				[
					597.9999999999998,
					-21
				],
				[
					633.9999999999998,
					-21
				],
				[
					656.9999999999998,
					-21
				],
				[
					678.9999999999998,
					-21
				],
				[
					701.9999999999998,
					-21
				],
				[
					728.9999999999998,
					-21
				],
				[
					753.9999999999998,
					-21
				],
				[
					781.9999999999998,
					-22
				],
				[
					812.9999999999997,
					-22
				],
				[
					840.9999999999997,
					-22
				],
				[
					888.9999999999997,
					-25
				],
				[
					928.9999999999997,
					-25
				],
				[
					969.9999999999997,
					-25
				],
				[
					1008.9999999999997,
					-24
				],
				[
					1039.9999999999995,
					-24
				],
				[
					1068.9999999999995,
					-24
				],
				[
					1107.9999999999995,
					-23
				],
				[
					1120.9999999999995,
					-23
				],
				[
					1151.9999999999995,
					-23
				],
				[
					1165.9999999999995,
					-23
				],
				[
					1181.9999999999995,
					-23
				],
				[
					1195.9999999999995,
					-23
				],
				[
					1208.9999999999995,
					-23
				],
				[
					1230.9999999999995,
					-23
				],
				[
					1243.9999999999995,
					-23
				],
				[
					1255.9999999999995,
					-23
				],
				[
					1269.9999999999995,
					-23
				],
				[
					1280.9999999999995,
					-23
				],
				[
					1297.9999999999995,
					-23
				],
				[
					1304.9999999999995,
					-23
				],
				[
					1319.9999999999995,
					-23
				],
				[
					1334.9999999999995,
					-23
				],
				[
					1354.9999999999995,
					-23
				],
				[
					1362.9999999999995,
					-23
				],
				[
					1367.9999999999995,
					-24
				],
				[
					1369.9999999999995,
					-25
				],
				[
					1370.9999999999995,
					-25
				],
				[
					1374.9999999999995,
					-26
				],
				[
					1378.9999999999995,
					-26
				],
				[
					1382.9999999999995,
					-26
				],
				[
					1385.9999999999995,
					-26
				],
				[
					1386.9999999999995,
					-26
				],
				[
					1386.9999999999995,
					-26
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 28,
			"versionNonce": 241585097,
			"isDeleted": false,
			"id": "ZW0fLNA6BMIDo9MstX_LD",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 963.4240024199785,
			"y": 138.13029926657464,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 886768415,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 53,
			"versionNonce": 718008647,
			"isDeleted": false,
			"id": "LIohKY-WAoL7ydeHOvmyA",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -139.57599758002107,
			"y": 188.13029926657453,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 135.9999999999999,
			"height": 6,
			"seed": 598649247,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2,
					-1
				],
				[
					12,
					-2
				],
				[
					22,
					-2
				],
				[
					36,
					-2
				],
				[
					48,
					0
				],
				[
					63,
					1
				],
				[
					77,
					3
				],
				[
					88,
					4
				],
				[
					97,
					4
				],
				[
					99,
					4
				],
				[
					101,
					4
				],
				[
					102,
					4
				],
				[
					103,
					3
				],
				[
					104,
					2
				],
				[
					107,
					1
				],
				[
					110,
					1
				],
				[
					113,
					1
				],
				[
					117,
					1
				],
				[
					119,
					1
				],
				[
					121,
					1
				],
				[
					124,
					1
				],
				[
					126,
					1
				],
				[
					130,
					1
				],
				[
					132.9999999999999,
					1
				],
				[
					134.9999999999999,
					1
				],
				[
					135.9999999999999,
					1
				],
				[
					135.9999999999999,
					1
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 62,
			"versionNonce": 756804265,
			"isDeleted": false,
			"id": "a9e80LahGLNOqrdItBf07",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 59.17400241997882,
			"y": 187.13029926657453,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 46,
			"height": 1,
			"seed": 1997961535,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-1,
					0
				],
				[
					-3,
					0
				],
				[
					-4,
					0
				],
				[
					-6,
					0
				],
				[
					-11,
					0
				],
				[
					-13,
					0
				],
				[
					-16,
					0
				],
				[
					-20,
					0
				],
				[
					-21,
					0
				],
				[
					-23,
					0
				],
				[
					-24,
					0
				],
				[
					-25,
					0
				],
				[
					-27,
					0
				],
				[
					-31,
					0
				],
				[
					-33,
					0
				],
				[
					-36,
					0
				],
				[
					-37,
					0
				],
				[
					-38,
					0
				],
				[
					-39,
					0
				],
				[
					-40,
					0
				],
				[
					-41,
					0
				],
				[
					-42,
					0
				],
				[
					-43,
					-1
				],
				[
					-44,
					-1
				],
				[
					-45,
					-1
				],
				[
					-46,
					-1
				],
				[
					-46,
					-1
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 45,
			"versionNonce": 854339687,
			"isDeleted": false,
			"id": "jwp8pN0swHT_tgkKmeqxZ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 135.42400241997882,
			"y": 194.13029926657453,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 56,
			"height": 0,
			"seed": 334472415,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-7,
					0
				],
				[
					-12,
					0
				],
				[
					-16,
					0
				],
				[
					-20,
					0
				],
				[
					-24,
					0
				],
				[
					-28,
					0
				],
				[
					-31,
					0
				],
				[
					-37,
					0
				],
				[
					-40,
					0
				],
				[
					-43,
					0
				],
				[
					-45,
					0
				],
				[
					-47,
					0
				],
				[
					-49,
					0
				],
				[
					-50,
					0
				],
				[
					-52,
					0
				],
				[
					-53,
					0
				],
				[
					-54,
					0
				],
				[
					-56,
					0
				],
				[
					-56,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 73,
			"versionNonce": 1702538633,
			"isDeleted": false,
			"id": "iBC1bph9Up1Q2oI6-7HFb",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -141.57599758002107,
			"y": 290.1302992665745,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 247.9999999999999,
			"height": 5,
			"seed": 850353023,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2,
					0
				],
				[
					3,
					-1
				],
				[
					8,
					-1
				],
				[
					13,
					-2
				],
				[
					18,
					-3
				],
				[
					22,
					-3
				],
				[
					26,
					-3
				],
				[
					30,
					-3
				],
				[
					36,
					-3
				],
				[
					42,
					-3
				],
				[
					48,
					-3
				],
				[
					53,
					-3
				],
				[
					60,
					-3
				],
				[
					65,
					-3
				],
				[
					71,
					-3
				],
				[
					81,
					-3
				],
				[
					88,
					-3
				],
				[
					96,
					-4
				],
				[
					105,
					-4
				],
				[
					114,
					-4
				],
				[
					120,
					-4
				],
				[
					127,
					-4
				],
				[
					133.9999999999999,
					-4
				],
				[
					143.9999999999999,
					-4
				],
				[
					149.9999999999999,
					-4
				],
				[
					156.9999999999999,
					-4
				],
				[
					163.9999999999999,
					-4
				],
				[
					168.9999999999999,
					-4
				],
				[
					175.9999999999999,
					-4
				],
				[
					184.9999999999999,
					-4
				],
				[
					191.9999999999999,
					-4
				],
				[
					197.9999999999999,
					-4
				],
				[
					202.9999999999999,
					-4
				],
				[
					207.9999999999999,
					-4
				],
				[
					211.9999999999999,
					-4
				],
				[
					215.9999999999999,
					-4
				],
				[
					221.9999999999999,
					-4
				],
				[
					225.9999999999999,
					-4
				],
				[
					229.9999999999999,
					-4
				],
				[
					233.9999999999999,
					-4
				],
				[
					236.9999999999999,
					-4
				],
				[
					238.9999999999999,
					-4
				],
				[
					239.9999999999999,
					-5
				],
				[
					240.9999999999999,
					-5
				],
				[
					245.9999999999999,
					-5
				],
				[
					247.9999999999999,
					-5
				],
				[
					247.9999999999999,
					-5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 32,
			"versionNonce": 1190628231,
			"isDeleted": false,
			"id": "qteMDo92",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -141.5963938504177,
			"y": 206.39311977939485,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 40,
			"height": 25,
			"seed": 207113489,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "长度",
			"rawText": "长度",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "长度",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "text",
			"version": 61,
			"versionNonce": 1857950825,
			"isDeleted": false,
			"id": "SZmvT1a6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -15.346393850417712,
			"y": 198.89311977939485,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 88.97990417480469,
			"height": 25,
			"seed": 1343469023,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "type ipv4",
			"rawText": "type ipv4",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "type ipv4",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "text",
			"version": 54,
			"versionNonce": 1932165799,
			"isDeleted": false,
			"id": "wTyEWpQf",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 95.90360614958229,
			"y": 200.14311977939485,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 40,
			"height": 25,
			"seed": 1273135967,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "保留",
			"rawText": "保留",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "保留",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "text",
			"version": 158,
			"versionNonce": 212967241,
			"isDeleted": false,
			"id": "eAewVCi9",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -107.84639385041771,
			"y": 295.14311977939485,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 194.25990295410156,
			"height": 25,
			"seed": 1656647615,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "ip 地址 172.20.3.105",
			"rawText": "ip 地址 172.20.3.105",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ip 地址 172.20.3.105",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "freedraw",
			"version": 65,
			"versionNonce": 137467335,
			"isDeleted": false,
			"id": "Ccw9PjIgcWYvU7ZG9XStc",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 0.9036061495822878,
			"y": 385.14311977939485,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 118.75,
			"height": 3.75,
			"seed": 1295697969,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					-1.25
				],
				[
					7.5,
					-2.5
				],
				[
					13.75,
					-2.5
				],
				[
					21.25,
					-3.75
				],
				[
					28.75,
					-3.75
				],
				[
					35,
					-3.75
				],
				[
					45,
					-3.75
				],
				[
					51.25,
					-3.75
				],
				[
					58.75,
					-3.75
				],
				[
					66.25,
					-3.75
				],
				[
					71.25,
					-3.75
				],
				[
					75,
					-3.75
				],
				[
					78.75,
					-3.75
				],
				[
					81.25,
					-3.75
				],
				[
					82.5,
					-3.75
				],
				[
					83.75,
					-2.5
				],
				[
					86.25,
					-2.5
				],
				[
					87.5,
					-2.5
				],
				[
					90,
					-2.5
				],
				[
					91.25,
					-2.5
				],
				[
					93.75,
					-1.25
				],
				[
					95,
					-1.25
				],
				[
					96.25,
					-1.25
				],
				[
					98.75,
					-1.25
				],
				[
					100,
					-1.25
				],
				[
					102.5,
					-1.25
				],
				[
					103.75,
					-1.25
				],
				[
					105,
					-1.25
				],
				[
					106.25,
					0
				],
				[
					107.5,
					0
				],
				[
					108.75,
					0
				],
				[
					110,
					0
				],
				[
					111.25,
					0
				],
				[
					112.5,
					0
				],
				[
					113.75,
					0
				],
				[
					115,
					0
				],
				[
					116.25,
					0
				],
				[
					117.5,
					0
				],
				[
					118.75,
					0
				],
				[
					118.75,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 66,
			"versionNonce": 2108739113,
			"isDeleted": false,
			"id": "pTr2X7VF",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -12.846393850417712,
			"y": 400.14311977939485,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 135.67996215820312,
			"height": 25,
			"seed": 220977951,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "端口号 30509",
			"rawText": "端口号 30509",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "端口号 30509",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "rectangle",
			"version": 58,
			"versionNonce": 220808423,
			"isDeleted": false,
			"id": "LKcBjdXedPNHFXr_jVWrU",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -229.76772252174692,
			"y": 706.1815813178562,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 574.0000000000002,
			"height": 94,
			"seed": 1654918463,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 44,
			"versionNonce": 682041609,
			"isDeleted": false,
			"id": "OauwLNGe",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -157.76772252174692,
			"y": 728.1815813178562,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 423.2159118652344,
			"height": 45,
			"seed": 1069780671,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "subscribe 发送的SD 报文",
			"rawText": "subscribe 发送的SD 报文",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "subscribe 发送的SD 报文",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "freedraw",
			"version": 157,
			"versionNonce": 1906184199,
			"isDeleted": false,
			"id": "UFaxQRXi_8BfB50A2cKzS",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -159.87819228052336,
			"y": -1067.065570425669,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 2.866273793743408,
			"height": 0,
			"seed": 1257270609,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.866273793743408,
					0
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "rectangle",
			"version": 106,
			"versionNonce": 185604073,
			"isDeleted": false,
			"id": "NHY34oDVJofB7FMtN7PxJ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -287.76772252174703,
			"y": -1122.3184186821445,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 574.0000000000002,
			"height": 94,
			"seed": 1039702833,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 98,
			"versionNonce": 2139911975,
			"isDeleted": false,
			"id": "484V0ODu",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -215.76772252174703,
			"y": -1100.3184186821445,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 365.32794189453125,
			"height": 45,
			"seed": 1602227473,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "notify 发送的SD 报文",
			"rawText": "notify 发送的SD 报文",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "notify 发送的SD 报文",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "freedraw",
			"version": 156,
			"versionNonce": 1727476425,
			"isDeleted": false,
			"id": "s6JB72C-crRV7UXhICwG6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1939.0106966083665,
			"y": -1008.4544593145577,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 2.866273793743408,
			"height": 0,
			"seed": 1733322673,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.866273793743408,
					0
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "rectangle",
			"version": 124,
			"versionNonce": 224459335,
			"isDeleted": false,
			"id": "qFEYh8cKtKaJVUy3Y_HsY",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1811.121166367143,
			"y": -1063.7073075710332,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 825.1111111111111,
			"height": 94,
			"seed": 355092881,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 125,
			"versionNonce": 821555625,
			"isDeleted": false,
			"id": "fuiZ1YJt",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1883.121166367143,
			"y": -1041.7073075710332,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 653.3280029296875,
			"height": 45,
			"seed": 355266417,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "板子 发送的SD 报文，退测就是notify的",
			"rawText": "板子 发送的SD 报文，退测就是notify的",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "板子 发送的SD 报文，退测就是notify的",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 1878530407,
			"isDeleted": false,
			"id": "yl8lUszY",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": -894.9674363311608,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 272.25,
			"height": 78.13496979042901,
			"seed": 1011334207,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "ffff8100",
			"rawText": "ffff8100",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ffff8100",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 1044239497,
			"isDeleted": false,
			"id": "1xqsVllJ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": -799.4691399206365,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 343.5625,
			"height": 78.13496979042901,
			"seed": 1515219761,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "00000030",
			"rawText": "00000030",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000030",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 748573831,
			"isDeleted": false,
			"id": "9fZodvWZ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": -703.9708435101121,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 317.9375,
			"height": 78.13496979042901,
			"seed": 27515999,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "00000001",
			"rawText": "00000001",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000001",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 847534953,
			"isDeleted": false,
			"id": "sWC3Sp49",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": -608.4725470995877,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 293.375,
			"height": 78.13496979042901,
			"seed": 1079893265,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "01010200",
			"rawText": "01010200",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "01010200",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 1796221863,
			"isDeleted": false,
			"id": "LXLDoZVb",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": -512.9742506890634,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 332.375,
			"height": 78.13496979042901,
			"seed": 1657206911,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "c0000000",
			"rawText": "c0000000",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "c0000000",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 773260873,
			"isDeleted": false,
			"id": "MRqS736a",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": -417.47595427853906,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 317.9375,
			"height": 78.13496979042901,
			"seed": 1268912881,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "00000010",
			"rawText": "00000010",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00000010",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 662314695,
			"isDeleted": false,
			"id": "8DVTAsXS",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": -321.97765786801426,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 314.9375,
			"height": 78.13496979042901,
			"seed": 1165070495,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "06000010",
			"rawText": "06000010",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "06000010",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 1003574569,
			"isDeleted": false,
			"id": "7UpzE76S",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": -226.47936145748997,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 282.5625,
			"height": 78.13496979042901,
			"seed": 816090321,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.507975832343206,
			"fontFamily": 1,
			"text": "90150001",
			"rawText": "90150001",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "90150001",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 611888615,
			"isDeleted": false,
			"id": "ZueW8TAE",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": -130.98106504696557,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 317.5,
			"height": 78.13496979042901,
			"seed": 55846079,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "01000003",
			"rawText": "01000003",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "01000003",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 2132723721,
			"isDeleted": false,
			"id": "bcjKtQSQ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": -35.48276863644128,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 308.5625,
			"height": 78.13496979042901,
			"seed": 654101169,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "00007001",
			"rawText": "00007001",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00007001",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 488134919,
			"isDeleted": false,
			"id": "UEm5jdtS",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": 60.015527774083125,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 332.375,
			"height": 78.13496979042901,
			"seed": 1812935903,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "0000000c",
			"rawText": "0000000c",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "0000000c",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 570089193,
			"isDeleted": false,
			"id": "cyyQG7df",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": 155.51382418460753,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 336.0625,
			"height": 78.13496979042901,
			"seed": 122834065,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "00900400",
			"rawText": "00900400",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "00900400",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 919969831,
			"isDeleted": false,
			"id": "t0te6rL2",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": 251.01212059513182,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 292.1875,
			"height": 78.13496979042901,
			"seed": 120799487,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234321,
			"fontFamily": 1,
			"text": "ac140307",
			"rawText": "ac140307",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ac140307",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "text",
			"version": 208,
			"versionNonce": 49355209,
			"isDeleted": false,
			"id": "aXw5xsA9",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3020.379685625662,
			"y": 346.5104170056561,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 264.875,
			"height": 78.13496979042903,
			"seed": 693932657,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 62.50797583234322,
			"fontFamily": 1,
			"text": "001176c6",
			"rawText": "001176c6",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "001176c6",
			"lineHeight": 1.25,
			"baseline": 55
		},
		{
			"type": "freedraw",
			"version": 110,
			"versionNonce": 865928007,
			"isDeleted": false,
			"id": "5YDEDIh9mMFGYCB9ouSOH",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3351.808257054233,
			"y": -294.9674363311608,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 74.28571428571468,
			"height": 322.8571428571429,
			"seed": 122891857,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.857142857143117,
					-2.8571428571428896
				],
				[
					14.285714285714675,
					-2.8571428571428896
				],
				[
					20,
					-2.8571428571428896
				],
				[
					25.71428571428578,
					-2.8571428571428896
				],
				[
					25.71428571428578,
					2.8571428571428896
				],
				[
					25.71428571428578,
					5.714285714285552
				],
				[
					25.71428571428578,
					8.571428571428442
				],
				[
					25.71428571428578,
					17.14285714285711
				],
				[
					25.71428571428578,
					20
				],
				[
					22.857142857143117,
					25.714285714285552
				],
				[
					22.857142857143117,
					28.57142857142844
				],
				[
					22.857142857143117,
					34.28571428571422
				],
				[
					22.857142857143117,
					37.14285714285711
				],
				[
					22.857142857143117,
					42.85714285714289
				],
				[
					22.857142857143117,
					51.42857142857133
				],
				[
					22.857142857143117,
					54.28571428571422
				],
				[
					22.857142857143117,
					60
				],
				[
					22.857142857143117,
					68.57142857142844
				],
				[
					22.857142857143117,
					74.28571428571422
				],
				[
					22.857142857143117,
					82.85714285714289
				],
				[
					22.857142857143117,
					91.42857142857133
				],
				[
					25.71428571428578,
					102.85714285714289
				],
				[
					25.71428571428578,
					117.14285714285711
				],
				[
					25.71428571428578,
					125.71428571428578
				],
				[
					28.571428571428896,
					137.1428571428571
				],
				[
					31.42857142857156,
					142.8571428571429
				],
				[
					34.285714285714675,
					157.1428571428571
				],
				[
					37.14285714285734,
					162.8571428571429
				],
				[
					40,
					171.42857142857133
				],
				[
					42.85714285714312,
					174.28571428571422
				],
				[
					45.71428571428578,
					177.1428571428571
				],
				[
					48.571428571428896,
					177.1428571428571
				],
				[
					48.571428571428896,
					174.28571428571422
				],
				[
					51.42857142857156,
					174.28571428571422
				],
				[
					54.285714285714675,
					174.28571428571422
				],
				[
					57.14285714285734,
					174.28571428571422
				],
				[
					57.14285714285734,
					171.42857142857133
				],
				[
					57.14285714285734,
					168.57142857142867
				],
				[
					60.000000000000455,
					168.57142857142867
				],
				[
					60.000000000000455,
					171.42857142857133
				],
				[
					60.000000000000455,
					174.28571428571422
				],
				[
					60.000000000000455,
					180
				],
				[
					60.000000000000455,
					185.71428571428578
				],
				[
					60.000000000000455,
					188.57142857142867
				],
				[
					62.85714285714312,
					194.28571428571422
				],
				[
					62.85714285714312,
					197.1428571428571
				],
				[
					62.85714285714312,
					205.71428571428578
				],
				[
					62.85714285714312,
					208.57142857142867
				],
				[
					62.85714285714312,
					214.28571428571422
				],
				[
					65.71428571428578,
					217.1428571428571
				],
				[
					65.71428571428578,
					222.8571428571429
				],
				[
					65.71428571428578,
					225.71428571428578
				],
				[
					65.71428571428578,
					234.28571428571422
				],
				[
					68.5714285714289,
					237.1428571428571
				],
				[
					68.5714285714289,
					242.8571428571429
				],
				[
					71.42857142857156,
					245.71428571428578
				],
				[
					71.42857142857156,
					251.42857142857156
				],
				[
					71.42857142857156,
					257.1428571428571
				],
				[
					71.42857142857156,
					262.8571428571429
				],
				[
					74.28571428571468,
					271.42857142857156
				],
				[
					74.28571428571468,
					277.1428571428571
				],
				[
					74.28571428571468,
					280
				],
				[
					74.28571428571468,
					282.8571428571429
				],
				[
					74.28571428571468,
					285.7142857142858
				],
				[
					74.28571428571468,
					288.57142857142867
				],
				[
					74.28571428571468,
					291.42857142857156
				],
				[
					74.28571428571468,
					294.2857142857142
				],
				[
					74.28571428571468,
					297.1428571428571
				],
				[
					74.28571428571468,
					300
				],
				[
					71.42857142857156,
					300
				],
				[
					71.42857142857156,
					302.8571428571429
				],
				[
					65.71428571428578,
					302.8571428571429
				],
				[
					65.71428571428578,
					305.7142857142858
				],
				[
					62.85714285714312,
					308.57142857142867
				],
				[
					60.000000000000455,
					308.57142857142867
				],
				[
					54.285714285714675,
					311.42857142857156
				],
				[
					51.42857142857156,
					311.42857142857156
				],
				[
					48.571428571428896,
					314.2857142857142
				],
				[
					42.85714285714312,
					314.2857142857142
				],
				[
					40,
					317.1428571428571
				],
				[
					37.14285714285734,
					320
				],
				[
					34.285714285714675,
					320
				],
				[
					31.42857142857156,
					320
				],
				[
					34.285714285714675,
					320
				],
				[
					34.285714285714675,
					320
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 42,
			"versionNonce": 589101225,
			"isDeleted": false,
			"id": "n0C1_RtclOhZQUXv1GQkp",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3028.95111419709,
			"y": -249.25315061687525,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 74.28571428571422,
			"height": 0,
			"seed": 546451999,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.8571428571426623,
					0
				],
				[
					11.428571428571104,
					0
				],
				[
					20,
					0
				],
				[
					28.57142857142844,
					0
				],
				[
					34.28571428571422,
					0
				],
				[
					37.14285714285688,
					0
				],
				[
					40,
					0
				],
				[
					45.71428571428578,
					0
				],
				[
					48.57142857142844,
					0
				],
				[
					54.28571428571422,
					0
				],
				[
					60,
					0
				],
				[
					62.85714285714266,
					0
				],
				[
					65.71428571428578,
					0
				],
				[
					68.57142857142844,
					0
				],
				[
					71.42857142857156,
					0
				],
				[
					74.28571428571422,
					0
				],
				[
					74.28571428571422,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 92,
			"versionNonce": 1674248807,
			"isDeleted": false,
			"id": "9Xsf8ZNl",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3586.093971339947,
			"y": -309.253150616875,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 108,
			"height": 45,
			"seed": 544737777,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "事件组",
			"rawText": "事件组",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "事件组",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "text",
			"version": 173,
			"versionNonce": 1412037513,
			"isDeleted": false,
			"id": "yMj4777c",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2944.6653999113755,
			"y": -251.39600775973213,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 161.84877014160156,
			"height": 45.64684443798515,
			"seed": 1926294033,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"fontSize": 36.51747555038812,
			"fontFamily": 1,
			"text": "Subscribe",
			"rawText": "Subscribe",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Subscribe",
			"lineHeight": 1.25,
			"baseline": 31
		},
		{
			"type": "freedraw",
			"version": 45,
			"versionNonce": 1479286151,
			"isDeleted": false,
			"id": "v6HqSj_wjjvmAEiwAVoGD",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3037.8796856256613,
			"y": -158.89600775973236,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 127.5,
			"height": 2.5,
			"seed": 1948733215,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					12.5,
					0
				],
				[
					27.5,
					0
				],
				[
					50,
					0
				],
				[
					60,
					0
				],
				[
					67.5,
					-2.5
				],
				[
					70,
					-2.5
				],
				[
					72.5,
					-2.5
				],
				[
					77.5,
					-2.5
				],
				[
					87.5,
					-2.5
				],
				[
					95,
					-2.5
				],
				[
					102.5,
					-2.5
				],
				[
					105,
					-2.5
				],
				[
					107.5,
					-2.5
				],
				[
					110,
					-2.5
				],
				[
					115,
					-2.5
				],
				[
					117.5,
					-2.5
				],
				[
					120,
					-2.5
				],
				[
					122.5,
					-2.5
				],
				[
					127.5,
					-2.5
				],
				[
					127.5,
					-2.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 50,
			"versionNonce": 643015273,
			"isDeleted": false,
			"id": "Kjmwhy-uVTDO53dJ3aeuu",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3175.3796856256613,
			"y": -148.89600775973236,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 150.00000000000045,
			"height": 12.5,
			"seed": 329054719,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					-2.5
				],
				[
					5,
					-2.5
				],
				[
					12.5,
					-7.5
				],
				[
					22.5,
					-10
				],
				[
					25,
					-10
				],
				[
					30.000000000000455,
					-10
				],
				[
					35.000000000000455,
					-12.5
				],
				[
					40.000000000000455,
					-12.5
				],
				[
					57.500000000000455,
					-12.5
				],
				[
					65.00000000000045,
					-12.5
				],
				[
					72.50000000000045,
					-12.5
				],
				[
					77.50000000000045,
					-12.5
				],
				[
					85.00000000000045,
					-12.5
				],
				[
					90.00000000000045,
					-12.5
				],
				[
					97.50000000000045,
					-12.5
				],
				[
					107.50000000000045,
					-12.5
				],
				[
					120.00000000000045,
					-12.5
				],
				[
					125.00000000000045,
					-12.5
				],
				[
					130.00000000000045,
					-12.5
				],
				[
					135.00000000000045,
					-12.5
				],
				[
					137.50000000000045,
					-12.5
				],
				[
					140.00000000000045,
					-12.5
				],
				[
					145.00000000000045,
					-12.5
				],
				[
					147.50000000000045,
					-12.5
				],
				[
					150.00000000000045,
					-12.5
				],
				[
					150.00000000000045,
					-12.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 36,
			"versionNonce": 1409078439,
			"isDeleted": false,
			"id": "sHxmkToMxSOB9VIKawDG-",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3025.3796856256613,
			"y": -61.396007759732356,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 60,
			"height": 5,
			"seed": 1684829567,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.5
				],
				[
					5,
					5
				],
				[
					12.5,
					5
				],
				[
					20,
					5
				],
				[
					30,
					5
				],
				[
					35,
					5
				],
				[
					42.5,
					5
				],
				[
					50,
					5
				],
				[
					55,
					5
				],
				[
					57.5,
					5
				],
				[
					60,
					5
				],
				[
					60,
					5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 71,
			"versionNonce": 375745865,
			"isDeleted": false,
			"id": "JsxUfJupP4HRvfKgFK4Fa",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3107.8796856256613,
			"y": -43.896007759732356,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 215.00000000000045,
			"height": 22.5,
			"seed": 1979620159,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					-5
				],
				[
					5,
					-5
				],
				[
					10,
					-7.5
				],
				[
					15,
					-12.5
				],
				[
					22.5,
					-15
				],
				[
					30,
					-17.5
				],
				[
					37.5,
					-20
				],
				[
					40,
					-22.5
				],
				[
					42.5,
					-22.5
				],
				[
					47.5,
					-22.5
				],
				[
					52.5,
					-22.5
				],
				[
					57.5,
					-22.5
				],
				[
					65,
					-22.5
				],
				[
					70,
					-22.5
				],
				[
					75,
					-22.5
				],
				[
					80,
					-22.5
				],
				[
					85,
					-22.5
				],
				[
					87.5,
					-20
				],
				[
					92.5,
					-20
				],
				[
					100.00000000000045,
					-20
				],
				[
					102.50000000000045,
					-20
				],
				[
					107.50000000000045,
					-20
				],
				[
					117.50000000000045,
					-20
				],
				[
					122.50000000000045,
					-20
				],
				[
					130.00000000000045,
					-20
				],
				[
					135.00000000000045,
					-20
				],
				[
					142.50000000000045,
					-20
				],
				[
					150.00000000000045,
					-20
				],
				[
					155.00000000000045,
					-20
				],
				[
					160.00000000000045,
					-20
				],
				[
					162.50000000000045,
					-20
				],
				[
					165.00000000000045,
					-20
				],
				[
					170.00000000000045,
					-20
				],
				[
					177.50000000000045,
					-20
				],
				[
					180.00000000000045,
					-20
				],
				[
					185.00000000000045,
					-20
				],
				[
					187.50000000000045,
					-20
				],
				[
					190.00000000000045,
					-20
				],
				[
					195.00000000000045,
					-20
				],
				[
					197.50000000000045,
					-20
				],
				[
					200.00000000000045,
					-20
				],
				[
					205.00000000000045,
					-20
				],
				[
					207.50000000000045,
					-20
				],
				[
					210.00000000000045,
					-20
				],
				[
					212.50000000000045,
					-20
				],
				[
					215.00000000000045,
					-20
				],
				[
					215.00000000000045,
					-20
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 32,
			"versionNonce": 2129242055,
			"isDeleted": false,
			"id": "GXNtNY4hx-2xeT1JVdLnZ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3017.8796856256613,
			"y": 36.103992240267644,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 30,
			"height": 0,
			"seed": 841253215,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					5,
					0
				],
				[
					15,
					0
				],
				[
					20,
					0
				],
				[
					25,
					0
				],
				[
					27.5,
					0
				],
				[
					30,
					0
				],
				[
					30,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 32,
			"versionNonce": 2075843625,
			"isDeleted": false,
			"id": "e0RMGm7ihp4TrKtVEXezh",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3097.8796856256613,
			"y": 41.103992240267644,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 12.5,
			"height": 2.5,
			"seed": 1347823263,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-2.5,
					0
				],
				[
					-2.5,
					-2.5
				],
				[
					-5,
					-2.5
				],
				[
					-7.5,
					-2.5
				],
				[
					-10,
					-2.5
				],
				[
					-12.5,
					-2.5
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 30,
			"versionNonce": 1460606695,
			"isDeleted": false,
			"id": "r6WYsApZWcBkS3Iaqd1Ta",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3072.8796856256613,
			"y": 31.103992240267644,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 15,
			"height": 5,
			"seed": 1765161951,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					7.5,
					2.5
				],
				[
					10,
					2.5
				],
				[
					15,
					5
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 68,
			"versionNonce": 910126857,
			"isDeleted": false,
			"id": "_Ak2k8LKMACLcX3VpG5ce",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3187.8796856256613,
			"y": 33.603992240267644,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 152.5,
			"height": 5,
			"seed": 1936010463,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-2.5,
					0
				],
				[
					-5,
					0
				],
				[
					-7.5,
					0
				],
				[
					-10,
					0
				],
				[
					-10,
					-2.5
				],
				[
					-12.5,
					-2.5
				],
				[
					-15,
					-2.5
				],
				[
					-17.5,
					-2.5
				],
				[
					-20,
					-2.5
				],
				[
					-22.5,
					-2.5
				],
				[
					-25,
					-2.5
				],
				[
					-27.5,
					-2.5
				],
				[
					-30,
					-2.5
				],
				[
					-32.5,
					-2.5
				],
				[
					-35,
					-2.5
				],
				[
					-37.5,
					-2.5
				],
				[
					-40,
					-2.5
				],
				[
					-45,
					-2.5
				],
				[
					-57.5,
					-2.5
				],
				[
					-67.5,
					-2.5
				],
				[
					-75,
					-2.5
				],
				[
					-85,
					-2.5
				],
				[
					-92.5,
					-2.5
				],
				[
					-97.5,
					0
				],
				[
					-102.5,
					0
				],
				[
					-105,
					0
				],
				[
					-107.5,
					0
				],
				[
					-110,
					0
				],
				[
					-112.5,
					0
				],
				[
					-115,
					0
				],
				[
					-115,
					2.5
				],
				[
					-120,
					2.5
				],
				[
					-122.5,
					2.5
				],
				[
					-127.5,
					2.5
				],
				[
					-130,
					2.5
				],
				[
					-135,
					2.5
				],
				[
					-137.5,
					2.5
				],
				[
					-140,
					2.5
				],
				[
					-142.5,
					2.5
				],
				[
					-145,
					2.5
				],
				[
					-147.5,
					2.5
				],
				[
					-150,
					2.5
				],
				[
					-152.5,
					2.5
				],
				[
					-152.5,
					2.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 47,
			"versionNonce": 1660527111,
			"isDeleted": false,
			"id": "6mdVxQ3rKTYGTfgPnMZBL",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3185.3796856256613,
			"y": 53.603992240267644,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 142.50000000000045,
			"height": 22.5,
			"seed": 75214495,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299017,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					7.5,
					0
				],
				[
					17.500000000000455,
					-5
				],
				[
					30.000000000000455,
					-7.5
				],
				[
					42.500000000000455,
					-7.5
				],
				[
					57.500000000000455,
					-10
				],
				[
					70.00000000000045,
					-15
				],
				[
					80.00000000000045,
					-15
				],
				[
					90.00000000000045,
					-15
				],
				[
					97.50000000000045,
					-17.5
				],
				[
					102.50000000000045,
					-20
				],
				[
					110.00000000000045,
					-20
				],
				[
					112.50000000000045,
					-20
				],
				[
					117.50000000000045,
					-22.5
				],
				[
					122.50000000000045,
					-22.5
				],
				[
					125.00000000000045,
					-22.5
				],
				[
					127.50000000000045,
					-22.5
				],
				[
					130.00000000000045,
					-22.5
				],
				[
					132.50000000000045,
					-22.5
				],
				[
					137.50000000000045,
					-22.5
				],
				[
					140.00000000000045,
					-22.5
				],
				[
					142.50000000000045,
					-22.5
				],
				[
					142.50000000000045,
					-22.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 43,
			"versionNonce": 477013481,
			"isDeleted": false,
			"id": "O7rdEX-rY3kTi4hpwVr2l",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3332.8796856256618,
			"y": 11.103992240267644,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 212.5,
			"height": 37.5,
			"seed": 567031679,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					2.5
				],
				[
					15,
					10
				],
				[
					42.5,
					20
				],
				[
					70,
					22.5
				],
				[
					95,
					25
				],
				[
					110,
					27.5
				],
				[
					125,
					30
				],
				[
					132.5,
					32.5
				],
				[
					140,
					32.5
				],
				[
					147.5,
					32.5
				],
				[
					155,
					32.5
				],
				[
					162.5,
					32.5
				],
				[
					170,
					32.5
				],
				[
					180,
					35
				],
				[
					187.5,
					35
				],
				[
					200,
					37.5
				],
				[
					202.5,
					37.5
				],
				[
					210,
					37.5
				],
				[
					212.5,
					37.5
				],
				[
					212.5,
					37.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 39,
			"versionNonce": 598067495,
			"isDeleted": false,
			"id": "nl37BnEbxkk84rcEH8miw",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3537.8796856256618,
			"y": 18.603992240267644,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 52.5,
			"height": 57.5,
			"seed": 364015167,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					5
				],
				[
					5,
					15
				],
				[
					12.5,
					27.5
				],
				[
					17.5,
					32.5
				],
				[
					20,
					37.5
				],
				[
					22.5,
					40
				],
				[
					25,
					42.5
				],
				[
					27.5,
					42.5
				],
				[
					25,
					42.5
				],
				[
					17.5,
					45
				],
				[
					10,
					47.5
				],
				[
					-5,
					50
				],
				[
					-17.5,
					55
				],
				[
					-22.5,
					57.5
				],
				[
					-25,
					57.5
				],
				[
					-25,
					57.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 42,
			"versionNonce": 693371081,
			"isDeleted": false,
			"id": "E182yYPi",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3610.3796856256618,
			"y": 53.603992240267644,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 266.3279113769531,
			"height": 45,
			"seed": 558419071,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "Event Group id",
			"rawText": "Event Group id",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Event Group id",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "freedraw",
			"version": 77,
			"versionNonce": 1182796871,
			"isDeleted": false,
			"id": "iZBOZd63iE_ta54bShoU5",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3382.8342310802072,
			"y": 97.92217405844951,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 85.45454545454504,
			"height": 330.9090909090911,
			"seed": 1128211985,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					3.6363636363635123,
					0
				],
				[
					10.909090909090992,
					1.8181818181818699
				],
				[
					16.363636363636033,
					5.454545454545496
				],
				[
					18.181818181818016,
					7.272727272727252
				],
				[
					20,
					7.272727272727252
				],
				[
					21.818181818181984,
					12.727272727272748
				],
				[
					21.818181818181984,
					20
				],
				[
					21.818181818181984,
					25.454545454545496
				],
				[
					20,
					34.54545454545462
				],
				[
					18.181818181818016,
					40
				],
				[
					18.181818181818016,
					47.272727272727366
				],
				[
					18.181818181818016,
					56.363636363636374
				],
				[
					18.181818181818016,
					63.636363636363626
				],
				[
					21.818181818181984,
					74.54545454545462
				],
				[
					23.636363636363512,
					81.81818181818187
				],
				[
					25.45454545454504,
					85.4545454545455
				],
				[
					29.09090909090901,
					89.09090909090912
				],
				[
					32.72727272727252,
					92.72727272727286
				],
				[
					36.36363636363603,
					92.72727272727286
				],
				[
					40,
					96.36363636363637
				],
				[
					41.81818181818198,
					96.36363636363637
				],
				[
					45.45454545454504,
					96.36363636363637
				],
				[
					43.63636363636351,
					100.00000000000011
				],
				[
					36.36363636363603,
					105.45454545454561
				],
				[
					25.45454545454504,
					112.72727272727286
				],
				[
					18.181818181818016,
					123.63636363636363
				],
				[
					12.72727272727252,
					130.90909090909088
				],
				[
					7.272727272727025,
					138.18181818181836
				],
				[
					5.454545454545041,
					145.4545454545456
				],
				[
					3.6363636363635123,
					152.72727272727286
				],
				[
					1.8181818181815288,
					165.4545454545456
				],
				[
					1.8181818181815288,
					176.36363636363637
				],
				[
					0,
					185.4545454545456
				],
				[
					-3.636363636363967,
					200.0000000000001
				],
				[
					-7.272727272727479,
					212.72727272727286
				],
				[
					-12.727272727272975,
					225.4545454545456
				],
				[
					-16.363636363636488,
					238.18181818181836
				],
				[
					-20,
					252.72727272727286
				],
				[
					-23.636363636363967,
					265.4545454545456
				],
				[
					-25.45454545454595,
					276.3636363636364
				],
				[
					-27.27272727272748,
					283.63636363636385
				],
				[
					-27.27272727272748,
					287.27272727272737
				],
				[
					-30.90909090909099,
					292.72727272727286
				],
				[
					-30.90909090909099,
					300.0000000000001
				],
				[
					-34.54545454545496,
					307.27272727272737
				],
				[
					-36.36363636363649,
					310.9090909090911
				],
				[
					-38.18181818181847,
					314.5454545454546
				],
				[
					-38.18181818181847,
					320.0000000000001
				],
				[
					-38.18181818181847,
					321.81818181818187
				],
				[
					-40,
					325.4545454545456
				],
				[
					-40,
					327.27272727272737
				],
				[
					-40,
					329.0909090909091
				],
				[
					-40,
					330.9090909090911
				],
				[
					-40,
					330.9090909090911
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 107,
			"versionNonce": 1787494313,
			"isDeleted": false,
			"id": "MPieT_t8mqaRFoSnC5Z3r",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3028.2887765347523,
			"y": 316.10399224026787,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 278.18181818181847,
			"height": 7.272727272727252,
			"seed": 768147217,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					5.454545454545496,
					1.8181818181817562
				],
				[
					10.909090909090992,
					5.4545454545452685
				],
				[
					14.545454545454959,
					5.4545454545452685
				],
				[
					21.818181818181984,
					5.4545454545452685
				],
				[
					25.454545454545496,
					5.4545454545452685
				],
				[
					30.90909090909099,
					5.4545454545452685
				],
				[
					40,
					5.4545454545452685
				],
				[
					43.63636363636397,
					5.4545454545452685
				],
				[
					52.727272727272975,
					3.6363636363635123
				],
				[
					60,
					1.8181818181817562
				],
				[
					67.27272727272748,
					1.8181818181817562
				],
				[
					74.54545454545496,
					1.8181818181817562
				],
				[
					78.18181818181802,
					1.8181818181817562
				],
				[
					81.81818181818198,
					1.8181818181817562
				],
				[
					85.4545454545455,
					1.8181818181817562
				],
				[
					87.27272727272748,
					0
				],
				[
					89.09090909090901,
					0
				],
				[
					90.90909090909099,
					0
				],
				[
					94.54545454545496,
					0
				],
				[
					96.36363636363649,
					0
				],
				[
					98.18181818181802,
					0
				],
				[
					100,
					0
				],
				[
					101.81818181818198,
					0
				],
				[
					103.63636363636397,
					0
				],
				[
					105.45454545454595,
					0
				],
				[
					107.27272727272748,
					0
				],
				[
					109.09090909090901,
					0
				],
				[
					110.90909090909099,
					0
				],
				[
					112.72727272727298,
					0
				],
				[
					114.54545454545496,
					0
				],
				[
					118.18181818181802,
					0
				],
				[
					121.81818181818198,
					0
				],
				[
					123.63636363636397,
					0
				],
				[
					125.45454545454595,
					0
				],
				[
					127.27272727272748,
					0
				],
				[
					129.090909090909,
					0
				],
				[
					132.72727272727298,
					0
				],
				[
					134.54545454545496,
					0
				],
				[
					136.3636363636365,
					0
				],
				[
					140,
					0
				],
				[
					141.81818181818198,
					0
				],
				[
					143.63636363636397,
					0
				],
				[
					147.27272727272748,
					0
				],
				[
					150.909090909091,
					0
				],
				[
					154.54545454545496,
					0
				],
				[
					156.3636363636365,
					0
				],
				[
					160,
					0
				],
				[
					161.81818181818198,
					0
				],
				[
					163.63636363636397,
					0
				],
				[
					167.27272727272748,
					0
				],
				[
					169.090909090909,
					0
				],
				[
					172.72727272727298,
					0
				],
				[
					174.54545454545496,
					0
				],
				[
					176.3636363636365,
					0
				],
				[
					178.18181818181847,
					0
				],
				[
					181.81818181818198,
					0
				],
				[
					183.63636363636397,
					0
				],
				[
					185.45454545454595,
					0
				],
				[
					187.27272727272748,
					0
				],
				[
					189.090909090909,
					0
				],
				[
					190.909090909091,
					0
				],
				[
					192.72727272727298,
					0
				],
				[
					194.54545454545496,
					0
				],
				[
					198.18181818181847,
					0
				],
				[
					200,
					0
				],
				[
					201.81818181818198,
					0
				],
				[
					205.45454545454595,
					0
				],
				[
					207.27272727272748,
					0
				],
				[
					209.090909090909,
					0
				],
				[
					210.909090909091,
					0
				],
				[
					212.72727272727298,
					0
				],
				[
					212.72727272727298,
					-1.8181818181819835
				],
				[
					214.54545454545496,
					-1.8181818181819835
				],
				[
					221.81818181818198,
					-1.8181818181819835
				],
				[
					225.45454545454595,
					-1.8181818181819835
				],
				[
					240,
					0
				],
				[
					247.27272727272748,
					0
				],
				[
					256.3636363636365,
					0
				],
				[
					265.45454545454595,
					0
				],
				[
					270.909090909091,
					0
				],
				[
					274.54545454545496,
					0
				],
				[
					276.3636363636365,
					0
				],
				[
					278.18181818181847,
					0
				],
				[
					278.18181818181847,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 105,
			"versionNonce": 392489831,
			"isDeleted": false,
			"id": "0qk0J0Z4",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3026.470594716571,
			"y": -1011.1687350324598,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 481.9679870605469,
			"height": 45,
			"seed": 1556064479,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "这里应该是一个SD的订阅报文",
			"rawText": "这里应该是一个SD的订阅报文",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "这里应该是一个SD的订阅报文",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "rectangle",
			"version": 51,
			"versionNonce": 775889545,
			"isDeleted": false,
			"id": "65uU3hKAA4I_OpLH5JgSr",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2979.1978674438433,
			"y": -1027.532371396096,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 665.454545454546,
			"height": 85.4545454545455,
			"seed": 1807810815,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 144,
			"versionNonce": 849405575,
			"isDeleted": false,
			"id": "FZ4i8Bje",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3474.6524128983892,
			"y": 275.42217405844985,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 687.81591796875,
			"height": 90,
			"seed": 209178225,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "表示发出此报文的source地址，172.20.3.7\n目的地址是172.20.3.4",
			"rawText": "表示发出此报文的source地址，172.20.3.7\n目的地址是172.20.3.4",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "表示发出此报文的source地址，172.20.3.7\n目的地址是172.20.3.4",
			"lineHeight": 1.25,
			"baseline": 77
		},
		{
			"type": "text",
			"version": 73,
			"versionNonce": 1898703209,
			"isDeleted": false,
			"id": "AIsMWF9t",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3618.2015697310862,
			"y": -416.56458999472807,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 375.71478271484375,
			"height": 45,
			"seed": 19571,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": "[[任务看板.canvas]]",
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "📍[[任务看板.canvas]]",
			"rawText": "[[任务看板.canvas]]",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "📍[[任务看板.canvas]]",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "text",
			"version": 678,
			"versionNonce": 1995472295,
			"isDeleted": false,
			"id": "hLtAgYx5",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1747.6639350838327,
			"y": 1278.0424689390748,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 2090.1240234375,
			"height": 315,
			"seed": 123019013,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "现在的问题：没有发送订阅报文， 但是已经  on_available了，说明服务成功解析了SD报文，但是没有发出订阅报文，这是个问题\n\n还有 对方的ARp协议不能使用，导致ping 不通\n    \n\n是因为arp导致的吗？ 程序中是否先发送了 icmp报文 看目标是否通？\n解决思路：搜索底层的程序实现，找问题所在",
			"rawText": "现在的问题：没有发送订阅报文， 但是已经  on_available了，说明服务成功解析了SD报文，但是没有发出订阅报文，这是个问题\n\n还有 对方的ARp协议不能使用，导致ping 不通\n    \n\n是因为arp导致的吗？ 程序中是否先发送了 icmp报文 看目标是否通？\n解决思路：搜索底层的程序实现，找问题所在",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "现在的问题：没有发送订阅报文， 但是已经  on_available了，说明服务成功解析了SD报文，但是没有发出订阅报文，这是个问题\n\n还有 对方的ARp协议不能使用，导致ping 不通\n    \n\n是因为arp导致的吗？ 程序中是否先发送了 icmp报文 看目标是否通？\n解决思路：搜索底层的程序实现，找问题所在",
			"lineHeight": 1.25,
			"baseline": 302
		},
		{
			"type": "embeddable",
			"version": 179,
			"versionNonce": 1511472234,
			"isDeleted": false,
			"id": "fG3xFay1iDP34cogxo3OR",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2636.9973803149524,
			"y": 2529.3756547707803,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"width": 1881.999969482423,
			"height": 840,
			"seed": 551355390,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1704436743959,
			"link": "https://blog.csdn.net/zjfengdou30/article/details/126363121",
			"locked": false,
			"validated": true,
			"scale": [
				1,
				1
			]
		},
		{
			"type": "text",
			"version": 137,
			"versionNonce": 931147975,
			"isDeleted": false,
			"id": "5eVnV173",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2755.4494052289206,
			"y": 2403.2806150398,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 893.447998046875,
			"height": 45,
			"seed": 1909350590,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "这里是  订阅过程的源码详细解释，明天按照这个打 log",
			"rawText": "这里是  订阅过程的源码详细解释，明天按照这个打 log",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "这里是  订阅过程的源码详细解释，明天按照这个打 log",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "embeddable",
			"version": 111,
			"versionNonce": 1666750262,
			"isDeleted": false,
			"id": "lZUhcBFrbL2RFP4M6wksD",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3015.5358358694784,
			"y": 3649.992452446362,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"width": 1037.0261670600742,
			"height": 840,
			"seed": 2058850021,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1704436743959,
			"link": "https://www.cnblogs.com/ouyshy/p/15225302.html",
			"locked": false,
			"validated": true,
			"scale": [
				1,
				1
			]
		},
		{
			"type": "text",
			"version": 42,
			"versionNonce": 770473959,
			"isDeleted": false,
			"id": "OJ9VuPdK",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 5607.241692471817,
			"y": 685.4487782862584,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 343.4039306640625,
			"height": 810,
			"seed": 1623755525,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "ff  ff  81  00 \n00  00  00  40  \n00  00  00  04  \n01  01  02  00  \nc0  00  00  00  \n00  00  00  20  \n06  00  00  10  \n90  15  00  01  \n01  00  00  00 \n 00  00  70  01 \n 06  00  00  10  \n90  15  00  01  \n01  00  00  03  \n00  00  70  01 \n 00  00  00  0c \n 00  09  04  00 \n ac  14  03  02 \n 00  11  9c  40 ",
			"rawText": "ff  ff  81  00 \n00  00  00  40  \n00  00  00  04  \n01  01  02  00  \nc0  00  00  00  \n00  00  00  20  \n06  00  00  10  \n90  15  00  01  \n01  00  00  00 \n 00  00  70  01 \n 06  00  00  10  \n90  15  00  01  \n01  00  00  03  \n00  00  70  01 \n 00  00  00  0c \n 00  09  04  00 \n ac  14  03  02 \n 00  11  9c  40 ",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ff  ff  81  00 \n00  00  00  40  \n00  00  00  04  \n01  01  02  00  \nc0  00  00  00  \n00  00  00  20  \n06  00  00  10  \n90  15  00  01  \n01  00  00  00 \n 00  00  70  01 \n 06  00  00  10  \n90  15  00  01  \n01  00  00  03  \n00  00  70  01 \n 00  00  00  0c \n 00  09  04  00 \n ac  14  03  02 \n 00  11  9c  40 ",
			"lineHeight": 1.25,
			"baseline": 797
		},
		{
			"type": "rectangle",
			"version": 43,
			"versionNonce": 1426658825,
			"isDeleted": false,
			"id": "khv10c75hiBO3IR5dop4a",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 4957.585670410911,
			"y": -1073.2463164512244,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 1137.5,
			"height": 595,
			"seed": 373186689,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false
		},
		{
			"type": "freedraw",
			"version": 38,
			"versionNonce": 742517511,
			"isDeleted": false,
			"id": "5RIabbw46ijeuH4je45XL",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 5315.08567041091,
			"y": -1348.2463164512244,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 22.5,
			"height": 1165.0000000000002,
			"seed": 1785675247,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-2.5,
					0
				],
				[
					-5,
					32.5
				],
				[
					-5,
					85
				],
				[
					-5,
					240
				],
				[
					-5,
					370.0000000000001
				],
				[
					-5,
					520.0000000000001
				],
				[
					-5,
					677.5
				],
				[
					-5,
					827.5
				],
				[
					-5,
					970
				],
				[
					-7.5,
					1055.0000000000002
				],
				[
					-17.5,
					1102.5000000000002
				],
				[
					-20,
					1132.5000000000002
				],
				[
					-22.5,
					1145.0000000000002
				],
				[
					-22.5,
					1155.0000000000002
				],
				[
					-22.5,
					1162.5000000000002
				],
				[
					-22.5,
					1165.0000000000002
				],
				[
					-22.5,
					1165.0000000000002
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 35,
			"versionNonce": 560688361,
			"isDeleted": false,
			"id": "YXAv0BUAym1_B7sjtxpHK",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 5855.08567041091,
			"y": -1313.2463164512244,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 115,
			"height": 1435.0000000000002,
			"seed": 1332752975,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					27.5
				],
				[
					0,
					75
				],
				[
					5,
					152.5
				],
				[
					5,
					315.0000000000001
				],
				[
					-10,
					625
				],
				[
					-35,
					840
				],
				[
					-57.5,
					1037.5000000000002
				],
				[
					-70,
					1202.5000000000002
				],
				[
					-85,
					1337.5000000000002
				],
				[
					-97.5,
					1400.0000000000002
				],
				[
					-107.5,
					1432.5000000000002
				],
				[
					-110,
					1435.0000000000002
				],
				[
					-107.5,
					1435.0000000000002
				],
				[
					-107.5,
					1435.0000000000002
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 25,
			"versionNonce": 251458087,
			"isDeleted": false,
			"id": "RDuFHf0m",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 5035.085670410911,
			"y": -818.2463164512243,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 20.483993530273438,
			"height": 45,
			"seed": 1260008527,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "d",
			"rawText": "d",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "d",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "rectangle",
			"version": 115,
			"versionNonce": 555739081,
			"isDeleted": false,
			"id": "8XyhxKkP2Ala7OghU9U1l",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 6784.555694048426,
			"y": 764.2064013309018,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 636.666666666667,
			"height": 1408.3333333333335,
			"seed": 116312929,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "AZTcnChN"
				}
			],
			"updated": 1704337299018,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 115,
			"versionNonce": 1862931783,
			"isDeleted": false,
			"id": "AZTcnChN",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 6789.7791335829315,
			"y": 1085.8730679975686,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 626.2197875976562,
			"height": 765,
			"seed": 1191940751,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "  aa bb cc dd ee 03 \naa bb cc dd ee 01 \n08 00 45 00\n  00 54\n 45 e5 \n40 00 40 11 \n96 85 \nac 14 03 02 ac 14\n03 04 77 1a 77 1a 00 40 17 fd\nff ff 81 00 00 00\n00 30 00 00 00 26 01 01 02\n00 c0 00 00 00 00 00\n  00 10 06 00 00 10 90 15 00 01\n01 00 00 00 00 00\n70 01 00 00 00 0c 00 09 04\n00 ac 14 03 02 00 11\n  9c 40",
			"rawText": "  aa bb cc dd ee 03 \naa bb cc dd ee 01 \n08 00 45 00\n  00 54\n 45 e5 \n40 00 40 11 \n96 85 \nac 14 03 02 ac 14\n  03 04 77 1a 77 1a 00 40 17 fd ff ff 81 00 00 00\n  00 30 00 00 00 26 01 01 02 00 c0 00 00 00 00 00\n  00 10 06 00 00 10 90 15 00 01 01 00 00 00 00 00\n  70 01 00 00 00 0c 00 09 04 00 ac 14 03 02 00 11\n  9c 40",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "8XyhxKkP2Ala7OghU9U1l",
			"originalText": "  aa bb cc dd ee 03 \naa bb cc dd ee 01 \n08 00 45 00\n  00 54\n 45 e5 \n40 00 40 11 \n96 85 \nac 14 03 02 ac 14\n  03 04 77 1a 77 1a 00 40 17 fd ff ff 81 00 00 00\n  00 30 00 00 00 26 01 01 02 00 c0 00 00 00 00 00\n  00 10 06 00 00 10 90 15 00 01 01 00 00 00 00 00\n  70 01 00 00 00 0c 00 09 04 00 ac 14 03 02 00 11\n  9c 40",
			"lineHeight": 1.25,
			"baseline": 752
		},
		{
			"type": "text",
			"version": 22,
			"versionNonce": 1849820841,
			"isDeleted": false,
			"id": "0TIXiiwW",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 7503.646603139335,
			"y": 1375.0505571750577,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 114.55195617675781,
			"height": 45,
			"seed": 1300943201,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "DC 65",
			"rawText": "DC 65",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "DC 65",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "text",
			"version": 204,
			"versionNonce": 331732071,
			"isDeleted": false,
			"id": "ghotJYdO",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 889.2890930042411,
			"y": 4269.2335165599525,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 422.10162353515625,
			"height": 1054.5932466524355,
			"seed": 1031214897,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 76.69769066563167,
			"fontFamily": 1,
			"text": "FFFF8100\n00000024\n0000004d\n01010200\nc0000000\n00000010\n07000000\n19050001\n01000000\n00000001\n00000000",
			"rawText": "FFFF8100\n00000024\n0000004d\n01010200\nc0000000\n00000010\n07000000\n19050001\n01000000\n00000001\n00000000",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "FFFF8100\n00000024\n0000004d\n01010200\nc0000000\n00000010\n07000000\n19050001\n01000000\n00000001\n00000000",
			"lineHeight": 1.25,
			"baseline": 1026
		},
		{
			"type": "freedraw",
			"version": 18,
			"versionNonce": 1400719753,
			"isDeleted": false,
			"id": "P0E5dCjME52g6Spjykb-K",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 572.2176644328126,
			"y": 4329.590659417095,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 234126751,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 93,
			"versionNonce": 620539783,
			"isDeleted": false,
			"id": "hQMecWNGKP3JBUFFGOZ8K",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 386.21766443281257,
			"y": 4737.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 1972.0000000000002,
			"height": 50,
			"seed": 208712895,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-2
				],
				[
					2,
					-4
				],
				[
					8,
					-6
				],
				[
					16,
					-8
				],
				[
					20,
					-8
				],
				[
					28,
					-12
				],
				[
					36,
					-16
				],
				[
					44,
					-18
				],
				[
					54,
					-20
				],
				[
					76,
					-22
				],
				[
					96,
					-22
				],
				[
					110,
					-22
				],
				[
					132.00000000000006,
					-22
				],
				[
					160.00000000000006,
					-18
				],
				[
					180.00000000000006,
					-16
				],
				[
					204.00000000000006,
					-14
				],
				[
					252.00000000000006,
					-10
				],
				[
					282.00000000000006,
					-6
				],
				[
					316.00000000000006,
					0
				],
				[
					340.00000000000006,
					2
				],
				[
					370.00000000000006,
					2
				],
				[
					386.00000000000006,
					2
				],
				[
					400.00000000000006,
					2
				],
				[
					422.00000000000006,
					2
				],
				[
					444.00000000000006,
					2
				],
				[
					468.00000000000006,
					2
				],
				[
					480.00000000000006,
					2
				],
				[
					486.00000000000006,
					2
				],
				[
					500.00000000000006,
					0
				],
				[
					510.00000000000006,
					-2
				],
				[
					520,
					-4
				],
				[
					534,
					-6
				],
				[
					562,
					-10
				],
				[
					582,
					-10
				],
				[
					604,
					-10
				],
				[
					618,
					-10
				],
				[
					628,
					-10
				],
				[
					650,
					-12
				],
				[
					670,
					-12
				],
				[
					694.0000000000002,
					-12
				],
				[
					740.0000000000002,
					-12
				],
				[
					746.0000000000002,
					-12
				],
				[
					782.0000000000002,
					-12
				],
				[
					804.0000000000002,
					-12
				],
				[
					836.0000000000002,
					-12
				],
				[
					868.0000000000002,
					-12
				],
				[
					908.0000000000002,
					-12
				],
				[
					946.0000000000002,
					-12
				],
				[
					982.0000000000002,
					-12
				],
				[
					1024.0000000000002,
					-12
				],
				[
					1044.0000000000002,
					-12
				],
				[
					1066.0000000000002,
					-12
				],
				[
					1086.0000000000002,
					-12
				],
				[
					1134.0000000000002,
					-10
				],
				[
					1170.0000000000002,
					-4
				],
				[
					1224.0000000000002,
					4
				],
				[
					1256.0000000000002,
					10
				],
				[
					1292.0000000000002,
					12
				],
				[
					1322.0000000000002,
					14
				],
				[
					1350.0000000000002,
					14
				],
				[
					1400.0000000000002,
					16
				],
				[
					1442.0000000000002,
					16
				],
				[
					1486.0000000000002,
					16
				],
				[
					1534.0000000000002,
					18
				],
				[
					1620.0000000000002,
					20
				],
				[
					1644.0000000000002,
					22
				],
				[
					1736.0000000000002,
					28
				],
				[
					1760.0000000000002,
					28
				],
				[
					1858.0000000000002,
					28
				],
				[
					1894.0000000000002,
					28
				],
				[
					1926.0000000000002,
					28
				],
				[
					1952.0000000000002,
					28
				],
				[
					1964.0000000000002,
					26
				],
				[
					1970.0000000000002,
					24
				],
				[
					1972.0000000000002,
					22
				],
				[
					1972.0000000000002,
					20
				],
				[
					1972.0000000000002,
					20
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 24,
			"versionNonce": 973942889,
			"isDeleted": false,
			"id": "JqT5QuHWEZpmQDd9Z2Ew7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1334.2176644328129,
			"y": 4795.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 88,
			"height": 6,
			"seed": 755042975,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					26,
					-2
				],
				[
					46,
					-2
				],
				[
					64,
					-2
				],
				[
					78,
					-4
				],
				[
					86,
					-4
				],
				[
					88,
					-4
				],
				[
					88,
					-6
				],
				[
					88,
					-6
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 62,
			"versionNonce": 485172903,
			"isDeleted": false,
			"id": "a44bAtVN",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1462.2176644328129,
			"y": 4775.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 122.79598999023438,
			"height": 45,
			"seed": 810819551,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "长度 16",
			"rawText": "长度 16",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "长度 16",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "freedraw",
			"version": 29,
			"versionNonce": 1472019273,
			"isDeleted": false,
			"id": "F-KHoBPLP5MjrAKplKIaC",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 892.2176644328126,
			"y": 4907.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 68,
			"height": 6,
			"seed": 2035331583,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					8,
					0
				],
				[
					22,
					-2
				],
				[
					32,
					-6
				],
				[
					38,
					-6
				],
				[
					46,
					-6
				],
				[
					54,
					-6
				],
				[
					56,
					-6
				],
				[
					58,
					-6
				],
				[
					60,
					-6
				],
				[
					62,
					-6
				],
				[
					66,
					-6
				],
				[
					68,
					-6
				],
				[
					68,
					-6
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 45,
			"versionNonce": 2050865607,
			"isDeleted": false,
			"id": "_slQ4KbwHCZyTTseEY5LL",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 896.2176644328126,
			"y": 5011.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 146,
			"height": 6,
			"seed": 596617183,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2,
					0
				],
				[
					20,
					0
				],
				[
					30,
					-2
				],
				[
					36,
					-2
				],
				[
					44,
					-4
				],
				[
					48,
					-4
				],
				[
					52,
					-4
				],
				[
					56,
					-4
				],
				[
					60,
					-4
				],
				[
					62,
					-4
				],
				[
					72,
					-4
				],
				[
					80,
					-4
				],
				[
					88,
					-2
				],
				[
					96,
					0
				],
				[
					100,
					0
				],
				[
					104,
					0
				],
				[
					108,
					0
				],
				[
					112,
					2
				],
				[
					116,
					2
				],
				[
					118,
					2
				],
				[
					120,
					2
				],
				[
					124,
					2
				],
				[
					134,
					2
				],
				[
					138,
					2
				],
				[
					140,
					2
				],
				[
					142,
					2
				],
				[
					144,
					2
				],
				[
					146,
					2
				],
				[
					146,
					2
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 44,
			"versionNonce": 485026345,
			"isDeleted": false,
			"id": "myVIQzW2Z20k9sSajLRqz",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1080.2176644328129,
			"y": 5013.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 158,
			"height": 6,
			"seed": 1419066303,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-2
				],
				[
					8,
					-4
				],
				[
					14,
					-6
				],
				[
					22,
					-6
				],
				[
					40,
					-6
				],
				[
					50,
					-6
				],
				[
					58,
					-4
				],
				[
					70,
					-4
				],
				[
					88,
					-4
				],
				[
					102,
					-4
				],
				[
					112,
					-4
				],
				[
					120,
					-4
				],
				[
					124,
					-4
				],
				[
					126,
					-4
				],
				[
					128,
					-4
				],
				[
					130,
					-4
				],
				[
					132,
					-4
				],
				[
					134,
					-4
				],
				[
					136,
					-4
				],
				[
					140,
					-4
				],
				[
					142,
					-4
				],
				[
					146,
					-4
				],
				[
					148,
					-4
				],
				[
					150,
					-4
				],
				[
					154,
					-4
				],
				[
					156,
					-4
				],
				[
					158,
					-4
				],
				[
					158,
					-4
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 39,
			"versionNonce": 839968999,
			"isDeleted": false,
			"id": "DVRykASzzn6TkLUgTX7ZE",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 874.2176644328126,
			"y": 5107.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 70,
			"height": 10,
			"seed": 426840959,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2,
					0
				],
				[
					4,
					-2
				],
				[
					14,
					-2
				],
				[
					18,
					-4
				],
				[
					26,
					-6
				],
				[
					32,
					-6
				],
				[
					38,
					-6
				],
				[
					40,
					-8
				],
				[
					42,
					-8
				],
				[
					44,
					-8
				],
				[
					48,
					-8
				],
				[
					50,
					-10
				],
				[
					52,
					-10
				],
				[
					54,
					-10
				],
				[
					56,
					-10
				],
				[
					58,
					-10
				],
				[
					60,
					-10
				],
				[
					62,
					-10
				],
				[
					64,
					-10
				],
				[
					66,
					-10
				],
				[
					68,
					-10
				],
				[
					70,
					-10
				],
				[
					70,
					-10
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 56,
			"versionNonce": 1652276489,
			"isDeleted": false,
			"id": "Qk3GiKOPaJuIeKYgJFHm3",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 992.2176644328126,
			"y": 5113.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 288.0000000000002,
			"height": 8,
			"seed": 2081873567,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2,
					-2
				],
				[
					10,
					-2
				],
				[
					24,
					-4
				],
				[
					34,
					-6
				],
				[
					48,
					-6
				],
				[
					60,
					-6
				],
				[
					72.00000000000023,
					-6
				],
				[
					82.00000000000023,
					-8
				],
				[
					88.00000000000023,
					-8
				],
				[
					94.00000000000023,
					-8
				],
				[
					106.00000000000023,
					-8
				],
				[
					114.00000000000023,
					-8
				],
				[
					124.00000000000023,
					-8
				],
				[
					134.00000000000023,
					-8
				],
				[
					146.00000000000023,
					-8
				],
				[
					150.00000000000023,
					-8
				],
				[
					154.00000000000023,
					-8
				],
				[
					174.00000000000023,
					-8
				],
				[
					188.00000000000023,
					-8
				],
				[
					194.00000000000023,
					-8
				],
				[
					202.00000000000023,
					-6
				],
				[
					208.00000000000023,
					-6
				],
				[
					216.00000000000023,
					-6
				],
				[
					222.00000000000023,
					-6
				],
				[
					230.00000000000023,
					-6
				],
				[
					232.00000000000023,
					-6
				],
				[
					238.00000000000023,
					-6
				],
				[
					246.00000000000023,
					-6
				],
				[
					250.00000000000023,
					-6
				],
				[
					256.0000000000002,
					-6
				],
				[
					258.0000000000002,
					-6
				],
				[
					266.0000000000002,
					-4
				],
				[
					270.0000000000002,
					-4
				],
				[
					272.0000000000002,
					-4
				],
				[
					278.0000000000002,
					-4
				],
				[
					282.0000000000002,
					-4
				],
				[
					284.0000000000002,
					-4
				],
				[
					286.0000000000002,
					-4
				],
				[
					288.0000000000002,
					-4
				],
				[
					288.0000000000002,
					-4
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 30,
			"versionNonce": 1643197447,
			"isDeleted": false,
			"id": "rkpjA5Hm4uG71dSOGlVXI",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1220.2176644328129,
			"y": 5211.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 70,
			"height": 2,
			"seed": 960935903,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2,
					0
				],
				[
					16,
					0
				],
				[
					28,
					0
				],
				[
					32,
					0
				],
				[
					46,
					0
				],
				[
					52,
					0
				],
				[
					56,
					0
				],
				[
					60,
					0
				],
				[
					62,
					0
				],
				[
					66,
					0
				],
				[
					68,
					0
				],
				[
					70,
					0
				],
				[
					70,
					-2
				],
				[
					70,
					-2
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 73,
			"versionNonce": 1475425257,
			"isDeleted": false,
			"id": "89OYk7-tqHsGSiO5WjCo0",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 896.2176644328126,
			"y": 5197.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 398.0000000000002,
			"height": 22,
			"seed": 2087426527,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					4,
					-2
				],
				[
					6,
					-2
				],
				[
					20,
					-4
				],
				[
					36,
					-6
				],
				[
					44,
					-6
				],
				[
					58,
					-6
				],
				[
					70,
					-6
				],
				[
					82,
					-6
				],
				[
					86,
					-6
				],
				[
					90,
					-6
				],
				[
					94,
					-6
				],
				[
					102,
					-6
				],
				[
					108,
					-6
				],
				[
					118,
					-6
				],
				[
					130,
					-6
				],
				[
					148,
					-6
				],
				[
					158,
					-4
				],
				[
					166.00000000000023,
					-4
				],
				[
					174.00000000000023,
					-4
				],
				[
					190.00000000000023,
					-4
				],
				[
					200.00000000000023,
					-4
				],
				[
					206.00000000000023,
					-4
				],
				[
					216.00000000000023,
					-4
				],
				[
					228.00000000000023,
					0
				],
				[
					236.00000000000023,
					0
				],
				[
					238.00000000000023,
					0
				],
				[
					248.00000000000023,
					2
				],
				[
					252.00000000000023,
					4
				],
				[
					254.00000000000023,
					4
				],
				[
					258.0000000000002,
					4
				],
				[
					264.0000000000002,
					4
				],
				[
					278.0000000000002,
					8
				],
				[
					286.0000000000002,
					8
				],
				[
					294.0000000000002,
					10
				],
				[
					302.0000000000002,
					12
				],
				[
					310.0000000000002,
					12
				],
				[
					314.0000000000002,
					12
				],
				[
					320.0000000000002,
					14
				],
				[
					326.0000000000002,
					16
				],
				[
					336.0000000000002,
					16
				],
				[
					338.0000000000002,
					16
				],
				[
					342.0000000000002,
					16
				],
				[
					346.0000000000002,
					16
				],
				[
					350.0000000000002,
					16
				],
				[
					352.0000000000002,
					16
				],
				[
					354.0000000000002,
					16
				],
				[
					356.0000000000002,
					16
				],
				[
					358.0000000000002,
					16
				],
				[
					362.0000000000002,
					16
				],
				[
					364.0000000000002,
					16
				],
				[
					366.0000000000002,
					16
				],
				[
					368.0000000000002,
					16
				],
				[
					372.0000000000002,
					14
				],
				[
					376.0000000000002,
					14
				],
				[
					384.0000000000002,
					14
				],
				[
					398.0000000000002,
					14
				],
				[
					398.0000000000002,
					14
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 81,
			"versionNonce": 1104878375,
			"isDeleted": false,
			"id": "uTvVKfwHPu-Ez2Xi6Ni8i",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 322.21766443281257,
			"y": 5201.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 1840.0000000000002,
			"height": 40,
			"seed": 196593983,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2
				],
				[
					2,
					2
				],
				[
					20,
					0
				],
				[
					44,
					0
				],
				[
					66,
					0
				],
				[
					82,
					2
				],
				[
					138,
					8
				],
				[
					194.00000000000006,
					8
				],
				[
					232.00000000000006,
					8
				],
				[
					272.00000000000006,
					8
				],
				[
					306.00000000000006,
					8
				],
				[
					346.00000000000006,
					8
				],
				[
					368.00000000000006,
					8
				],
				[
					390.00000000000006,
					10
				],
				[
					414.00000000000006,
					12
				],
				[
					450.00000000000006,
					14
				],
				[
					462.00000000000006,
					16
				],
				[
					514,
					16
				],
				[
					538,
					16
				],
				[
					576,
					16
				],
				[
					596,
					16
				],
				[
					616,
					18
				],
				[
					636,
					18
				],
				[
					652,
					20
				],
				[
					666,
					20
				],
				[
					680,
					20
				],
				[
					690,
					20
				],
				[
					712,
					20
				],
				[
					730,
					20
				],
				[
					742.0000000000002,
					20
				],
				[
					756.0000000000002,
					20
				],
				[
					778.0000000000002,
					22
				],
				[
					800.0000000000002,
					26
				],
				[
					820.0000000000002,
					26
				],
				[
					838.0000000000002,
					26
				],
				[
					872.0000000000002,
					30
				],
				[
					894.0000000000002,
					30
				],
				[
					912.0000000000002,
					30
				],
				[
					938.0000000000002,
					32
				],
				[
					980.0000000000002,
					32
				],
				[
					992.0000000000002,
					32
				],
				[
					1042.0000000000002,
					32
				],
				[
					1066.0000000000002,
					32
				],
				[
					1092.0000000000002,
					32
				],
				[
					1124.0000000000002,
					32
				],
				[
					1160.0000000000002,
					30
				],
				[
					1178.0000000000002,
					30
				],
				[
					1266.0000000000002,
					30
				],
				[
					1314.0000000000002,
					28
				],
				[
					1368.0000000000002,
					28
				],
				[
					1422.0000000000002,
					28
				],
				[
					1498.0000000000002,
					34
				],
				[
					1542.0000000000002,
					34
				],
				[
					1584.0000000000002,
					34
				],
				[
					1618.0000000000002,
					34
				],
				[
					1672.0000000000002,
					34
				],
				[
					1710.0000000000002,
					38
				],
				[
					1754.0000000000002,
					40
				],
				[
					1790.0000000000002,
					40
				],
				[
					1822.0000000000002,
					40
				],
				[
					1832.0000000000002,
					40
				],
				[
					1838.0000000000002,
					40
				],
				[
					1840.0000000000002,
					40
				],
				[
					1840.0000000000002,
					38
				],
				[
					1840.0000000000002,
					38
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 19,
			"versionNonce": 827641545,
			"isDeleted": false,
			"id": "2ZToOshqC_VzMoV773AMw",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2210.217664432813,
			"y": 5257.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 2,
			"height": 0,
			"seed": 340673951,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2,
					0
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 24,
			"versionNonce": 1446714951,
			"isDeleted": false,
			"id": "k3st6Mlp",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1346.2176644328129,
			"y": 5065.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 205.45199584960938,
			"height": 45,
			"seed": 1759606559,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "TTL 有问题",
			"rawText": "TTL 有问题",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "TTL 有问题",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "text",
			"version": 78,
			"versionNonce": 356650409,
			"isDeleted": false,
			"id": "wyYH4Cud",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1646.2176644328129,
			"y": 5057.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 259.4519958496094,
			"height": 45,
			"seed": 1409637727,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "排除TTL的问题",
			"rawText": "排除TTL的问题",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "排除TTL的问题",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "text",
			"version": 86,
			"versionNonce": 1642970471,
			"isDeleted": false,
			"id": "BA6YTTjo",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 2054.217664432813,
			"y": 5069.590659417095,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 752.327880859375,
			"height": 45,
			"seed": 2057613489,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "因为ttl为0  所以断定是一个 subscribe_nack",
			"rawText": "因为ttl为0  所以断定是一个 subscribe_nack",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "因为ttl为0  所以断定是一个 subscribe_nack",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "text",
			"version": 649,
			"versionNonce": 1256485001,
			"isDeleted": false,
			"id": "NjcaFLmO",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 795.3843310994807,
			"y": 5677.257326083762,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 1582.307861328125,
			"height": 405,
			"seed": 1471973567,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "今日收获：\n    1、解决了由于防火墙导致的收不到组播报文的问题\n    2、查找到返回的ack报文是属于nack类型的，由ttl 和 type字段共同决定\n    3、SD的on_message方法是处理这个的\n\n后续工作：\n    1、查找为什么导致的返回nack，是否跟订阅报文的东西，ttl有关？\n\n    2、从配置文件中找问题，查看vsomeip.json 中的client 中的部分，需要有相关信息的。很重要",
			"rawText": "今日收获：\n    1、解决了由于防火墙导致的收不到组播报文的问题\n    2、查找到返回的ack报文是属于nack类型的，由ttl 和 type字段共同决定\n    3、SD的on_message方法是处理这个的\n\n后续工作：\n    1、查找为什么导致的返回nack，是否跟订阅报文的东西，ttl有关？\n\n    2、从配置文件中找问题，查看vsomeip.json 中的client 中的部分，需要有相关信息的。很重要",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "今日收获：\n    1、解决了由于防火墙导致的收不到组播报文的问题\n    2、查找到返回的ack报文是属于nack类型的，由ttl 和 type字段共同决定\n    3、SD的on_message方法是处理这个的\n\n后续工作：\n    1、查找为什么导致的返回nack，是否跟订阅报文的东西，ttl有关？\n\n    2、从配置文件中找问题，查看vsomeip.json 中的client 中的部分，需要有相关信息的。很重要",
			"lineHeight": 1.25,
			"baseline": 392
		},
		{
			"type": "freedraw",
			"version": 120,
			"versionNonce": 406812807,
			"isDeleted": false,
			"id": "5KkhexfJ67vxXoHv0QPaq",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1011.9240136391633,
			"y": 6010.749389575824,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 1617.142857142857,
			"height": 104.28571428571468,
			"seed": 2055666673,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-11.428571428571445,
					5.714285714286234
				],
				[
					-28.571428571428555,
					11.428571428571558
				],
				[
					-45.714285714285666,
					18.57142857142844
				],
				[
					-68.57142857142856,
					24.285714285714675
				],
				[
					-114.28571428571422,
					34.285714285714675
				],
				[
					-145.71428571428567,
					41.42857142857156
				],
				[
					-164.28571428571422,
					50
				],
				[
					-175.71428571428567,
					58.57142857142844
				],
				[
					-191.42857142857144,
					70
				],
				[
					-198.57142857142856,
					80
				],
				[
					-205.71428571428567,
					85.71428571428623
				],
				[
					-211.42857142857144,
					91.42857142857156
				],
				[
					-217.1428571428571,
					94.28571428571468
				],
				[
					-217.1428571428571,
					95.71428571428623
				],
				[
					-217.1428571428571,
					97.14285714285779
				],
				[
					-209.9999999999999,
					100
				],
				[
					-155.71428571428567,
					104.28571428571468
				],
				[
					-84.28571428571422,
					104.28571428571468
				],
				[
					4.285714285714334,
					104.28571428571468
				],
				[
					105.71428571428567,
					104.28571428571468
				],
				[
					208.57142857142856,
					98.57142857142844
				],
				[
					348.57142857142856,
					84.28571428571468
				],
				[
					441.42857142857144,
					71.42857142857156
				],
				[
					537.142857142857,
					64.28571428571468
				],
				[
					688.5714285714286,
					64.28571428571468
				],
				[
					785.7142857142857,
					64.28571428571468
				],
				[
					871.4285714285714,
					64.28571428571468
				],
				[
					941.4285714285714,
					64.28571428571468
				],
				[
					1015.7142857142857,
					64.28571428571468
				],
				[
					1057.1428571428573,
					64.28571428571468
				],
				[
					1120,
					65.71428571428623
				],
				[
					1141.4285714285716,
					65.71428571428623
				],
				[
					1205.7142857142858,
					65.71428571428623
				],
				[
					1241.428571428571,
					65.71428571428623
				],
				[
					1267.1428571428573,
					65.71428571428623
				],
				[
					1284.2857142857142,
					64.28571428571468
				],
				[
					1302.8571428571427,
					64.28571428571468
				],
				[
					1315.7142857142858,
					64.28571428571468
				],
				[
					1334.2857142857142,
					64.28571428571468
				],
				[
					1350,
					65.71428571428623
				],
				[
					1362.8571428571427,
					68.57142857142844
				],
				[
					1367.1428571428573,
					68.57142857142844
				],
				[
					1368.5714285714284,
					68.57142857142844
				],
				[
					1371.4285714285716,
					68.57142857142844
				],
				[
					1377.1428571428573,
					67.14285714285779
				],
				[
					1380,
					65.71428571428623
				],
				[
					1385.7142857142858,
					62.85714285714312
				],
				[
					1387.1428571428573,
					60
				],
				[
					1390,
					57.14285714285779
				],
				[
					1391.4285714285716,
					54.285714285714675
				],
				[
					1394.2857142857142,
					50
				],
				[
					1395.7142857142858,
					45.714285714286234
				],
				[
					1397.1428571428573,
					44.285714285714675
				],
				[
					1400,
					41.42857142857156
				],
				[
					1400,
					37.14285714285779
				],
				[
					1398.5714285714284,
					35.714285714286234
				],
				[
					1397.1428571428573,
					34.285714285714675
				],
				[
					1395.7142857142858,
					32.85714285714312
				],
				[
					1387.1428571428573,
					27.142857142857792
				],
				[
					1365.7142857142858,
					24.285714285714675
				],
				[
					1331.428571428571,
					21.42857142857156
				],
				[
					1280,
					17.142857142857792
				],
				[
					1214.2857142857142,
					15.714285714286234
				],
				[
					1178.571428571429,
					15.714285714286234
				],
				[
					1151.4285714285716,
					18.57142857142844
				],
				[
					1124.2857142857142,
					21.42857142857156
				],
				[
					1070,
					27.142857142857792
				],
				[
					1032.8571428571427,
					31.42857142857156
				],
				[
					1002.8571428571428,
					35.714285714286234
				],
				[
					982.8571428571428,
					38.57142857142844
				],
				[
					964.2857142857141,
					42.85714285714312
				],
				[
					951.4285714285714,
					47.14285714285779
				],
				[
					934.2857142857141,
					47.14285714285779
				],
				[
					901.4285714285714,
					48.57142857142844
				],
				[
					815.7142857142857,
					48.57142857142844
				],
				[
					745.7142857142857,
					48.57142857142844
				],
				[
					702.8571428571428,
					48.57142857142844
				],
				[
					667.142857142857,
					48.57142857142844
				],
				[
					638.5714285714286,
					48.57142857142844
				],
				[
					622.8571428571428,
					50
				],
				[
					599.9999999999999,
					51.42857142857156
				],
				[
					571.4285714285714,
					51.42857142857156
				],
				[
					514.2857142857143,
					51.42857142857156
				],
				[
					475.71428571428567,
					47.14285714285779
				],
				[
					444.28571428571433,
					45.714285714286234
				],
				[
					422.8571428571428,
					44.285714285714675
				],
				[
					398.57142857142856,
					42.85714285714312
				],
				[
					382.8571428571428,
					42.85714285714312
				],
				[
					369.9999999999999,
					42.85714285714312
				],
				[
					352.8571428571428,
					42.85714285714312
				],
				[
					319.9999999999999,
					38.57142857142844
				],
				[
					295.71428571428567,
					32.85714285714312
				],
				[
					274.2857142857141,
					30
				],
				[
					252.857142857143,
					27.142857142857792
				],
				[
					231.42857142857144,
					24.285714285714675
				],
				[
					201.42857142857144,
					20
				],
				[
					184.28571428571433,
					17.142857142857792
				],
				[
					167.14285714285722,
					17.142857142857792
				],
				[
					139.9999999999999,
					17.142857142857792
				],
				[
					124.28571428571433,
					17.142857142857792
				],
				[
					105.71428571428567,
					14.285714285714675
				],
				[
					85.71428571428567,
					14.285714285714675
				],
				[
					52.857142857143,
					14.285714285714675
				],
				[
					35.714285714285666,
					14.285714285714675
				],
				[
					18.571428571428555,
					14.285714285714675
				],
				[
					8.571428571428555,
					14.285714285714675
				],
				[
					-4.285714285714221,
					14.285714285714675
				],
				[
					-14.28571428571422,
					14.285714285714675
				],
				[
					-25.714285714285666,
					12.857142857143117
				],
				[
					-37.14285714285711,
					12.857142857143117
				],
				[
					-50,
					10
				],
				[
					-51.428571428571445,
					10
				],
				[
					-52.85714285714289,
					10
				],
				[
					-52.85714285714289,
					8.571428571428442
				],
				[
					-52.85714285714289,
					8.571428571428442
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 23,
			"versionNonce": 670529385,
			"isDeleted": false,
			"id": "7Hh1rbhxBk57SrBsNcMdv",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1324.7811564963063,
			"y": 6133.6065324329675,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 642.8571428571427,
			"height": 218.57142857142844,
			"seed": 693999441,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					1.4285714285715585
				],
				[
					8.571428571428442,
					11.428571428571558
				],
				[
					35.71428571428555,
					38.57142857142844
				],
				[
					62.85714285714266,
					62.85714285714312
				],
				[
					89.99999999999977,
					81.42857142857156
				],
				[
					104.28571428571422,
					90
				],
				[
					111.42857142857133,
					91.42857142857156
				],
				[
					114.28571428571422,
					90
				],
				[
					122.85714285714266,
					81.42857142857156
				],
				[
					158.57142857142844,
					61.42857142857156
				],
				[
					277.1428571428569,
					20
				],
				[
					385.71428571428555,
					-14.285714285714675
				],
				[
					495.71428571428555,
					-55.714285714285325
				],
				[
					577.1428571428569,
					-90
				],
				[
					632.8571428571427,
					-121.42857142857156
				],
				[
					642.8571428571427,
					-125.71428571428532
				],
				[
					642.8571428571427,
					-127.14285714285688
				],
				[
					642.8571428571427,
					-127.14285714285688
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 232,
			"versionNonce": 250400679,
			"isDeleted": false,
			"id": "ms7diM9G",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -593.1973853085073,
			"y": 4293.9420127527765,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 324.7146911621094,
			"height": 1321.6810013433233,
			"seed": 147718535,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 58.74137783748103,
			"fontFamily": 1,
			"text": "FFFF8100\n00000040\n00000005\n01010200\nc0000000\n00000020\n06000010\n19050001\n01000000\n00000001\n06000010\n19050001\n01000064\n00000001\n0000000c\n00090400\nac140369\n0011ae26",
			"rawText": "FFFF8100\n00000040\n00000005\n01010200\nc0000000\n00000020\n06000010\n19050001\n01000000\n00000001\n06000010\n19050001\n01000064\n00000001\n0000000c\n00090400\nac140369\n0011ae26",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "FFFF8100\n00000040\n00000005\n01010200\nc0000000\n00000020\n06000010\n19050001\n01000000\n00000001\n06000010\n19050001\n01000064\n00000001\n0000000c\n00090400\nac140369\n0011ae26",
			"lineHeight": 1.25,
			"baseline": 1299
		},
		{
			"type": "freedraw",
			"version": 48,
			"versionNonce": 1053205065,
			"isDeleted": false,
			"id": "SS_QNCXQTFF_uJtPhfZk-",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -687.1973853085069,
			"y": 4640.815028625792,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 756.0000000000002,
			"height": 14,
			"seed": 891106825,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2
				],
				[
					2,
					2
				],
				[
					12,
					2
				],
				[
					26.000000000000114,
					2
				],
				[
					44.000000000000114,
					2
				],
				[
					62.000000000000114,
					4
				],
				[
					88.00000000000011,
					6
				],
				[
					126.00000000000011,
					12
				],
				[
					146.0000000000001,
					14
				],
				[
					168.0000000000001,
					14
				],
				[
					190.0000000000001,
					14
				],
				[
					210.0000000000001,
					14
				],
				[
					236.0000000000001,
					14
				],
				[
					264.0000000000001,
					14
				],
				[
					300.0000000000001,
					14
				],
				[
					350.0000000000001,
					14
				],
				[
					388.0000000000001,
					14
				],
				[
					418.0000000000001,
					14
				],
				[
					452.0000000000001,
					14
				],
				[
					484.0000000000001,
					14
				],
				[
					518.0000000000001,
					14
				],
				[
					550.0000000000002,
					14
				],
				[
					588.0000000000002,
					14
				],
				[
					602.0000000000002,
					14
				],
				[
					618.0000000000002,
					14
				],
				[
					628.0000000000002,
					12
				],
				[
					636.0000000000002,
					12
				],
				[
					644.0000000000002,
					12
				],
				[
					652.0000000000002,
					12
				],
				[
					660.0000000000002,
					12
				],
				[
					668.0000000000002,
					12
				],
				[
					676.0000000000002,
					12
				],
				[
					682.0000000000002,
					12
				],
				[
					692.0000000000002,
					12
				],
				[
					700.0000000000002,
					12
				],
				[
					710.0000000000002,
					12
				],
				[
					720.0000000000002,
					12
				],
				[
					740.0000000000002,
					12
				],
				[
					748.0000000000002,
					12
				],
				[
					752.0000000000002,
					12
				],
				[
					754.0000000000002,
					12
				],
				[
					756.0000000000002,
					12
				],
				[
					756.0000000000002,
					12
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 25,
			"versionNonce": 1881293511,
			"isDeleted": false,
			"id": "FkR1lVpRF74NzFhH-4DwX",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -343.1973853085068,
			"y": 4718.815028625792,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 54,
			"height": 4,
			"seed": 1255846761,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-2,
					2
				],
				[
					4,
					2
				],
				[
					12,
					2
				],
				[
					16,
					2
				],
				[
					18,
					2
				],
				[
					20,
					2
				],
				[
					22,
					2
				],
				[
					24,
					2
				],
				[
					30,
					2
				],
				[
					32,
					2
				],
				[
					36,
					2
				],
				[
					38,
					2
				],
				[
					40,
					2
				],
				[
					42,
					2
				],
				[
					44,
					2
				],
				[
					46,
					2
				],
				[
					48,
					4
				],
				[
					50,
					4
				],
				[
					52,
					4
				],
				[
					52,
					4
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 69,
			"versionNonce": 1278046505,
			"isDeleted": false,
			"id": "OGSMgfL10zHI3hCmF0-mW",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -277.1973853085068,
			"y": 4758.815028625792,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 26,
			"height": 248,
			"seed": 944135849,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2
				],
				[
					0,
					6
				],
				[
					0,
					8
				],
				[
					2,
					14
				],
				[
					2,
					20
				],
				[
					4,
					24
				],
				[
					4,
					28
				],
				[
					6,
					30
				],
				[
					6,
					34
				],
				[
					6,
					40
				],
				[
					6,
					44
				],
				[
					6,
					50
				],
				[
					6,
					58
				],
				[
					8,
					64
				],
				[
					10,
					68
				],
				[
					10,
					76
				],
				[
					12,
					82
				],
				[
					14,
					88
				],
				[
					14,
					98
				],
				[
					16,
					102
				],
				[
					18,
					108
				],
				[
					18,
					114
				],
				[
					20,
					120
				],
				[
					20,
					126
				],
				[
					20,
					130
				],
				[
					22,
					136
				],
				[
					22,
					138
				],
				[
					22,
					142
				],
				[
					22,
					144
				],
				[
					22,
					148
				],
				[
					22,
					150
				],
				[
					22,
					156
				],
				[
					24,
					158
				],
				[
					24,
					162
				],
				[
					26,
					166
				],
				[
					26,
					172
				],
				[
					26,
					176
				],
				[
					26,
					182
				],
				[
					26,
					186
				],
				[
					26,
					188
				],
				[
					26,
					194
				],
				[
					26,
					198
				],
				[
					26,
					200
				],
				[
					26,
					204
				],
				[
					26,
					206
				],
				[
					26,
					208
				],
				[
					26,
					210
				],
				[
					26,
					214
				],
				[
					26,
					216
				],
				[
					24,
					218
				],
				[
					22,
					220
				],
				[
					22,
					224
				],
				[
					20,
					228
				],
				[
					18,
					230
				],
				[
					18,
					232
				],
				[
					16,
					236
				],
				[
					14,
					238
				],
				[
					14,
					240
				],
				[
					14,
					242
				],
				[
					12,
					244
				],
				[
					12,
					246
				],
				[
					12,
					248
				],
				[
					10,
					248
				],
				[
					10,
					248
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 106,
			"versionNonce": 1820086759,
			"isDeleted": false,
			"id": "9L3q6xBvQOWY3Q1a1pKx6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -273.1973853085068,
			"y": 5050.815028625792,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 30,
			"height": 250,
			"seed": 443138153,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2
				],
				[
					0,
					4
				],
				[
					0,
					8
				],
				[
					4,
					14
				],
				[
					8,
					18
				],
				[
					10,
					20
				],
				[
					10,
					24
				],
				[
					12,
					28
				],
				[
					12,
					30
				],
				[
					14,
					34
				],
				[
					16,
					40
				],
				[
					18,
					44
				],
				[
					20,
					48
				],
				[
					22,
					52
				],
				[
					22,
					56
				],
				[
					24,
					60
				],
				[
					24,
					66
				],
				[
					26,
					70
				],
				[
					26,
					74
				],
				[
					26,
					76
				],
				[
					28,
					80
				],
				[
					28,
					82
				],
				[
					30,
					84
				],
				[
					30,
					88
				],
				[
					30,
					90
				],
				[
					30,
					94
				],
				[
					30,
					96
				],
				[
					30,
					98
				],
				[
					30,
					102
				],
				[
					30,
					104
				],
				[
					30,
					106
				],
				[
					30,
					108
				],
				[
					30,
					112
				],
				[
					30,
					114
				],
				[
					30,
					118
				],
				[
					30,
					122
				],
				[
					30,
					126
				],
				[
					30,
					130
				],
				[
					30,
					132
				],
				[
					30,
					136
				],
				[
					30,
					138
				],
				[
					30,
					140
				],
				[
					30,
					144
				],
				[
					30,
					146
				],
				[
					30,
					148
				],
				[
					30,
					150
				],
				[
					30,
					152
				],
				[
					30,
					154
				],
				[
					30,
					156
				],
				[
					30,
					158
				],
				[
					30,
					160
				],
				[
					30,
					162
				],
				[
					30,
					164
				],
				[
					30,
					166
				],
				[
					30,
					168
				],
				[
					30,
					170
				],
				[
					30,
					172
				],
				[
					30,
					174
				],
				[
					30,
					176
				],
				[
					30,
					178
				],
				[
					30,
					180
				],
				[
					30,
					184
				],
				[
					30,
					188
				],
				[
					30,
					192
				],
				[
					30,
					194
				],
				[
					30,
					196
				],
				[
					30,
					198
				],
				[
					30,
					200
				],
				[
					30,
					202
				],
				[
					28,
					204
				],
				[
					28,
					206
				],
				[
					28,
					208
				],
				[
					28,
					210
				],
				[
					28,
					212
				],
				[
					28,
					214
				],
				[
					26,
					218
				],
				[
					26,
					220
				],
				[
					26,
					222
				],
				[
					24,
					222
				],
				[
					24,
					224
				],
				[
					24,
					226
				],
				[
					22,
					226
				],
				[
					22,
					228
				],
				[
					22,
					230
				],
				[
					20,
					230
				],
				[
					20,
					232
				],
				[
					18,
					232
				],
				[
					18,
					234
				],
				[
					18,
					236
				],
				[
					18,
					238
				],
				[
					16,
					238
				],
				[
					16,
					240
				],
				[
					14,
					240
				],
				[
					14,
					242
				],
				[
					14,
					244
				],
				[
					12,
					246
				],
				[
					10,
					246
				],
				[
					10,
					248
				],
				[
					10,
					250
				],
				[
					8,
					250
				],
				[
					8,
					250
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 12,
			"versionNonce": 1704420361,
			"isDeleted": false,
			"id": "cEKXrc6s59PVeopTpP1w_",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -317.1973853085068,
			"y": 5384.815028625792,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 48,
			"height": 2,
			"seed": 1721160841,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					14,
					0
				],
				[
					24,
					-2
				],
				[
					34,
					-2
				],
				[
					42,
					-2
				],
				[
					46,
					-2
				],
				[
					48,
					-2
				],
				[
					48,
					-2
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 49,
			"versionNonce": 1829207303,
			"isDeleted": false,
			"id": "U0CixaRLUexosJyHBwLX4",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -253.1973853085068,
			"y": 5422.815028625792,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 82,
			"height": 164,
			"seed": 1384948329,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2,
					0
				],
				[
					4,
					2
				],
				[
					6,
					6
				],
				[
					10,
					10
				],
				[
					14,
					14
				],
				[
					22,
					26
				],
				[
					28,
					36
				],
				[
					34,
					44
				],
				[
					38,
					50
				],
				[
					40,
					56
				],
				[
					42,
					60
				],
				[
					42,
					64
				],
				[
					42,
					68
				],
				[
					44,
					72
				],
				[
					44,
					76
				],
				[
					44,
					80
				],
				[
					44,
					86
				],
				[
					44,
					96
				],
				[
					44,
					100
				],
				[
					42,
					106
				],
				[
					42,
					112
				],
				[
					38,
					116
				],
				[
					34,
					120
				],
				[
					32,
					124
				],
				[
					30,
					126
				],
				[
					28,
					130
				],
				[
					22,
					134
				],
				[
					20,
					136
				],
				[
					16,
					138
				],
				[
					12,
					142
				],
				[
					10,
					144
				],
				[
					4,
					146
				],
				[
					-4,
					150
				],
				[
					-12,
					154
				],
				[
					-18,
					156
				],
				[
					-24,
					158
				],
				[
					-26,
					158
				],
				[
					-28,
					160
				],
				[
					-32,
					162
				],
				[
					-34,
					162
				],
				[
					-34,
					164
				],
				[
					-36,
					164
				],
				[
					-38,
					164
				],
				[
					-38,
					164
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 22,
			"versionNonce": 1728051945,
			"isDeleted": false,
			"id": "IEStjPurq4tQv3ZFBZ7Ka",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -263.1973853085068,
			"y": 5504.815028625792,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 176.0000000000001,
			"height": 4,
			"seed": 1685136041,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					16,
					0
				],
				[
					40,
					0
				],
				[
					64,
					0
				],
				[
					86,
					0
				],
				[
					108,
					2
				],
				[
					120.00000000000011,
					2
				],
				[
					126.00000000000011,
					2
				],
				[
					134.0000000000001,
					2
				],
				[
					136.0000000000001,
					0
				],
				[
					140.0000000000001,
					0
				],
				[
					148.0000000000001,
					-2
				],
				[
					154.0000000000001,
					-2
				],
				[
					162.0000000000001,
					-2
				],
				[
					172.0000000000001,
					-2
				],
				[
					174.0000000000001,
					-2
				],
				[
					176.0000000000001,
					-2
				],
				[
					176.0000000000001,
					-2
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 32,
			"versionNonce": 88097831,
			"isDeleted": false,
			"id": "TPqansPflEX6OW3gHKLKC",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -475.1973853085068,
			"y": 5612.815028625792,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 150,
			"height": 10,
			"seed": 246785353,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2,
					-2
				],
				[
					6,
					-4
				],
				[
					10,
					-4
				],
				[
					16,
					-8
				],
				[
					30,
					-10
				],
				[
					40,
					-10
				],
				[
					50,
					-10
				],
				[
					60,
					-10
				],
				[
					66,
					-10
				],
				[
					74,
					-10
				],
				[
					82,
					-10
				],
				[
					90,
					-10
				],
				[
					98,
					-10
				],
				[
					106,
					-10
				],
				[
					114,
					-10
				],
				[
					120,
					-10
				],
				[
					128,
					-10
				],
				[
					132,
					-10
				],
				[
					134,
					-10
				],
				[
					136,
					-10
				],
				[
					138,
					-10
				],
				[
					140,
					-10
				],
				[
					142,
					-10
				],
				[
					144,
					-10
				],
				[
					148,
					-10
				],
				[
					150,
					-10
				],
				[
					150,
					-10
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 17,
			"versionNonce": 552777161,
			"isDeleted": false,
			"id": "oiSiw9JiPeCcs5aIcYvKf",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -517.1973853085068,
			"y": 5616.815028625792,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 26,
			"height": 6,
			"seed": 1435520169,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2,
					0
				],
				[
					4,
					0
				],
				[
					6,
					-2
				],
				[
					8,
					-2
				],
				[
					10,
					-2
				],
				[
					12,
					-4
				],
				[
					14,
					-4
				],
				[
					18,
					-6
				],
				[
					22,
					-6
				],
				[
					24,
					-6
				],
				[
					26,
					-6
				],
				[
					26,
					-6
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 111,
			"versionNonce": 622012231,
			"isDeleted": false,
			"id": "YyLIArUo",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -1162.4196075307289,
			"y": 5686.283282594048,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 1530.4320068359375,
			"height": 225,
			"seed": 971652649,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "对于Offer/ StopOfferService、Subscribe/ StopSubscribe和SubscribeAck/ Nack，\n每一组Entries都共用了相同的Type值，但通过TTL字段可以识别究竟是提供服务还是\n停止提供服务，是订阅事件还是取消订阅，是订阅成功应答还是订阅失败应答：当TTL = 0时，\n表示报文对应的服务实例不再有效，此时对应的Type类型分别就是停止提供服务、停止订阅事件\n以及订阅失败应答。",
			"rawText": "对于Offer/ StopOfferService、Subscribe/ StopSubscribe和SubscribeAck/ Nack，\n每一组Entries都共用了相同的Type值，但通过TTL字段可以识别究竟是提供服务还是\n停止提供服务，是订阅事件还是取消订阅，是订阅成功应答还是订阅失败应答：当TTL = 0时，\n表示报文对应的服务实例不再有效，此时对应的Type类型分别就是停止提供服务、停止订阅事件\n以及订阅失败应答。",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "对于Offer/ StopOfferService、Subscribe/ StopSubscribe和SubscribeAck/ Nack，\n每一组Entries都共用了相同的Type值，但通过TTL字段可以识别究竟是提供服务还是\n停止提供服务，是订阅事件还是取消订阅，是订阅成功应答还是订阅失败应答：当TTL = 0时，\n表示报文对应的服务实例不再有效，此时对应的Type类型分别就是停止提供服务、停止订阅事件\n以及订阅失败应答。",
			"lineHeight": 1.25,
			"baseline": 212
		},
		{
			"type": "freedraw",
			"version": 31,
			"versionNonce": 1183519913,
			"isDeleted": false,
			"id": "zlN7k5PtzXmTLgVjmDUbP",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -600.1973853085067,
			"y": 5237.394393705156,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 57.77777777777783,
			"height": 4.444444444444343,
			"seed": 688926953,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.2222222222222854,
					0
				],
				[
					4.444444444444457,
					0
				],
				[
					4.444444444444457,
					-2.222222222221717
				],
				[
					8.888888888888914,
					-2.222222222221717
				],
				[
					11.111111111111086,
					-2.222222222221717
				],
				[
					13.333333333333371,
					-2.222222222221717
				],
				[
					15.555555555555543,
					-2.222222222221717
				],
				[
					17.77777777777783,
					-2.222222222221717
				],
				[
					20,
					-2.222222222221717
				],
				[
					22.222222222222285,
					-2.222222222221717
				],
				[
					22.222222222222285,
					-4.444444444444343
				],
				[
					26.66666666666663,
					-4.444444444444343
				],
				[
					28.888888888888914,
					-4.444444444444343
				],
				[
					31.111111111111086,
					-4.444444444444343
				],
				[
					35.55555555555554,
					-4.444444444444343
				],
				[
					37.77777777777783,
					-4.444444444444343
				],
				[
					40,
					-4.444444444444343
				],
				[
					42.222222222222285,
					-4.444444444444343
				],
				[
					44.44444444444446,
					-4.444444444444343
				],
				[
					46.66666666666663,
					-4.444444444444343
				],
				[
					48.888888888888914,
					-4.444444444444343
				],
				[
					51.111111111111086,
					-4.444444444444343
				],
				[
					53.33333333333337,
					-4.444444444444343
				],
				[
					55.55555555555554,
					-4.444444444444343
				],
				[
					57.77777777777783,
					-4.444444444444343
				],
				[
					57.77777777777783,
					-4.444444444444343
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 18,
			"versionNonce": 182232679,
			"isDeleted": false,
			"id": "xvk_by9suHSyMEPijlmqk",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -582.4196075307289,
			"y": 4926.283282594045,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 42.22222222222217,
			"height": 4.444444444444343,
			"seed": 1912457577,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.2222222222226264
				],
				[
					2.2222222222221717,
					4.444444444444343
				],
				[
					6.666666666666629,
					4.444444444444343
				],
				[
					15.555555555555543,
					4.444444444444343
				],
				[
					24.444444444444457,
					4.444444444444343
				],
				[
					26.66666666666663,
					4.444444444444343
				],
				[
					28.8888888888888,
					4.444444444444343
				],
				[
					31.111111111111086,
					4.444444444444343
				],
				[
					35.55555555555554,
					4.444444444444343
				],
				[
					37.777777777777715,
					4.444444444444343
				],
				[
					40,
					4.444444444444343
				],
				[
					42.22222222222217,
					4.444444444444343
				],
				[
					42.22222222222217,
					4.444444444444343
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 51,
			"versionNonce": 460625801,
			"isDeleted": false,
			"id": "D47T0ck8AcMBAq53sCxJS",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -589.0862741973956,
			"y": 5459.616615927379,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 148.8888888888889,
			"height": 8.888888888889596,
			"seed": 816992393,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.2222222222222854,
					-2.2222222222226264
				],
				[
					4.444444444444457,
					-2.2222222222226264
				],
				[
					8.888888888888914,
					-4.444444444444343
				],
				[
					11.1111111111112,
					-4.444444444444343
				],
				[
					13.333333333333371,
					-4.444444444444343
				],
				[
					15.555555555555543,
					-6.66666666666697
				],
				[
					17.77777777777783,
					-6.66666666666697
				],
				[
					20,
					-8.888888888889596
				],
				[
					24.444444444444457,
					-8.888888888889596
				],
				[
					26.666666666666742,
					-8.888888888889596
				],
				[
					31.1111111111112,
					-8.888888888889596
				],
				[
					33.33333333333337,
					-8.888888888889596
				],
				[
					40,
					-8.888888888889596
				],
				[
					44.44444444444446,
					-8.888888888889596
				],
				[
					48.888888888888914,
					-8.888888888889596
				],
				[
					55.55555555555554,
					-6.66666666666697
				],
				[
					62.222222222222285,
					-6.66666666666697
				],
				[
					66.66666666666674,
					-6.66666666666697
				],
				[
					68.88888888888891,
					-6.66666666666697
				],
				[
					71.1111111111112,
					-6.66666666666697
				],
				[
					75.55555555555554,
					-6.66666666666697
				],
				[
					80,
					-6.66666666666697
				],
				[
					82.22222222222229,
					-6.66666666666697
				],
				[
					86.66666666666674,
					-6.66666666666697
				],
				[
					88.88888888888891,
					-6.66666666666697
				],
				[
					95.55555555555554,
					-6.66666666666697
				],
				[
					97.77777777777783,
					-6.66666666666697
				],
				[
					102.22222222222229,
					-6.66666666666697
				],
				[
					104.44444444444446,
					-6.66666666666697
				],
				[
					108.88888888888891,
					-6.66666666666697
				],
				[
					111.1111111111112,
					-6.66666666666697
				],
				[
					113.33333333333337,
					-6.66666666666697
				],
				[
					117.77777777777783,
					-6.66666666666697
				],
				[
					122.22222222222229,
					-6.66666666666697
				],
				[
					126.66666666666674,
					-6.66666666666697
				],
				[
					128.8888888888889,
					-6.66666666666697
				],
				[
					131.1111111111112,
					-6.66666666666697
				],
				[
					133.33333333333337,
					-6.66666666666697
				],
				[
					135.55555555555566,
					-6.66666666666697
				],
				[
					137.77777777777783,
					-6.66666666666697
				],
				[
					140,
					-6.66666666666697
				],
				[
					142.22222222222229,
					-6.66666666666697
				],
				[
					144.44444444444446,
					-6.66666666666697
				],
				[
					146.66666666666674,
					-8.888888888889596
				],
				[
					148.8888888888889,
					-8.888888888889596
				],
				[
					148.8888888888889,
					-8.888888888889596
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 46,
			"versionNonce": 1969832327,
			"isDeleted": false,
			"id": "M33ZBgpWc9IXXtgsHQjf6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -420.1973853085067,
			"y": 5466.283282594046,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 148.8888888888889,
			"height": 11.111111111111313,
			"seed": 1798978185,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-2.2222222222221717,
					0
				],
				[
					2.2222222222222854,
					0
				],
				[
					6.6666666666667425,
					0
				],
				[
					13.333333333333258,
					0
				],
				[
					20,
					0
				],
				[
					28.888888888888914,
					0
				],
				[
					37.77777777777783,
					2.222222222221717
				],
				[
					44.44444444444457,
					2.222222222221717
				],
				[
					51.111111111111086,
					2.222222222221717
				],
				[
					55.55555555555566,
					2.222222222221717
				],
				[
					62.22222222222217,
					2.222222222221717
				],
				[
					66.66666666666674,
					2.222222222221717
				],
				[
					71.11111111111109,
					2.222222222221717
				],
				[
					75.55555555555566,
					2.222222222221717
				],
				[
					77.77777777777783,
					2.222222222221717
				],
				[
					84.44444444444457,
					2.222222222221717
				],
				[
					86.66666666666674,
					2.222222222221717
				],
				[
					91.11111111111109,
					2.222222222221717
				],
				[
					95.55555555555566,
					2.222222222221717
				],
				[
					97.77777777777783,
					2.222222222221717
				],
				[
					102.22222222222217,
					2.222222222221717
				],
				[
					106.66666666666674,
					0
				],
				[
					108.88888888888891,
					0
				],
				[
					113.33333333333326,
					0
				],
				[
					115.55555555555566,
					0
				],
				[
					117.77777777777783,
					0
				],
				[
					120,
					0
				],
				[
					122.22222222222217,
					0
				],
				[
					124.44444444444457,
					0
				],
				[
					126.66666666666674,
					0
				],
				[
					128.8888888888889,
					0
				],
				[
					131.1111111111111,
					0
				],
				[
					133.33333333333326,
					0
				],
				[
					135.55555555555566,
					-2.2222222222226264
				],
				[
					137.77777777777783,
					-2.2222222222226264
				],
				[
					140,
					-4.444444444445253
				],
				[
					142.22222222222217,
					-4.444444444445253
				],
				[
					144.44444444444457,
					-4.444444444445253
				],
				[
					146.66666666666674,
					-6.66666666666697
				],
				[
					146.66666666666674,
					-8.888888888889596
				],
				[
					146.66666666666674,
					-8.888888888889596
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 45,
			"versionNonce": 1642774121,
			"isDeleted": false,
			"id": "WpSW04wFQHB9A6Y0rAgFf",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -355.7529408640621,
			"y": 5450.727727038489,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 6.666666666666515,
			"height": 82.22222222222263,
			"seed": 90906153,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.2222222222226264
				],
				[
					0,
					6.66666666666697
				],
				[
					0,
					11.111111111111313
				],
				[
					2.2222222222221717,
					13.33333333333394
				],
				[
					2.2222222222221717,
					15.555555555556566
				],
				[
					2.2222222222221717,
					17.777777777778283
				],
				[
					2.2222222222221717,
					20
				],
				[
					2.2222222222221717,
					22.222222222222626
				],
				[
					2.2222222222221717,
					24.444444444445253
				],
				[
					2.2222222222221717,
					22.222222222222626
				],
				[
					2.2222222222221717,
					17.777777777778283
				],
				[
					2.2222222222221717,
					15.555555555556566
				],
				[
					2.2222222222221717,
					11.111111111111313
				],
				[
					2.2222222222221717,
					8.888888888889596
				],
				[
					2.2222222222221717,
					6.66666666666697
				],
				[
					4.444444444444343,
					4.444444444445253
				],
				[
					4.444444444444343,
					0
				],
				[
					6.666666666666515,
					-4.444444444443434
				],
				[
					6.666666666666515,
					-6.66666666666606
				],
				[
					6.666666666666515,
					-8.888888888888687
				],
				[
					6.666666666666515,
					-11.111111111110404
				],
				[
					6.666666666666515,
					-13.33333333333303
				],
				[
					6.666666666666515,
					-15.555555555554747
				],
				[
					6.666666666666515,
					-20
				],
				[
					6.666666666666515,
					-22.222222222221717
				],
				[
					6.666666666666515,
					-24.444444444443434
				],
				[
					6.666666666666515,
					-26.66666666666606
				],
				[
					6.666666666666515,
					-28.888888888888687
				],
				[
					6.666666666666515,
					-31.111111111110404
				],
				[
					6.666666666666515,
					-33.33333333333303
				],
				[
					6.666666666666515,
					-37.777777777777374
				],
				[
					6.666666666666515,
					-42.22222222222172
				],
				[
					6.666666666666515,
					-44.444444444443434
				],
				[
					6.666666666666515,
					-46.66666666666606
				],
				[
					6.666666666666515,
					-48.88888888888869
				],
				[
					6.666666666666515,
					-51.111111111110404
				],
				[
					6.666666666666515,
					-53.33333333333303
				],
				[
					6.666666666666515,
					-55.55555555555475
				],
				[
					6.666666666666515,
					-57.777777777777374
				],
				[
					6.666666666666515,
					-57.777777777777374
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 68,
			"versionNonce": 368408743,
			"isDeleted": false,
			"id": "AgiO-vyPVAG-IKA2KhlTn",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -84.64182975295103,
			"y": 5315.172171482935,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 624.4444444444446,
			"height": 20,
			"seed": 1540770537,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-4.444444444444571,
					0
				],
				[
					-22.22222222222217,
					0
				],
				[
					-51.111111111111086,
					2.222222222221717
				],
				[
					-75.55555555555566,
					2.222222222221717
				],
				[
					-95.55555555555566,
					2.222222222221717
				],
				[
					-113.33333333333348,
					2.222222222221717
				],
				[
					-128.8888888888889,
					2.222222222221717
				],
				[
					-142.22222222222217,
					2.222222222221717
				],
				[
					-151.1111111111111,
					2.222222222221717
				],
				[
					-157.77777777777783,
					2.222222222221717
				],
				[
					-164.44444444444457,
					2.222222222221717
				],
				[
					-168.8888888888889,
					2.222222222221717
				],
				[
					-173.33333333333348,
					4.444444444444343
				],
				[
					-177.77777777777783,
					4.444444444444343
				],
				[
					-182.22222222222217,
					6.66666666666606
				],
				[
					-186.66666666666674,
					6.66666666666606
				],
				[
					-188.8888888888889,
					6.66666666666606
				],
				[
					-195.55555555555566,
					6.66666666666606
				],
				[
					-200,
					6.66666666666606
				],
				[
					-204.44444444444457,
					6.66666666666606
				],
				[
					-211.1111111111111,
					6.66666666666606
				],
				[
					-213.33333333333348,
					6.66666666666606
				],
				[
					-217.77777777777783,
					6.66666666666606
				],
				[
					-224.44444444444457,
					6.66666666666606
				],
				[
					-240,
					6.66666666666606
				],
				[
					-244.44444444444457,
					6.66666666666606
				],
				[
					-257.7777777777778,
					6.66666666666606
				],
				[
					-271.1111111111111,
					6.66666666666606
				],
				[
					-280,
					2.222222222221717
				],
				[
					-288.8888888888889,
					2.222222222221717
				],
				[
					-300,
					2.222222222221717
				],
				[
					-313.3333333333335,
					0
				],
				[
					-322.2222222222224,
					-2.2222222222226264
				],
				[
					-331.1111111111112,
					-2.2222222222226264
				],
				[
					-344.44444444444457,
					-2.2222222222226264
				],
				[
					-351.1111111111112,
					-2.2222222222226264
				],
				[
					-362.2222222222223,
					-2.2222222222226264
				],
				[
					-368.8888888888889,
					-2.2222222222226264
				],
				[
					-382.2222222222223,
					-2.2222222222226264
				],
				[
					-393.33333333333337,
					-4.444444444445253
				],
				[
					-402.2222222222223,
					-4.444444444445253
				],
				[
					-411.1111111111112,
					-4.444444444445253
				],
				[
					-422.2222222222223,
					-4.444444444445253
				],
				[
					-431.1111111111112,
					-4.444444444445253
				],
				[
					-440.0000000000001,
					-4.444444444445253
				],
				[
					-453.33333333333337,
					-4.444444444445253
				],
				[
					-460.0000000000001,
					-4.444444444445253
				],
				[
					-468.888888888889,
					-4.444444444445253
				],
				[
					-480.0000000000001,
					-4.444444444445253
				],
				[
					-488.888888888889,
					-4.444444444445253
				],
				[
					-502.2222222222223,
					-6.66666666666697
				],
				[
					-513.3333333333334,
					-6.66666666666697
				],
				[
					-524.4444444444446,
					-8.888888888888687
				],
				[
					-542.2222222222223,
					-8.888888888888687
				],
				[
					-562.2222222222223,
					-8.888888888888687
				],
				[
					-577.7777777777778,
					-8.888888888888687
				],
				[
					-595.5555555555557,
					-8.888888888888687
				],
				[
					-608.888888888889,
					-11.111111111111313
				],
				[
					-615.5555555555557,
					-11.111111111111313
				],
				[
					-620.0000000000001,
					-13.33333333333394
				],
				[
					-622.2222222222223,
					-13.33333333333394
				],
				[
					-624.4444444444446,
					-13.33333333333394
				],
				[
					-624.4444444444446,
					-13.33333333333394
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 51,
			"versionNonce": 146344265,
			"isDeleted": false,
			"id": "m4kklmJHJL9sTropie9Pk",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -217.9751630862845,
			"y": 5024.061060371823,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 435.55555555555554,
			"height": 15.555555555555657,
			"seed": 1269972425,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-2.2222222222221717,
					0
				],
				[
					-4.444444444444343,
					0
				],
				[
					-15.55555555555543,
					0
				],
				[
					-24.444444444444343,
					0
				],
				[
					-40,
					-2.2222222222226264
				],
				[
					-55.55555555555543,
					-4.444444444444343
				],
				[
					-68.88888888888891,
					-6.66666666666697
				],
				[
					-80,
					-8.888888888888687
				],
				[
					-95.55555555555543,
					-11.111111111111313
				],
				[
					-108.88888888888891,
					-13.33333333333394
				],
				[
					-126.66666666666652,
					-15.555555555555657
				],
				[
					-142.22222222222217,
					-15.555555555555657
				],
				[
					-157.7777777777776,
					-15.555555555555657
				],
				[
					-168.8888888888889,
					-15.555555555555657
				],
				[
					-177.7777777777776,
					-15.555555555555657
				],
				[
					-186.66666666666652,
					-15.555555555555657
				],
				[
					-195.55555555555543,
					-15.555555555555657
				],
				[
					-204.44444444444434,
					-15.555555555555657
				],
				[
					-208.8888888888888,
					-15.555555555555657
				],
				[
					-217.77777777777771,
					-15.555555555555657
				],
				[
					-226.66666666666663,
					-15.555555555555657
				],
				[
					-235.55555555555543,
					-15.555555555555657
				],
				[
					-244.44444444444434,
					-13.33333333333394
				],
				[
					-259.9999999999999,
					-11.111111111111313
				],
				[
					-266.66666666666663,
					-11.111111111111313
				],
				[
					-275.55555555555554,
					-11.111111111111313
				],
				[
					-284.44444444444434,
					-8.888888888888687
				],
				[
					-293.33333333333326,
					-8.888888888888687
				],
				[
					-299.9999999999999,
					-6.66666666666697
				],
				[
					-308.8888888888888,
					-6.66666666666697
				],
				[
					-317.7777777777777,
					-6.66666666666697
				],
				[
					-328.8888888888888,
					-6.66666666666697
				],
				[
					-339.9999999999999,
					-6.66666666666697
				],
				[
					-348.8888888888888,
					-6.66666666666697
				],
				[
					-357.7777777777777,
					-6.66666666666697
				],
				[
					-362.2222222222222,
					-6.66666666666697
				],
				[
					-366.66666666666663,
					-6.66666666666697
				],
				[
					-375.55555555555554,
					-6.66666666666697
				],
				[
					-404.44444444444434,
					-6.66666666666697
				],
				[
					-415.55555555555554,
					-6.66666666666697
				],
				[
					-422.2222222222222,
					-8.888888888888687
				],
				[
					-428.8888888888888,
					-8.888888888888687
				],
				[
					-433.33333333333326,
					-8.888888888888687
				],
				[
					-433.33333333333326,
					-11.111111111111313
				],
				[
					-435.55555555555554,
					-11.111111111111313
				],
				[
					-435.55555555555554,
					-11.111111111111313
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 6,
			"versionNonce": 1110297543,
			"isDeleted": false,
			"id": "IBYjN8t1eeYpPGFyPG2TZ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -724.6418297529511,
			"y": 4908.505504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 148023241,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 6,
			"versionNonce": 423295017,
			"isDeleted": false,
			"id": "63Whkzm_dQtrzlpkGBLSo",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -724.6418297529511,
			"y": 4908.505504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 364376169,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 28,
			"versionNonce": 1714338535,
			"isDeleted": false,
			"id": "i8LCbEo2",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -737.9751630862845,
			"y": 4904.061060371823,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 108,
			"height": 45,
			"seed": 354319625,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "版本号",
			"rawText": "版本号",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "版本号",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "freedraw",
			"version": 47,
			"versionNonce": 1700530953,
			"isDeleted": false,
			"id": "3QI_6bxIJ4AyM4yxsro9v",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -480.1973853085067,
			"y": 4939.616615927379,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 153.33333333333326,
			"height": 2.222222222221717,
			"seed": 1519483207,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299018,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					4.444444444444457,
					0
				],
				[
					8.888888888888914,
					0
				],
				[
					13.333333333333371,
					0
				],
				[
					15.555555555555543,
					0
				],
				[
					26.666666666666742,
					0
				],
				[
					28.888888888888914,
					0
				],
				[
					37.77777777777783,
					0
				],
				[
					40,
					0
				],
				[
					44.44444444444446,
					0
				],
				[
					48.888888888888914,
					0
				],
				[
					53.33333333333337,
					0
				],
				[
					55.55555555555554,
					0
				],
				[
					57.77777777777783,
					0
				],
				[
					62.222222222222285,
					0
				],
				[
					66.66666666666674,
					0
				],
				[
					68.88888888888891,
					0
				],
				[
					75.55555555555566,
					0
				],
				[
					80,
					0
				],
				[
					84.44444444444457,
					0
				],
				[
					88.88888888888891,
					0
				],
				[
					95.55555555555566,
					0
				],
				[
					97.77777777777783,
					0
				],
				[
					102.22222222222217,
					0
				],
				[
					104.44444444444457,
					0
				],
				[
					106.66666666666674,
					0
				],
				[
					111.11111111111109,
					0
				],
				[
					113.33333333333326,
					0
				],
				[
					115.55555555555566,
					0
				],
				[
					120,
					0
				],
				[
					124.44444444444457,
					0
				],
				[
					126.66666666666674,
					0
				],
				[
					131.1111111111111,
					0
				],
				[
					135.55555555555566,
					0
				],
				[
					137.77777777777783,
					0
				],
				[
					142.22222222222217,
					0
				],
				[
					144.44444444444457,
					0
				],
				[
					146.66666666666674,
					0
				],
				[
					148.8888888888889,
					0
				],
				[
					151.1111111111111,
					0
				],
				[
					151.1111111111111,
					2.222222222221717
				],
				[
					153.33333333333326,
					2.222222222221717
				],
				[
					153.33333333333326,
					2.222222222221717
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 50,
			"versionNonce": 914671111,
			"isDeleted": false,
			"id": "Vqh1AITl",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -226.8640519751732,
			"y": 4910.727727038489,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 427.679931640625,
			"height": 45,
			"seed": 1018940103,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "ttl 为0 表示STOP订阅？",
			"rawText": "ttl 为0 表示STOP订阅？",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ttl 为0 表示STOP订阅？",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "text",
			"version": 276,
			"versionNonce": 1972879849,
			"isDeleted": false,
			"id": "CuWJIjNh",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -2146.0307186418404,
			"y": 4316.005504816268,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 372.86151123046875,
			"height": 1187.1222861822112,
			"seed": 1891095113,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"fontSize": 67.83555921041207,
			"fontFamily": 1,
			"text": "FFFF8100\n00000030\n00000001\n01010200\nc0000000\n00000010\n06000010\n19050001\n01000064\n00000001\n0000000c\n00090400\nac140369\n00119c40",
			"rawText": "FFFF8100\n00000030\n00000001\n01010200\nc0000000\n00000010\n06000010\n19050001\n01000064\n00000001\n0000000c\n00090400\nac140369\n00119c40",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "FFFF8100\n00000030\n00000001\n01010200\nc0000000\n00000010\n06000010\n19050001\n01000064\n00000001\n0000000c\n00090400\nac140369\n00119c40",
			"lineHeight": 1.25,
			"baseline": 1161
		},
		{
			"type": "freedraw",
			"version": 67,
			"versionNonce": 573336871,
			"isDeleted": false,
			"id": "oWH1QlAP38T0klC5kRLwE",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -2278.53071864184,
			"y": 4731.005504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 667.5000000000002,
			"height": 15,
			"seed": 1506818473,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					5,
					-2.5
				],
				[
					7.5,
					-2.5
				],
				[
					12.5,
					-2.5
				],
				[
					15,
					-5
				],
				[
					20,
					-7.5
				],
				[
					27.5,
					-7.5
				],
				[
					40,
					-10
				],
				[
					47.5,
					-12.5
				],
				[
					57.5,
					-12.5
				],
				[
					65,
					-12.5
				],
				[
					75,
					-12.5
				],
				[
					80,
					-12.5
				],
				[
					95,
					-12.5
				],
				[
					102.5,
					-12.5
				],
				[
					115,
					-12.5
				],
				[
					127.5,
					-12.5
				],
				[
					140,
					-12.5
				],
				[
					155,
					-12.5
				],
				[
					170,
					-12.5
				],
				[
					192.5,
					-12.5
				],
				[
					210,
					-12.5
				],
				[
					225,
					-12.5
				],
				[
					240,
					-15
				],
				[
					252.5,
					-15
				],
				[
					262.5,
					-15
				],
				[
					270,
					-15
				],
				[
					272.5,
					-15
				],
				[
					277.5,
					-15
				],
				[
					282.5,
					-15
				],
				[
					287.5,
					-12.5
				],
				[
					300,
					-12.5
				],
				[
					310,
					-12.5
				],
				[
					322.5,
					-12.5
				],
				[
					340,
					-12.5
				],
				[
					350,
					-12.5
				],
				[
					365,
					-12.5
				],
				[
					377.5,
					-12.5
				],
				[
					392.5,
					-12.5
				],
				[
					405,
					-12.5
				],
				[
					420,
					-12.5
				],
				[
					435,
					-12.5
				],
				[
					455,
					-12.5
				],
				[
					470,
					-12.5
				],
				[
					482.5,
					-12.5
				],
				[
					500,
					-12.5
				],
				[
					520,
					-12.5
				],
				[
					535,
					-12.5
				],
				[
					547.5,
					-12.5
				],
				[
					565,
					-12.5
				],
				[
					580,
					-15
				],
				[
					595,
					-15
				],
				[
					612.5,
					-15
				],
				[
					627.5,
					-15
				],
				[
					637.5000000000002,
					-15
				],
				[
					650.0000000000002,
					-15
				],
				[
					655.0000000000002,
					-15
				],
				[
					660.0000000000002,
					-15
				],
				[
					665.0000000000002,
					-15
				],
				[
					667.5000000000002,
					-15
				],
				[
					667.5000000000002,
					-12.5
				],
				[
					667.5000000000002,
					-12.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 18,
			"versionNonce": 922328265,
			"isDeleted": false,
			"id": "WIFYhS29HAIu5Fx7SedxM",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -1866.03071864184,
			"y": 4811.005504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 65,
			"height": 0,
			"seed": 280261033,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					7.5,
					0
				],
				[
					15,
					0
				],
				[
					25,
					0
				],
				[
					35,
					0
				],
				[
					40,
					0
				],
				[
					47.5,
					0
				],
				[
					52.5,
					0
				],
				[
					55,
					0
				],
				[
					60,
					0
				],
				[
					62.5,
					0
				],
				[
					65,
					0
				],
				[
					65,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 20,
			"versionNonce": 76689479,
			"isDeleted": false,
			"id": "Ae0wjr7sVr3GkbjspY93N",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -2131.03071864184,
			"y": 4891.005504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 75,
			"height": 2.5,
			"seed": 2107670729,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					5,
					0
				],
				[
					7.5,
					-2.5
				],
				[
					10,
					-2.5
				],
				[
					12.5,
					-2.5
				],
				[
					17.5,
					-2.5
				],
				[
					25,
					-2.5
				],
				[
					32.5,
					-2.5
				],
				[
					37.5,
					-2.5
				],
				[
					45,
					-2.5
				],
				[
					57.5,
					-2.5
				],
				[
					62.5,
					-2.5
				],
				[
					67.5,
					-2.5
				],
				[
					72.5,
					-2.5
				],
				[
					75,
					-2.5
				],
				[
					75,
					-2.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 23,
			"versionNonce": 1763515305,
			"isDeleted": false,
			"id": "XDIRORylTCHWUZgj8Fqk4",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -2131.03071864184,
			"y": 4988.505504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 127.5,
			"height": 5,
			"seed": 1660849577,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					10,
					0
				],
				[
					30,
					2.5
				],
				[
					45,
					2.5
				],
				[
					60,
					5
				],
				[
					72.5,
					5
				],
				[
					82.5,
					5
				],
				[
					92.5,
					5
				],
				[
					100,
					5
				],
				[
					102.5,
					5
				],
				[
					110,
					5
				],
				[
					112.5,
					5
				],
				[
					115,
					5
				],
				[
					120,
					5
				],
				[
					122.5,
					5
				],
				[
					125,
					5
				],
				[
					127.5,
					5
				],
				[
					127.5,
					5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 20,
			"versionNonce": 395480935,
			"isDeleted": false,
			"id": "wiYQLlpvRJmfBLoQeDQ5l",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -1958.53071864184,
			"y": 4986.005504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 147.5,
			"height": 0,
			"seed": 1838022441,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					7.5,
					0
				],
				[
					17.5,
					0
				],
				[
					25,
					0
				],
				[
					37.5,
					0
				],
				[
					57.5,
					0
				],
				[
					80,
					0
				],
				[
					95,
					0
				],
				[
					110,
					0
				],
				[
					117.5,
					0
				],
				[
					127.5,
					0
				],
				[
					137.5,
					0
				],
				[
					140,
					0
				],
				[
					145,
					0
				],
				[
					147.5,
					0
				],
				[
					147.5,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 20,
			"versionNonce": 1278066313,
			"isDeleted": false,
			"id": "nORMNOvJTJ5RLrMA4LKkk",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -2123.53071864184,
			"y": 5068.505504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 57.5,
			"height": 2.5,
			"seed": 1821147145,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					10,
					0
				],
				[
					20,
					0
				],
				[
					32.5,
					0
				],
				[
					35,
					0
				],
				[
					37.5,
					0
				],
				[
					40,
					0
				],
				[
					42.5,
					0
				],
				[
					45,
					-2.5
				],
				[
					47.5,
					-2.5
				],
				[
					50,
					-2.5
				],
				[
					52.5,
					-2.5
				],
				[
					55,
					-2.5
				],
				[
					57.5,
					-2.5
				],
				[
					57.5,
					-2.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 31,
			"versionNonce": 628755079,
			"isDeleted": false,
			"id": "iTp0DUnhSpphq36wZEbxp",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -2003.53071864184,
			"y": 5068.505504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 205,
			"height": 2.5,
			"seed": 1743922409,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					5,
					0
				],
				[
					10,
					-2.5
				],
				[
					15,
					-2.5
				],
				[
					22.5,
					-2.5
				],
				[
					37.5,
					-2.5
				],
				[
					57.5,
					-2.5
				],
				[
					72.5,
					-2.5
				],
				[
					85,
					-2.5
				],
				[
					92.5,
					-2.5
				],
				[
					105,
					-2.5
				],
				[
					117.5,
					-2.5
				],
				[
					122.5,
					-2.5
				],
				[
					132.5,
					-2.5
				],
				[
					140,
					-2.5
				],
				[
					150,
					-2.5
				],
				[
					160,
					-2.5
				],
				[
					170,
					-2.5
				],
				[
					180,
					-2.5
				],
				[
					185,
					-2.5
				],
				[
					190,
					-2.5
				],
				[
					195,
					-2.5
				],
				[
					200,
					-2.5
				],
				[
					202.5,
					-2.5
				],
				[
					205,
					-2.5
				],
				[
					205,
					-2.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 62,
			"versionNonce": 250021225,
			"isDeleted": false,
			"id": "vCzZRgfjAG_BVrlyLpQLV",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -2343.53071864184,
			"y": 5151.005504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 720.0000000000002,
			"height": 10,
			"seed": 665435497,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					7.5,
					-2.5
				],
				[
					15,
					-2.5
				],
				[
					22.5,
					-2.5
				],
				[
					30,
					-2.5
				],
				[
					37.5,
					-2.5
				],
				[
					45,
					-2.5
				],
				[
					57.5,
					-2.5
				],
				[
					72.5,
					-2.5
				],
				[
					90,
					-2.5
				],
				[
					112.5,
					-2.5
				],
				[
					135,
					-2.5
				],
				[
					162.5,
					0
				],
				[
					177.5,
					2.5
				],
				[
					195,
					2.5
				],
				[
					202.5,
					2.5
				],
				[
					215,
					2.5
				],
				[
					225,
					2.5
				],
				[
					240,
					2.5
				],
				[
					255,
					2.5
				],
				[
					285,
					2.5
				],
				[
					310,
					2.5
				],
				[
					325,
					2.5
				],
				[
					340,
					2.5
				],
				[
					355,
					2.5
				],
				[
					362.5,
					2.5
				],
				[
					375,
					2.5
				],
				[
					387.5,
					2.5
				],
				[
					400,
					2.5
				],
				[
					412.5,
					2.5
				],
				[
					425,
					2.5
				],
				[
					430,
					2.5
				],
				[
					440,
					2.5
				],
				[
					455,
					2.5
				],
				[
					470,
					2.5
				],
				[
					495,
					2.5
				],
				[
					512.5,
					2.5
				],
				[
					525,
					2.5
				],
				[
					537.5,
					2.5
				],
				[
					550,
					2.5
				],
				[
					560,
					2.5
				],
				[
					575,
					2.5
				],
				[
					600,
					2.5
				],
				[
					615,
					2.5
				],
				[
					635,
					5
				],
				[
					650,
					5
				],
				[
					662.5,
					5
				],
				[
					672.5,
					5
				],
				[
					682.5,
					5
				],
				[
					687.5,
					5
				],
				[
					700.0000000000002,
					5
				],
				[
					705.0000000000002,
					5
				],
				[
					710.0000000000002,
					5
				],
				[
					717.5000000000002,
					5
				],
				[
					717.5000000000002,
					7.5
				],
				[
					720.0000000000002,
					7.5
				],
				[
					720.0000000000002,
					7.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 37,
			"versionNonce": 2063933863,
			"isDeleted": false,
			"id": "kMErvv4nGyizHLaekPomL",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -1671.03071864184,
			"y": 4298.505504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 20,
			"height": 1295,
			"seed": 920320777,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.5
				],
				[
					-7.5,
					35
				],
				[
					-10,
					80
				],
				[
					-15,
					150
				],
				[
					-15,
					267.5
				],
				[
					-15,
					402.5
				],
				[
					-15,
					540
				],
				[
					-15,
					662.5
				],
				[
					-15,
					787.5
				],
				[
					-15,
					850
				],
				[
					-15,
					915
				],
				[
					-15,
					970
				],
				[
					-15,
					1012.5
				],
				[
					-15,
					1045
				],
				[
					-15,
					1062.5
				],
				[
					-15,
					1080
				],
				[
					-15,
					1100
				],
				[
					-15,
					1130
				],
				[
					-17.5,
					1160
				],
				[
					-17.5,
					1195
				],
				[
					-17.5,
					1215
				],
				[
					-17.5,
					1237.5
				],
				[
					-17.5,
					1257.5
				],
				[
					-17.5,
					1262.5
				],
				[
					-17.5,
					1265
				],
				[
					-17.5,
					1270
				],
				[
					-20,
					1272.5
				],
				[
					-20,
					1280
				],
				[
					-20,
					1287.5
				],
				[
					-20,
					1292.5
				],
				[
					-20,
					1295
				],
				[
					-20,
					1295
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 346,
			"versionNonce": 2090102857,
			"isDeleted": false,
			"id": "auhzV99P",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -2696.03071864184,
			"y": 5683.505504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 1230.8399658203125,
			"height": 180,
			"seed": 1978804425,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "这里是先发送了 正常的订阅报文，\n然后订阅失败，给出了nack报文\n\n然后我这里重新发布了订阅报文，表示先取消订阅，然后重新订阅，2个entry",
			"rawText": "这里是先发送了 正常的订阅报文，\n然后订阅失败，给出了nack报文\n\n然后我这里重新发布了订阅报文，表示先取消订阅，然后重新订阅，2个entry",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "这里是先发送了 正常的订阅报文，\n然后订阅失败，给出了nack报文\n\n然后我这里重新发布了订阅报文，表示先取消订阅，然后重新订阅，2个entry",
			"lineHeight": 1.25,
			"baseline": 167
		},
		{
			"type": "freedraw",
			"version": 67,
			"versionNonce": 425743559,
			"isDeleted": false,
			"id": "rfcE7ceVWm6KRSkd8qAeZ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -1776.03071864184,
			"y": 5748.505504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 1217.5,
			"height": 1422.5,
			"seed": 616118313,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					17.5,
					-7.5
				],
				[
					52.5,
					-35
				],
				[
					102.5,
					-67.5
				],
				[
					170.00000000000023,
					-112.5
				],
				[
					235.00000000000023,
					-162.5
				],
				[
					287.5000000000002,
					-207.5
				],
				[
					352.5000000000002,
					-262.5
				],
				[
					392.5000000000002,
					-297.5
				],
				[
					432.5000000000002,
					-335
				],
				[
					470.0000000000002,
					-367.5
				],
				[
					505.0000000000002,
					-397.5
				],
				[
					537.5000000000002,
					-432.5
				],
				[
					575.0000000000002,
					-472.5
				],
				[
					600.0000000000002,
					-502.5
				],
				[
					612.5000000000002,
					-517.5
				],
				[
					640.0000000000002,
					-555
				],
				[
					657.5000000000002,
					-575
				],
				[
					675.0000000000002,
					-592.5
				],
				[
					690.0000000000002,
					-610
				],
				[
					717.5000000000002,
					-642.5
				],
				[
					750.0000000000002,
					-672.5
				],
				[
					790.0000000000002,
					-712.5
				],
				[
					807.5000000000002,
					-735
				],
				[
					820,
					-752.5
				],
				[
					827.5,
					-765
				],
				[
					835,
					-777.5
				],
				[
					842.5,
					-790
				],
				[
					852.5,
					-812.5
				],
				[
					860,
					-825
				],
				[
					870,
					-842.5
				],
				[
					877.5,
					-852.5
				],
				[
					885,
					-867.5
				],
				[
					895,
					-885
				],
				[
					915,
					-915
				],
				[
					925,
					-935
				],
				[
					935,
					-950
				],
				[
					940,
					-965
				],
				[
					947.5,
					-982.5
				],
				[
					957.5,
					-1000
				],
				[
					962.5,
					-1012.5
				],
				[
					980,
					-1040
				],
				[
					987.5,
					-1052.5
				],
				[
					995,
					-1065
				],
				[
					997.5,
					-1072.5
				],
				[
					1082.5,
					-1217.5
				],
				[
					1095,
					-1242.5
				],
				[
					1105,
					-1267.5
				],
				[
					1110,
					-1282.5
				],
				[
					1112.5,
					-1290
				],
				[
					1125,
					-1317.5
				],
				[
					1132.5,
					-1330
				],
				[
					1142.5,
					-1347.5
				],
				[
					1152.5,
					-1360
				],
				[
					1157.5,
					-1365
				],
				[
					1180,
					-1385
				],
				[
					1192.5,
					-1400
				],
				[
					1202.5,
					-1410
				],
				[
					1212.5,
					-1417.5
				],
				[
					1215,
					-1420
				],
				[
					1217.5,
					-1422.5
				],
				[
					1217.5,
					-1422.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 22,
			"versionNonce": 1796308777,
			"isDeleted": false,
			"id": "fXWD6b24fRy0TIj_aQ_TP",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -703.5307186418399,
			"y": 4331.005504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 175,
			"height": 72.5,
			"seed": 1936289833,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.5,
					0
				],
				[
					5,
					0
				],
				[
					12.5,
					0
				],
				[
					32.5,
					0
				],
				[
					72.5,
					0
				],
				[
					135,
					0
				],
				[
					160,
					0
				],
				[
					172.5,
					-2.5
				],
				[
					175,
					-2.5
				],
				[
					172.5,
					-2.5
				],
				[
					165,
					10
				],
				[
					157.5,
					20
				],
				[
					145,
					40
				],
				[
					135,
					52.5
				],
				[
					122.5,
					67.5
				],
				[
					122.5,
					70
				],
				[
					122.5,
					70
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 14,
			"versionNonce": 673719271,
			"isDeleted": false,
			"id": "c9Q_DYQlTnpkOSvslxCR1",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -2011.03071864184,
			"y": 5488.505504816268,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 135,
			"height": 7.5,
			"seed": 1900497479,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704337299019,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					7.5,
					0
				],
				[
					30,
					-5
				],
				[
					50,
					-7.5
				],
				[
					82.5,
					-7.5
				],
				[
					105,
					-7.5
				],
				[
					122.5,
					-7.5
				],
				[
					130,
					-7.5
				],
				[
					135,
					-7.5
				],
				[
					135,
					-7.5
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "arrow",
			"version": 26,
			"versionNonce": 379584521,
			"isDeleted": false,
			"id": "QBGkgd6NViFn6ELTJlVD-",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -2102.816432927554,
			"y": 6035.624552435316,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 605,
			"height": 1305,
			"seed": 970560487,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1704337311596,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-605,
					1305
				]
			]
		},
		{
			"type": "text",
			"version": 369,
			"versionNonce": 253686343,
			"isDeleted": false,
			"id": "rVi5VeUT",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -3194.0545281656496,
			"y": 7403.195981006746,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 1177.6319580078125,
			"height": 270,
			"seed": 292672391,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704338240344,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "到这里，最后的一个方法是完全模拟，对方的ip，报文完全一致，再试试看\n\n订阅失败的原因\n    1、服务不可用------应该不会   现在是1905  0001，   0001\n    2、第二种是订阅权限的问题？\n    3、其他未知问题！",
			"rawText": "到这里，最后的一个方法是完全模拟，对方的ip，报文完全一致，再试试看\n\n订阅失败的原因\n    1、服务不可用------应该不会   现在是1905  0001，   0001\n    2、第二种是订阅权限的问题？\n    3、其他未知问题！",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "到这里，最后的一个方法是完全模拟，对方的ip，报文完全一致，再试试看\n\n订阅失败的原因\n    1、服务不可用------应该不会   现在是1905  0001，   0001\n    2、第二种是订阅权限的问题？\n    3、其他未知问题！",
			"lineHeight": 1.25,
			"baseline": 257
		},
		{
			"type": "arrow",
			"version": 12,
			"versionNonce": 1696894279,
			"isDeleted": false,
			"id": "94M9X0qh1c2EsqO63ZOom",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -2742.666079662875,
			"y": 7726.9322637351925,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 10,
			"height": 288,
			"seed": 1905489673,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1704345067003,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-10,
					288
				]
			]
		},
		{
			"type": "text",
			"version": 110,
			"versionNonce": 63730569,
			"isDeleted": false,
			"id": "hsS398DA",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -3134.666079662875,
			"y": 8090.9322637351925,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 990.50390625,
			"height": 45,
			"seed": 1987616423,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704345125328,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "确定是不是因为端口的问题，是因为 ip 和mac地址的权限问题",
			"rawText": "确定是不是因为端口的问题，是因为 ip 和mac地址的权限问题",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "确定是不是因为端口的问题，是因为 ip 和mac地址的权限问题",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "text",
			"version": 74,
			"versionNonce": 759095401,
			"isDeleted": false,
			"id": "i8xuG2BG",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -2957.332746329542,
			"y": 8258.538324341254,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 519.3358154296875,
			"height": 90,
			"seed": 2015655849,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704345182473,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "修改 ip 为 172.20.3.7\n修改 mac 为 aa:bb:cc:dd:ee:06",
			"rawText": "修改 ip 为 172.20.3.7\n修改 mac 为 aa:bb:cc:dd:ee:06",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "修改 ip 为 172.20.3.7\n修改 mac 为 aa:bb:cc:dd:ee:06",
			"lineHeight": 1.25,
			"baseline": 77
		},
		{
			"type": "text",
			"version": 214,
			"versionNonce": 417899625,
			"isDeleted": false,
			"id": "GlHtuNvd",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -3078.9994129962083,
			"y": 8435.142719945648,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 1509.4078369140625,
			"height": 45,
			"seed": 1386094503,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704345443814,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "单独修改ip之后，返回的mac 地址为 aabbccddee06 能抓包成功，但是程序不能收到，奇怪吧",
			"rawText": "单独修改ip之后，返回的mac 地址为 aabbccddee06 能抓包成功，但是程序不能收到，奇怪吧",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "单独修改ip之后，返回的mac 地址为 aabbccddee06 能抓包成功，但是程序不能收到，奇怪吧",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "image",
			"version": 90,
			"versionNonce": 1008178857,
			"isDeleted": false,
			"id": "0OYrWgRqweg92nrEfYqH4",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 371.5005870037894,
			"y": 7059.753831056755,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"width": 1718.3574179350826,
			"height": 1407.5714285714294,
			"seed": 1854141225,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"status": "pending",
			"fileId": "2d2d6ddb25345372017c49b7bcdb05e01488791f",
			"scale": [
				1,
				1
			]
		},
		{
			"type": "text",
			"version": 106,
			"versionNonce": 1881201033,
			"isDeleted": false,
			"id": "8Hu2lj8V",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 2392.143444146647,
			"y": 7116.920497723421,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 409.9390869140625,
			"height": 510.71428571428504,
			"seed": 231003561,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"fontSize": 81.71428571428561,
			"fontFamily": 1,
			"text": "19059012\n00000015\n000059d1\n01010200\npayload",
			"rawText": "19059012\n00000015\n000059d1\n01010200\npayload",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "19059012\n00000015\n000059d1\n01010200\npayload",
			"lineHeight": 1.25,
			"baseline": 480
		},
		{
			"type": "text",
			"version": 183,
			"versionNonce": 465485929,
			"isDeleted": false,
			"id": "almZxgsC",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 3241.4489598598093,
			"y": 7115.849069151991,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 429.7945556640625,
			"height": 510.71428571428504,
			"seed": 467408617,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"fontSize": 81.71428571428561,
			"fontFamily": 1,
			"text": "19059012\n00000015\n000059d2\n01010200\npayload",
			"rawText": "19059012\n00000015\n000059d2\n01010200\npayload",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "19059012\n00000015\n000059d2\n01010200\npayload",
			"lineHeight": 1.25,
			"baseline": 480
		},
		{
			"type": "text",
			"version": 262,
			"versionNonce": 750570313,
			"isDeleted": false,
			"id": "8UFJbINr",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 3251.5318806003297,
			"y": 7872.991926294852,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 429.7945556640625,
			"height": 510.71428571428504,
			"seed": 380066759,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"fontSize": 81.71428571428561,
			"fontFamily": 1,
			"text": "19059013\n00000015\n000059d2\n01010200\npayload",
			"rawText": "19059013\n00000015\n000059d2\n01010200\npayload",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "19059013\n00000015\n000059d2\n01010200\npayload",
			"lineHeight": 1.25,
			"baseline": 480
		},
		{
			"type": "text",
			"version": 312,
			"versionNonce": 1266055721,
			"isDeleted": false,
			"id": "POtTlWtV",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 2397.2461663146155,
			"y": 7838.706212009137,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 429.7945556640625,
			"height": 510.71428571428504,
			"seed": 1587181831,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"fontSize": 81.71428571428561,
			"fontFamily": 1,
			"text": "19059013\n00000015\n000059d2\n01010200\npayload",
			"rawText": "19059013\n00000015\n000059d2\n01010200\npayload",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "19059013\n00000015\n000059d2\n01010200\npayload",
			"lineHeight": 1.25,
			"baseline": 480
		},
		{
			"type": "freedraw",
			"version": 48,
			"versionNonce": 148327689,
			"isDeleted": false,
			"id": "x5dRjuo99Z60xbb1pA9oz",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 2409.286301289504,
			"y": 7211.206212009136,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 171.42857142857156,
			"height": 8.571428571428442,
			"seed": 532973255,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.857142857143117
				],
				[
					5.714285714285779,
					2.857142857143117
				],
				[
					25.71428571428578,
					2.857142857143117
				],
				[
					48.57142857142844,
					0
				],
				[
					62.85714285714266,
					0
				],
				[
					71.42857142857156,
					0
				],
				[
					74.28571428571422,
					0
				],
				[
					77.14285714285688,
					0
				],
				[
					88.57142857142844,
					-2.857142857143117
				],
				[
					94.28571428571422,
					-2.857142857143117
				],
				[
					97.14285714285688,
					-2.857142857143117
				],
				[
					100,
					-2.857142857143117
				],
				[
					102.85714285714266,
					-2.857142857143117
				],
				[
					105.71428571428578,
					-2.857142857143117
				],
				[
					108.57142857142844,
					-5.7142857142853245
				],
				[
					114.28571428571422,
					-5.7142857142853245
				],
				[
					117.14285714285688,
					-5.7142857142853245
				],
				[
					120,
					-5.7142857142853245
				],
				[
					122.85714285714266,
					-5.7142857142853245
				],
				[
					125.71428571428578,
					-5.7142857142853245
				],
				[
					131.42857142857156,
					-5.7142857142853245
				],
				[
					142.85714285714266,
					-5.7142857142853245
				],
				[
					148.57142857142844,
					-5.7142857142853245
				],
				[
					157.14285714285688,
					-5.7142857142853245
				],
				[
					162.85714285714266,
					-5.7142857142853245
				],
				[
					165.71428571428578,
					-5.7142857142853245
				],
				[
					168.57142857142844,
					-5.7142857142853245
				],
				[
					171.42857142857156,
					-5.7142857142853245
				],
				[
					171.42857142857156,
					-5.7142857142853245
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 35,
			"versionNonce": 1281016809,
			"isDeleted": false,
			"id": "lzhNzTcMnR9Y_i-SZFD32",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 2643.5720155752183,
			"y": 7205.491926294851,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 122.85714285714266,
			"height": 2.8571428571422075,
			"seed": 449066919,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.8571428571422075
				],
				[
					5.714285714285779,
					2.8571428571422075
				],
				[
					28.57142857142844,
					2.8571428571422075
				],
				[
					45.71428571428578,
					2.8571428571422075
				],
				[
					57.14285714285734,
					2.8571428571422075
				],
				[
					68.57142857142844,
					2.8571428571422075
				],
				[
					80,
					2.8571428571422075
				],
				[
					85.71428571428578,
					2.8571428571422075
				],
				[
					97.14285714285734,
					2.8571428571422075
				],
				[
					102.85714285714266,
					2.8571428571422075
				],
				[
					105.71428571428578,
					2.8571428571422075
				],
				[
					114.28571428571422,
					2.8571428571422075
				],
				[
					117.14285714285734,
					2.8571428571422075
				],
				[
					120,
					2.8571428571422075
				],
				[
					122.85714285714266,
					2.8571428571422075
				],
				[
					122.85714285714266,
					2.8571428571422075
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 114,
			"versionNonce": 34365129,
			"isDeleted": false,
			"id": "LbZn0pOnhI0ykyeUxhvVV",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 2415.00058700379,
			"y": 7311.206212009136,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 380,
			"height": 11.428571428571558,
			"seed": 1030146569,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.8571428571426623,
					0
				],
				[
					2.8571428571426623,
					2.857142857143117
				],
				[
					22.857142857142662,
					2.857142857143117
				],
				[
					34.28571428571422,
					2.857142857143117
				],
				[
					42.85714285714266,
					2.857142857143117
				],
				[
					45.71428571428578,
					2.857142857143117
				],
				[
					48.57142857142844,
					2.857142857143117
				],
				[
					54.28571428571422,
					2.857142857143117
				],
				[
					60,
					2.857142857143117
				],
				[
					62.85714285714266,
					2.857142857143117
				],
				[
					65.71428571428578,
					2.857142857143117
				],
				[
					71.4285714285711,
					2.857142857143117
				],
				[
					74.28571428571422,
					2.857142857143117
				],
				[
					80,
					2.857142857143117
				],
				[
					85.71428571428578,
					0
				],
				[
					91.4285714285711,
					0
				],
				[
					97.14285714285688,
					0
				],
				[
					102.85714285714266,
					-2.857142857143117
				],
				[
					105.71428571428578,
					-2.857142857143117
				],
				[
					111.4285714285711,
					-5.7142857142853245
				],
				[
					120,
					-5.7142857142853245
				],
				[
					125.71428571428578,
					-5.7142857142853245
				],
				[
					134.28571428571422,
					-8.571428571428442
				],
				[
					140,
					-8.571428571428442
				],
				[
					142.85714285714266,
					-8.571428571428442
				],
				[
					148.57142857142844,
					-8.571428571428442
				],
				[
					151.4285714285711,
					-8.571428571428442
				],
				[
					154.28571428571422,
					-8.571428571428442
				],
				[
					160,
					-8.571428571428442
				],
				[
					162.85714285714266,
					-8.571428571428442
				],
				[
					165.71428571428578,
					-8.571428571428442
				],
				[
					171.4285714285711,
					-8.571428571428442
				],
				[
					174.28571428571422,
					-8.571428571428442
				],
				[
					177.14285714285688,
					-8.571428571428442
				],
				[
					180,
					-8.571428571428442
				],
				[
					182.85714285714266,
					-8.571428571428442
				],
				[
					185.71428571428578,
					-8.571428571428442
				],
				[
					191.4285714285711,
					-8.571428571428442
				],
				[
					194.28571428571422,
					-8.571428571428442
				],
				[
					197.14285714285688,
					-8.571428571428442
				],
				[
					200,
					-8.571428571428442
				],
				[
					205.71428571428578,
					-8.571428571428442
				],
				[
					208.57142857142844,
					-8.571428571428442
				],
				[
					211.4285714285711,
					-8.571428571428442
				],
				[
					214.28571428571422,
					-8.571428571428442
				],
				[
					217.14285714285688,
					-8.571428571428442
				],
				[
					220,
					-8.571428571428442
				],
				[
					222.85714285714266,
					-8.571428571428442
				],
				[
					225.71428571428578,
					-8.571428571428442
				],
				[
					228.57142857142844,
					-8.571428571428442
				],
				[
					231.4285714285711,
					-8.571428571428442
				],
				[
					237.14285714285688,
					-8.571428571428442
				],
				[
					240,
					-8.571428571428442
				],
				[
					242.85714285714266,
					-8.571428571428442
				],
				[
					245.71428571428578,
					-8.571428571428442
				],
				[
					251.4285714285711,
					-8.571428571428442
				],
				[
					254.28571428571422,
					-8.571428571428442
				],
				[
					260,
					-8.571428571428442
				],
				[
					262.85714285714266,
					-8.571428571428442
				],
				[
					268.57142857142844,
					-8.571428571428442
				],
				[
					271.4285714285711,
					-8.571428571428442
				],
				[
					274.2857142857142,
					-8.571428571428442
				],
				[
					277.1428571428569,
					-8.571428571428442
				],
				[
					280,
					-8.571428571428442
				],
				[
					282.85714285714266,
					-8.571428571428442
				],
				[
					285.7142857142858,
					-8.571428571428442
				],
				[
					288.57142857142844,
					-8.571428571428442
				],
				[
					294.2857142857142,
					-8.571428571428442
				],
				[
					300,
					-5.7142857142853245
				],
				[
					302.85714285714266,
					-5.7142857142853245
				],
				[
					308.57142857142844,
					-5.7142857142853245
				],
				[
					311.4285714285711,
					-5.7142857142853245
				],
				[
					314.2857142857142,
					-5.7142857142853245
				],
				[
					317.1428571428569,
					-5.7142857142853245
				],
				[
					320,
					-5.7142857142853245
				],
				[
					322.85714285714266,
					-5.7142857142853245
				],
				[
					325.7142857142858,
					-5.7142857142853245
				],
				[
					328.57142857142844,
					-5.7142857142853245
				],
				[
					334.2857142857142,
					-5.7142857142853245
				],
				[
					337.1428571428569,
					-5.7142857142853245
				],
				[
					340,
					-5.7142857142853245
				],
				[
					342.85714285714266,
					-5.7142857142853245
				],
				[
					345.7142857142858,
					-5.7142857142853245
				],
				[
					348.57142857142844,
					-5.7142857142853245
				],
				[
					351.4285714285711,
					-5.7142857142853245
				],
				[
					357.1428571428569,
					-5.7142857142853245
				],
				[
					360,
					-5.7142857142853245
				],
				[
					362.85714285714266,
					-5.7142857142853245
				],
				[
					365.7142857142858,
					-5.7142857142853245
				],
				[
					368.57142857142844,
					-5.7142857142853245
				],
				[
					371.42857142857156,
					-5.7142857142853245
				],
				[
					374.2857142857142,
					-5.7142857142853245
				],
				[
					377.1428571428569,
					-8.571428571428442
				],
				[
					380,
					-8.571428571428442
				],
				[
					380,
					-8.571428571428442
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 45,
			"versionNonce": 143105449,
			"isDeleted": false,
			"id": "ht-IzS70S-DOGvoqmbS00",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 2400.7148727180756,
			"y": 7394.063354866279,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 160,
			"height": 2.857142857143117,
			"seed": 1478096105,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					5.7142857142853245,
					0
				],
				[
					25.714285714285325,
					0
				],
				[
					48.57142857142844,
					0
				],
				[
					60,
					0
				],
				[
					68.57142857142844,
					0
				],
				[
					80,
					0
				],
				[
					85.71428571428532,
					0
				],
				[
					91.4285714285711,
					0
				],
				[
					97.14285714285688,
					0
				],
				[
					102.85714285714266,
					-2.857142857143117
				],
				[
					105.71428571428532,
					-2.857142857143117
				],
				[
					111.4285714285711,
					-2.857142857143117
				],
				[
					117.14285714285688,
					-2.857142857143117
				],
				[
					120,
					-2.857142857143117
				],
				[
					125.71428571428532,
					-2.857142857143117
				],
				[
					131.4285714285711,
					-2.857142857143117
				],
				[
					134.28571428571422,
					-2.857142857143117
				],
				[
					137.14285714285688,
					-2.857142857143117
				],
				[
					142.85714285714266,
					-2.857142857143117
				],
				[
					145.71428571428532,
					-2.857142857143117
				],
				[
					148.57142857142844,
					-2.857142857143117
				],
				[
					151.4285714285711,
					-2.857142857143117
				],
				[
					154.28571428571422,
					-2.857142857143117
				],
				[
					157.14285714285688,
					-2.857142857143117
				],
				[
					160,
					-2.857142857143117
				],
				[
					160,
					-2.857142857143117
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 39,
			"versionNonce": 1593311369,
			"isDeleted": false,
			"id": "91YwEaYMjJ4FV0r0RQwNZ",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 2637.8577298609325,
			"y": 7402.6347834377075,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 160,
			"height": 2.857142857143117,
			"seed": 1123650921,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.857142857143117
				],
				[
					11.428571428571558,
					2.857142857143117
				],
				[
					28.57142857142844,
					2.857142857143117
				],
				[
					51.42857142857156,
					2.857142857143117
				],
				[
					62.85714285714312,
					2.857142857143117
				],
				[
					74.28571428571422,
					2.857142857143117
				],
				[
					85.71428571428578,
					2.857142857143117
				],
				[
					100,
					2.857142857143117
				],
				[
					114.28571428571422,
					2.857142857143117
				],
				[
					120,
					2.857142857143117
				],
				[
					128.57142857142844,
					2.857142857143117
				],
				[
					131.42857142857156,
					2.857142857143117
				],
				[
					137.14285714285734,
					2.857142857143117
				],
				[
					140,
					2.857142857143117
				],
				[
					145.71428571428578,
					2.857142857143117
				],
				[
					151.42857142857156,
					2.857142857143117
				],
				[
					154.28571428571422,
					2.857142857143117
				],
				[
					157.14285714285734,
					2.857142857143117
				],
				[
					160,
					2.857142857143117
				],
				[
					160,
					2.857142857143117
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 38,
			"versionNonce": 320407401,
			"isDeleted": false,
			"id": "nuHD7Rb61O-O5YaKBRpF3",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 3486.4291584323614,
			"y": 7402.6347834377075,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 185.71428571428532,
			"height": 2.857142857143117,
			"seed": 117815465,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.8571428571426623,
					0
				],
				[
					5.7142857142853245,
					0
				],
				[
					8.571428571428442,
					0
				],
				[
					20,
					2.857142857143117
				],
				[
					42.85714285714266,
					2.857142857143117
				],
				[
					71.4285714285711,
					2.857142857143117
				],
				[
					85.71428571428532,
					2.857142857143117
				],
				[
					97.14285714285688,
					2.857142857143117
				],
				[
					105.71428571428532,
					2.857142857143117
				],
				[
					114.28571428571422,
					2.857142857143117
				],
				[
					125.71428571428532,
					0
				],
				[
					134.28571428571422,
					0
				],
				[
					142.85714285714266,
					0
				],
				[
					154.28571428571422,
					0
				],
				[
					168.57142857142844,
					0
				],
				[
					177.14285714285688,
					0
				],
				[
					182.85714285714266,
					0
				],
				[
					185.71428571428532,
					0
				],
				[
					185.71428571428532,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 79,
			"versionNonce": 1865822793,
			"isDeleted": false,
			"id": "b-Mea4liVyZVWORP62Bnx",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 2417.8577298609325,
			"y": 7502.6347834377075,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 360,
			"height": 2.857142857143117,
			"seed": 594312457,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.857142857143117,
					0
				],
				[
					5.714285714285779,
					0
				],
				[
					8.571428571428442,
					0
				],
				[
					11.428571428571558,
					0
				],
				[
					25.71428571428578,
					0
				],
				[
					57.14285714285734,
					2.857142857143117
				],
				[
					77.14285714285734,
					2.857142857143117
				],
				[
					100,
					2.857142857143117
				],
				[
					111.42857142857156,
					2.857142857143117
				],
				[
					117.14285714285734,
					2.857142857143117
				],
				[
					122.85714285714312,
					2.857142857143117
				],
				[
					128.57142857142844,
					2.857142857143117
				],
				[
					134.28571428571422,
					2.857142857143117
				],
				[
					142.85714285714312,
					2.857142857143117
				],
				[
					148.57142857142844,
					2.857142857143117
				],
				[
					154.28571428571422,
					2.857142857143117
				],
				[
					160,
					2.857142857143117
				],
				[
					168.57142857142844,
					2.857142857143117
				],
				[
					177.14285714285734,
					2.857142857143117
				],
				[
					180,
					2.857142857143117
				],
				[
					182.85714285714312,
					2.857142857143117
				],
				[
					188.57142857142844,
					2.857142857143117
				],
				[
					191.42857142857156,
					2.857142857143117
				],
				[
					194.28571428571422,
					2.857142857143117
				],
				[
					200,
					2.857142857143117
				],
				[
					214.28571428571422,
					2.857142857143117
				],
				[
					220,
					2.857142857143117
				],
				[
					231.42857142857156,
					2.857142857143117
				],
				[
					234.28571428571422,
					2.857142857143117
				],
				[
					237.14285714285734,
					2.857142857143117
				],
				[
					240,
					2.857142857143117
				],
				[
					242.85714285714312,
					2.857142857143117
				],
				[
					245.71428571428578,
					2.857142857143117
				],
				[
					251.42857142857156,
					2.857142857143117
				],
				[
					254.28571428571422,
					2.857142857143117
				],
				[
					257.14285714285734,
					2.857142857143117
				],
				[
					260,
					2.857142857143117
				],
				[
					262.8571428571431,
					2.857142857143117
				],
				[
					265.7142857142858,
					2.857142857143117
				],
				[
					268.57142857142844,
					0
				],
				[
					271.42857142857156,
					0
				],
				[
					274.2857142857142,
					0
				],
				[
					280,
					0
				],
				[
					285.7142857142858,
					0
				],
				[
					288.57142857142844,
					0
				],
				[
					291.42857142857156,
					0
				],
				[
					300,
					0
				],
				[
					305.7142857142858,
					0
				],
				[
					311.42857142857156,
					0
				],
				[
					322.8571428571431,
					0
				],
				[
					328.57142857142844,
					0
				],
				[
					334.2857142857142,
					0
				],
				[
					340,
					0
				],
				[
					342.8571428571431,
					0
				],
				[
					348.57142857142844,
					0
				],
				[
					351.42857142857156,
					0
				],
				[
					354.2857142857142,
					0
				],
				[
					357.14285714285734,
					0
				],
				[
					360,
					0
				],
				[
					360,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 35,
			"versionNonce": 1747648809,
			"isDeleted": false,
			"id": "NiybVbZuKvt4Yt9Tyx_x1",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 2403.5720155752183,
			"y": 7651.206212009136,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 354.2857142857142,
			"height": 20,
			"seed": 1168454473,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					11.428571428571558,
					0
				],
				[
					42.85714285714266,
					0
				],
				[
					100,
					0
				],
				[
					145.71428571428578,
					2.857142857143117
				],
				[
					185.71428571428578,
					2.857142857143117
				],
				[
					205.71428571428578,
					2.857142857143117
				],
				[
					222.85714285714266,
					2.857142857143117
				],
				[
					242.85714285714266,
					-2.857142857143117
				],
				[
					262.85714285714266,
					-5.7142857142853245
				],
				[
					282.85714285714266,
					-8.571428571428442
				],
				[
					320,
					-11.428571428571558
				],
				[
					334.2857142857142,
					-14.285714285713766
				],
				[
					348.57142857142844,
					-17.142857142856883
				],
				[
					351.42857142857156,
					-17.142857142856883
				],
				[
					354.2857142857142,
					-17.142857142856883
				],
				[
					354.2857142857142,
					-17.142857142856883
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 20,
			"versionNonce": 1264776201,
			"isDeleted": false,
			"id": "nSx5j3X_vicBSsqlawQvT",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 2572.1434441466467,
			"y": 7791.206212009136,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 884343561,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 20,
			"versionNonce": 752454377,
			"isDeleted": false,
			"id": "5FEHWsDPEwgxuCIrmeb8p",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 2120.7148727180756,
			"y": 6788.349069151993,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 1511658409,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353168606,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 3,
			"versionNonce": 1007856615,
			"isDeleted": false,
			"id": "ik5K0_ef8DtvEoeBcu9-C",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -2363.6660796628767,
			"y": 8595.396688199611,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 773089353,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704351588382,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "arrow",
			"version": 14,
			"versionNonce": 76938151,
			"isDeleted": false,
			"id": "NFprS3oX9sP81GBDLensR",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -2683.547032043829,
			"y": 8699.801450104373,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 305.71428571428623,
			"height": 517.1428571428587,
			"seed": 664502505,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1704351595885,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					305.71428571428623,
					517.1428571428587
				]
			]
		},
		{
			"type": "text",
			"version": 262,
			"versionNonce": 650549191,
			"isDeleted": false,
			"id": "ULtjSrEK",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -2703.547032043829,
			"y": 9294.087164390088,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 1395.3599853515625,
			"height": 135,
			"seed": 801500871,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704351656252,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "修改ip  和mac 成功 解决了\n\n出现新的问题： 只能接收到 一次 的 notify 报文，其他 的报文都被抛弃掉，定位原因",
			"rawText": "修改ip  和mac 成功 解决了\n\n出现新的问题： 只能接收到 一次 的 notify 报文，其他 的报文都被抛弃掉，定位原因",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "修改ip  和mac 成功 解决了\n\n出现新的问题： 只能接收到 一次 的 notify 报文，其他 的报文都被抛弃掉，定位原因",
			"lineHeight": 1.25,
			"baseline": 122
		},
		{
			"type": "arrow",
			"version": 20,
			"versionNonce": 507780521,
			"isDeleted": false,
			"id": "HJ0Z91GQylRUNtclrSPrk",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -2160.689889186686,
			"y": 9542.658592961516,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 371.42857142857133,
			"height": 357.1428571428569,
			"seed": 207262215,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1704351663271,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					371.42857142857133,
					357.1428571428569
				]
			]
		},
		{
			"type": "text",
			"version": 257,
			"versionNonce": 119584359,
			"isDeleted": false,
			"id": "Co0pugU7",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -2009.2613177581145,
			"y": 9994.087164390086,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 1345.53564453125,
			"height": 225,
			"seed": 153387145,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704352518352,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "原因： 在 routing_manager_impl.cpp：2452附近， its_subscribers 大小为0.  \n打印出来的为 1\n没能打印出来的为0\n\n查找为什么这个 会变成 0",
			"rawText": "原因： 在 routing_manager_impl.cpp：2452附近， its_subscribers 大小为0.  \n打印出来的为 1\n没能打印出来的为0\n\n查找为什么这个 会变成 0",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "原因： 在 routing_manager_impl.cpp：2452附近， its_subscribers 大小为0.  \n打印出来的为 1\n没能打印出来的为0\n\n查找为什么这个 会变成 0",
			"lineHeight": 1.25,
			"baseline": 212
		},
		{
			"type": "arrow",
			"version": 34,
			"versionNonce": 388339017,
			"isDeleted": false,
			"id": "VeqlIWXKw2zvmx8wVDHqd",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -1700.6898891866858,
			"y": 10305.515735818657,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 417.1428571428569,
			"height": 440,
			"seed": 1014335655,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1704352523370,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-417.1428571428569,
					440
				]
			]
		},
		{
			"type": "text",
			"version": 364,
			"versionNonce": 175440455,
			"isDeleted": false,
			"id": "Zgcim9O7",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -2537.8327463295427,
			"y": 10865.515735818659,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 1786.751708984375,
			"height": 270,
			"seed": 1140455943,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1704353035694,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "原因是 被过滤掉了， 过滤原因  在app 的地方在  request event的时候  类型写成了  field 导致 被过滤掉 \n\n为什么要有这种机制 是未知的， 条件是 因为 三个\n1、type 是 field\n2、不是强制执行的\n3、payload 没有改变",
			"rawText": "原因是 被过滤掉了， 过滤原因  在app 的地方在  request event的时候  类型写成了  field 导致 被过滤掉 \n\n为什么要有这种机制 是未知的， 条件是 因为 三个\n1、type 是 field\n2、不是强制执行的\n3、payload 没有改变",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "原因是 被过滤掉了， 过滤原因  在app 的地方在  request event的时候  类型写成了  field 导致 被过滤掉 \n\n为什么要有这种机制 是未知的， 条件是 因为 三个\n1、type 是 field\n2、不是强制执行的\n3、payload 没有改变",
			"lineHeight": 1.25,
			"baseline": 257
		},
		{
			"id": "rPCdlM0SE8WM4xJD7JoDS",
			"type": "arrow",
			"x": -2305.5407605375544,
			"y": 11208.242601791604,
			"width": 502.2222222222224,
			"height": 360,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 45662646,
			"version": 19,
			"versionNonce": 1670882154,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1704439403515,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					502.2222222222224,
					360
				]
			],
			"lastCommittedPoint": null,
			"startBinding": null,
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "lzl4AEPn",
			"type": "text",
			"x": -2096.6518716486653,
			"y": 11641.575935124938,
			"width": 858.1319580078125,
			"height": 90,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 35737834,
			"version": 68,
			"versionNonce": 408244150,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1704439428179,
			"link": null,
			"locked": false,
			"text": "发现端口也必须一致 必须为30406  ，所以比较严格\n",
			"rawText": "发现端口也必须一致 必须为30406  ，所以比较严格\n",
			"fontSize": 36,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 77,
			"containerId": null,
			"originalText": "发现端口也必须一致 必须为30406  ，所以比较严格\n",
			"lineHeight": 1.25
		}
	],
	"appState": {
		"theme": "light",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#2f9e44",
		"currentItemBackgroundColor": "transparent",
		"currentItemFillStyle": "solid",
		"currentItemStrokeWidth": 4,
		"currentItemStrokeStyle": "solid",
		"currentItemRoughness": 2,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 1,
		"currentItemFontSize": 36,
		"currentItemTextAlign": "left",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"scrollX": 3053.3185383153323,
		"scrollY": -10071.575935124938,
		"zoom": {
			"value": 0.44999999999999996
		},
		"currentItemRoundness": "round",
		"gridSize": null,
		"gridColor": {
			"Bold": "#C9C9C9FF",
			"Regular": "#EDEDEDFF"
		},
		"currentStrokeOptions": null,
		"previousGridSize": null,
		"frameRendering": {
			"enabled": true,
			"clip": true,
			"name": true,
			"outline": true
		}
	},
	"files": {}
}
```
%%