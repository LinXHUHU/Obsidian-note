


> 1.   **Technical field of the invention and Prior art state**. (_Please give a brief introduction about the technical field of the invention._ The purpose is to let the readers of this document have a brief information about the technology)

在现代汽车系统中，各种电子控制单元（ECU）之间的通信对于实现高效可靠的操作至关重要。随着Adas以及自动驾驶技术的发展，需要传输的数据量非常庞大，传统的通信协议和中间件解决方案通常在满足汽车应用的实时性和带宽需求方面面临挑战。

近年来，通信技术的进步导致了像DDS（Data Distribution Service）这样的解决方案的出现，它提供了适用于汽车应用的高性能、实时的数据分发。DDS利用多种数据传输等技术来增强效率，利用实时数据分发最小化ECU之间的通信延迟，利用零拷贝技术加大片内进程之间通信的数据吞吐量。这种方法解决了传统中间件解决方案的一些缺点，使其在汽车软件架构中尤其具有前景。

本发明的目的是在轻量级autosar解决方案MODAR中，在SOA架构的基础上实现零拷贝技术，进一步改进现有的MODSAR COM模块的通信数据传输性能、增强性能。本发明旨在为汽车系统在轻量级的基础上提供更高效可靠的通信解决方案，满足现代车辆架构的不断发展的需求。

> 1.   **Problem to be solved; which prior art defects can be improved?** (As a logic sequence of the state of art, please point out the defeats of the state of art which has been overcome in the invention)

该发明旨在解决轻量级autosar中间件框架MODSAR使用的先前技术通信系统和中间件解决方案存在的多种限制和缺陷。这些缺陷包括：

2. **实时性能**：许多现有的通信协议和中间件解决方案往往难以满足现代汽车应用的严格实时要求。数据传输的延迟可能会导致延迟问题，影响到诸如高级驾驶辅助系统（ADAS）和自动驾驶等关键功能， 数据量大且对实时性要求较高。
    
3. **带宽效率**：一些先前的解决方案可能无法有效利用可用的网络带宽，导致潜在的拥塞和低效率，特别是在需要在ECU之间交换大量数据的场景中。
    

该发明通过将DDS零拷贝技术移植到modsar框架中的组件通信（COM）模块中，从而提供了几项改进来克服这些缺陷：
    
2. **提高的实时性能**：利用DDS协议高性能数据分发能力，本发明确保及时可预测的数据传递，满足关键汽车功能的严格时间要求。
    
3. **降低资源消耗**：DDS零拷贝数据传输通路通过采用高效的数据序列化机制和零拷贝数据传输机制，减少不必要的开销，最大限度地提高CPU利用率， 提高数据传输速度以及传输吞吐量。

总的来说，该发明解决了先前通信系统和中间件解决方案的限制，为现代汽车架构提供了更高效、可扩展和可靠的通信解决方案


> **1.**   **What are the main improvements and advantage of the invention, especially compared to what is already known?**( After analyzing the defeats of the state of art, what purposes would you like to achieve via the invention. The advantage of the invention over the state of art should be described here.)

该发明针对Modsar中间件解决方案，引入了几项关键改进和优势，包括：

1. **增强的性能**：将dds零拷贝技术移植进入通信框架中，提高数据传输量，降低了延迟，提高了整个系统的响应能力。这确保了及时可预测的数据传递，对于诸如ADAS和自动驾驶等实时汽车应用至关重要。
    
4. **降低的资源消耗**：采用高效的数据序列化机制以及零拷贝技术有助于降低资源消耗，包括CPU周期和内存使用。这种优化确保了系统资源的有效利用，提高了整个系统的性能和可靠性。通过最小化资源开销，该发明使汽车系统能够在资源受限环境中更有效地运行。



> **1.**   **Detailed description of structure and function of the invention together with alternative embodiments. Drawings (block diagram, mechanical structure, flow charts etc.) The description and the drawings are better to be consistent** **and syncretic.**





> **1.**   **In which product or project will the invention be used and when will the invention be published?**






