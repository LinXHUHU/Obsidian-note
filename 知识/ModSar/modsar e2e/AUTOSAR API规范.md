# API

`ris:AncientGate`PRS_E2E_UC_00321

**发送接口调用

```
middleware_send(in dataRecord)
```

**接收接口调用

```
# 需要多输出一个 result，代表结果
middleware_receive(out dataRecord, out e2eResult)
```

---
`ris:AncientGate`PRS_E2E_00322

- e2eResult 应该包含e2eStatus
- e2eState 即 SM

---
DataID 应该使用  serviceid  eventid  以及  instanceid 共同定义 ，对于event来说



## Configuration Parameters
 对应 class  CmConfig



CMconfig 的解释在 表 Table 8.1: E2E configuration parameters

后面还有关于参数范围的限制




## 协议的使用和指导

CRC的计算应该 在 上面数据区域
For profiles 1, 2, 4, 5, 6, 7, 11, and 22 the E2E CRC should
be calculated over the following parts of the serialized SOME/IP message
1. Request ID (Client ID / Session ID) [32 bit]
2. Protocol Version [8 bit]
3. Interface Version [8 bit]
4. Message Type [8 bit]
5. Return Code [8 bit]
6. Payload [variable size]


For profiles 4m, 7m, 8m and 44m the E2E CRC shall be
calculated over the following parts of the serialized SOME/IP message.
1. Payload [variable size]



---
- 当服务器收到 一帧计数之后，应该返回 这个 counter 无论是 返回错误或者正常帧


---
e2e check 方法应该在  最大容错时间（FTTI）之内至少调用一次



---
最大数据长度
![[Pasted image 20231121182209.png]]

--- 
要求E2E错误检测，包括错误码

---
关于 Xmmessage的相关规定
1. Xm 消息类型定义  request 和  response
2. 消息结果定义   ok error
3. 每个e2e profile  提供  protect  check 以及 forward （AOS 中没有，可能是功能和protect类似）三种方法



---
计数功能 counter

接收端：
1. Repitition 数据重复，没有新数据
2. OK 正常加一，或者在容忍范围内
3. error 容忍范围外丢包

---
超时检测

---
counter 智能被profile 使用，不被上层使用修改

递增，当达到上限，归零，重新计数



---

TransitToInvalidExtended 

0
![[Pasted image 20231129171201.png]]
1

Figure 6.130: E2E state machine check


