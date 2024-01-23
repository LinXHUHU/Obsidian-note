

# 什么是E2E
E2E，全称End to End，中文即端到端的通信保护，是一种针对安全相关数据，为防止通信链路中可能存在的故障（HW/SW）， 在 通信节点 之间 执行的 一种数据保护协议/机制。其适用于多种网络结构：CAN、 CANFD、FlexRay、Ethernet等

只要涉及通信就需要这个，只是AUTOSAR对其进行了规范


![[Pasted image 20231110134450.png]]



# 数据通信过程的失效模式


数据交换过程中可能的失效模式 有哪些呢？关于这个问题ISO26262 中有总结，如下:

● 信息的重复发送 (Repetition of Information)，相同的信息被收到了多次

● 信息的丢失 (Loss of Information)，整条或者信息的一部分在通信过程中丢失

● 信息的延迟 (Delay of Information)，接收信息的时间异于期望的时间

● 信息的插入 (Insertion of Information)，多余的内容被插入到信息中

● 假冒的或者不正确的寻址 (Masquerade or Incorrect Addressing of Information)，假冒的发送者发送未认证的信息被接收端接受，或者正确的信息被错误的接收端接受

● 信息顺序错误 (Incorrect Sequence of Information)，数据流中的信息顺序错误

● 信息破损 (Corruption of Information)，信息的内容被篡改

● 向多个接收端发送非对称信息 (Asymmetric information sent from a sender to multiple receivers)，接收端收到的数据不一致

● 仅部分接收端收到发送者的信息 (Information from a sender received by only a subset of receivers

● 阻塞通信通道 (Blocking access to communication channel)






# e2e 的实现

针对E2E 数据校验目前存在2种方式，如下

E2E Lib + E2E PW: 采用这种方式的校验E2E_Check接口将返回E2E PXX Status（例子可参见E2E PXX Status Estimation） ，App 需要自行根据返回的E2E PXX Status来判断采取什么Action , 对于这种组合在AUTOSAR 4.3 之后就不再采用了

E2E Lib +E2EXf+ E2ESM: 对于AUTOSAR 4.3 之后的版本都将采用这种组合，和前面提到的那种方式相比这种方式提供了滑动窗和动态判断“错误”的机制，使得APP 不用自己去技术和实现机制来完成一些功能

比如： 我们要判断5 次里有3次CRC 错误，我们就采取措施，如果采用E2E Lib + E2E PW 方式。APP 需要自行实现这个滑动窗动态监测机制，但是在E2E Lib +E2EXf+ E2ESM模式下只需要配置对应的属性即可完成

NOTE: 虽然E2E Lib +E2EXf+ E2ESM 可以减少APP的实现，但是需要相关人员对于这套组合具有非常好的理解才行。相比E2E Lib + E2E PW 虽然实现简单了，但是配置复杂度增加了

---
E2EXf = E2E Transformer

E2E Protection Wrapper



[AUTOSAR_TR_BSWModuleList.xls](https://www.autosar.org/fileadmin/standards/R4-2/CP/AUTOSAR_TR_BSWModuleList.pdf)


E2E Lib +E2EXf+ E2ESM=  lib+transformer + 状态管理


## AUTOSAR_EXP_ARAComAPI
- SWS_CM_10474

RawDataStream接口仅传输原始数据，不包含任何数据类型信息。因此，原始数据流接口无法提供任何数据保护，比如E2E保护。如果需要此类保护，必须在使用RawDataStream接口的应用程序中进行实现。

InstanceSpecifier和InstanceIdentifier可用于唯一标识提供的服务。这意味着客户端知道他们正在与哪个特定的服务实例进行通信。然而对于提供的服务来说，缺乏此信息。客户端无法通过InstanceIdentifier得到唯一标识，因此服务器无法确定与哪个客户端通信。在大多数情况下，这并不是问题，然而我们预见到在安全性方面这可能会成为一个问题。对于这些情况，我们建议使用方法E2E_check的E2E参数dataID（参见[10]的PRS_E2E_00323）。

## Specification of Communication Management
- serializedSample由两部分组成，e2e头和序列化之后的数据

一个周期描述了定期发送和接收消息的时间间隔。对于具有消息计数器的E2E保护消息来说，这非常重要，这个计数器应该在每个新周期（即每个新消息）由发送实体递增。在每个周期内，接收实体应检查是否有新消息到达，以及其内容是否可用。有关更多信息，请参阅文档PRS_E2EProtocol（第6章）和SWS_E2ELibrary（第9章）。


**事件的E2E保护设置**
- E2E受保护的事件应在End2EndEventProtectionProps和E2EProfileConfiguration中配置其选项。这些设置需符合E2E保护的要求。

**E2E功能的要求**
- 在此部分提及的E2E功能，如E2E_protect和E2E_check，应符合E2E保护的要求，这些要求在[7]中定义，并遵守[4]中的E2E保护协议规范（特别是[PRS_E2E_00323]）。对E2E保护的需求还包括符合指定的数据ID，这个ID基于特定的事件类，属于特定的Service-Proxy/ServiceSkeleton类。



**存在一些限制
1、 counterOffset
 crcOffset
 dataIdNibbleOffset 这三个值由标准规定，不能更改   等等 不重要


![[Pasted image 20231113170102.png]]




Figure 7.27: E2E Subscriber




**对于E2E-protected Events，对于接收到的一个或多个样本的序列化数据，应执行以下步骤：

1. **处理E2E-protected样本的非E2E保护标头**
   - 对于给定的E2E-protected样本，GetNewSamples将处理样本序列化数据的非E2E-protected标头（如果有）。
2. **E2E_check的调用**
   - 对于给定的E2E-protected样本，将根据[PRS_E2E_00323]的规范，传递受保护的序列化数据（作为参数serializedData传递给E2E_check）进行E2E_check的调用。
3. **传递dataID参数**
   - 对于给定的E2E-protected样本，End2EndEventProtectionProps.dataId将作为参数dataID传递给E2E_check。
4. **提供E2E_check的Result**
   - 对于给定的E2E-protected样本，E2E_check将提供一个Result（根据[4]的[PRS_E2E_00322]）包含SMState（根据[4]的[PRS_E2E_00322]）和ProfileCheckStatus（根据[4]的[PRS_E2E_00322]）的元素。
5. **移除E2E保护标头**
   - 对于给定的E2E-protected样本，将从序列化数据中移除E2E保护标头。
6. **反序列化样本**
   - 对于给定的E2E-protected样本，在特定的网络绑定规则下（例如，在SOME/IP网络绑定情况下），GetNewSamples将根据规则对序列化数据进行反序列化，得到反序列化的样本。
7. **存储和更新状态信息**
   - 对于给定的E2E-protected样本，GetNewSamples将将ProfileCheckStatus存储在SamplePtr中，并更新或覆盖特定Event class内的全局SMState。



**对于未收到序列化数据的E2E-protected Events，E2E保护将作为超时检测而工作，步骤较为简单。

1. **调用E2E_check**
   - 对于未收到序列化数据的情况，根据[PRS_E2E_00323]的规范，将在null样本上（即传递一个空指针作为参数serializedData给E2E_check）进行E2E_check的调用。

2. **传递dataID参数**
   - 对于未收到序列化数据的情况，End2EndEventProtectionProps.dataId将作为参数dataID传递给E2E_check。

3. **提供E2E_check的Result**
   - 对于给定的null样本，E2E_check将提供一个Result（根据[4]的[PRS_E2E_00322]）包含SMState（根据[4]的[PRS_E2E_00322]）和ProfileCheckStatus（根据[4]的[PRS_E2E_00322]）的元素。

4. **更新状态信息**
   - 对于未收到序列化数据的E2E-protected Events，GetNewSamples将更新或覆盖特定Event class内的全局SMState。




**Subscriber - Access to E2E information

这些条款表明在特定服务代理类的每个事件类中提供了 GetE2EStateMachineState 方法。这个方法提供了对特定事件类的全局 SMState 的访问权限，该状态是在上一次对 GetNewSamples 的调用中通过上一次调用 E2E_check 函数确定的。这个方法应该返回一个 ara::com::e2e::SMState 对象。

```
ara::com::e2e::SMState GetE2EStateMachineState() const noexcept;
```


**End-to-end communication protection for Methods


**两个图

7.29: Interaction of components during E2E checking of the Method request at
the server side - polling

Interaction of components during E2E checking of the Method request at
the server side - event driven



保护方法


保护payload






## AUTOSAR_PRS_E2EProtocol

## AUTOSAR_RS_E2E