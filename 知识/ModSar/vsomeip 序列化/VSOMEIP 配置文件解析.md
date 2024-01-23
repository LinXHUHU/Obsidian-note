*'unicast'：主机系统的IP地址。

'*netmask'：用于指定主机系统子网的网络掩码。

 *'device' (optional)：如果指定，IP端点将绑定到此设备

 *'diagnosis'：用于构建客户端标识符的诊断地址（byte）。如果没有另外指定标识符，这个诊断地址分配给所有客户端中最重要的字节（例如通过预定义的客户端ID）。

*'diagnosis_mask'：诊断掩码（2字节）用于控制允许的最大诊断量ECU上的并发vsomeip客户端和客户端ID的起始值。

默认值为“0xFF00”，意思是客户端ID的最高有效字节保留用于诊断地址和客户端ID将以指定的诊断地址开始。最大客户端数为255，作为反转掩码的汉明权重是8（2^8=256-1（对于路由管理器）=255）。生成的客户端ID诊断地址为0x45的范围为0x4501到0x45ff。将掩码设置为“0xFE00”会将客户端ID范围加倍，将其设置为511个客户端倒置面罩的汉明重量增加1。有诊断地址在0x45中，当0x4500中的位8被屏蔽时，客户端ID的起始值为0x4401，这将产生0x4400到0x45ff的客户机ID范围。

*'network'：用于在一台主机上支持多个路由管理器的网络标识符。这设置会更改“/dev/shm”中共享内存段和“/tmp/”中的unix域套接字。默认为“vsomeip”，表示共享内存将被命名为“/dev/shm/vsomeip”，unix域套接字将被命名为`/tmp/vsomeip-$CLIENTID`

*'logging'：用于日志记录

　　**'level'：指定日志级别（有效值：_trace_, _debug_, _info_, _warning_,_error_, _fatal_）

　　**'console'：指定是否启用通过控制台的日志记录（有效值：_true，false_）

　　**'file'：log文件

　　　　***'enable'：指定是否应创建日志文件（有效值：_true，false_）。

　　　　***'path'：日志文件的绝对路径。

　　**'dlt'：指定是否启用诊断日志和跟踪（DLT）（有效值：_true，false_）。

 　　**'version'：配置vsomeip版本的日志记录

 　　　　***'enable'：启用或禁用vsomeip版本的循环日志记录，默认为true（有效值：_true，false_）

　　　　***'interval'：以秒为单位配置间隔以记录vsomeip版本。默认值为10。

　　**'memory_log_interval'：配置路由管理器记录其使用内存的时间间隔（以秒为单位）。当使用时，设置大于零的值将启用日志记录。

　　**'status_log_interval'：配置路由管理器记录其内部状态日志的时间间隔（以秒为单位）。设置大于零的值将启用日志记录。

*anchor:config-tracing[]'tracing'：配置跟踪，可选

　　**'enable'：指定是否启用对SOME/IP消息的跟踪（有效值：_true，false_）。默认值为_false_。如果启用了跟踪，消息将通过<traceconnector，Trace Connector>

　　**'sd_enable'：指定是否对SOME/IP服务发现消息进行跟踪已启用（有效值：_true，false_）。默认值为_false。

　　** 'channels (array)' (optional):包含指向DLT的通道,注意：您可以设置多个到DLT的通道，以便转发信息。

　　　　***'name':通道的名字

　　　　***'id'：通道的ID

　　 **'filters (array)' (optional)：消息的过滤器，只有经过过滤的消息才会被转发DLT

　　　　**'channel' (optional)：过滤后的消息转发到DLT的通道id。如果未指定任何通道，则使用默认通道（TC）。如果你想使用在多个不同的通道中进行筛选，可以提供一组通道ID。注意：如果使用多个通道的正滤波器，则相同的消息将被多次进入DLT

　　　　*** 'matches' (optional)：在跟踪中包含/排除消息的标准规范。

　　　　*** 'type' (optional)：

*'applications (array)'：包含使用此配置文件的主机系统的应用程序

　　 **'name'：应用程序的名称。

　　 **'id'：应用程序的id。通常其高位字节等于诊断地址。在这个低字节必须与零不同。因此，如果诊断地址为0x63，则有效值的范围从0x6301到0x63FF。也可以使用高字节的id值与诊断地址不同。

　　** 'max_dispatchers' (optional)：应用于执行应用程序回调的最大线程数。默认值为10

　　** 'max_dispatch_time' (optional)：应用程序回调最大阻塞时间，默认值为100ms。

　　** 'threads' (optional)：在应用程序内处理消息和事件的内部线程数。有效值为1-255。默认值为2。

　　** 'io_thread_nice' (optional)：内部线程处理消息和事件的良好级别。仅限POSIX/Linux。有关实际值，请参阅nice（）文档。

　　**'request_debounce_time' (optional)：指定request-service 消息发送到路由管理器的去抖动时间间隔（毫秒）。如果一个应用程序在短时间内请求多个服务向路由管理器发送消息的负载，以及来自路由管理器（包含请求服务的路由信息，如果可用）可以大幅减少。如果未指定，默认值为10ms。

　　**'plugins' (optional array)：

　　　　***'name'：插件的名称。

　　　　***'type'：插件的类型。（有效值 _application_plugin_）。应用程序插件扩展了应用程序级别的功能。通过vsomeip和基本应用程序状态（INIT/START/STOP）和can得到通知，基于这些通知，运行时可以访问标准的“应用程序”API。

　　** 'overlay' (optional)：包含覆盖特定配置元素的配置的路径（单播、网络掩码、设备、网络、诊断地址和掩码、服务发现）应用这允许从单个进程管理不同的网络地址。当编译时配置了ENABLE_CONFIGURATION_OVERLAYS才可用。

*`services` (array)：服务提供列表

　　**`service`：服务的id

　　**`instance`：服务实例的id。

　　**`protocol` (optional)：用于实现服务实例的协议。默认是is _someip_，如果提供了不同的设置，vsomeip不会打开指定的端口（服务器端）或未连接到指定端口（客户端）。因此此选项可用于让服务发现宣布一个正在运行的服务外部实现。

　　**`unicast` (optional)：主机服务实例的单播。注：如果需要使用外部服务实例，则需要单播地址，但服务发现被禁用。在这种情况下，提供的单播地址用于访问服务实例。

　　**`reliable`：指定与服务的通信分别是可靠的TCP协议用于通信。

　　 　　***`port`：TCP端点的端口。

　　　　***`enable-magic-cookies`:指定是否启用了magic Cookie（有效值：_true_，_false_）。

　　** `unreliable`：分别指定与服务的通信不可靠UDP协议用于通信（有效值：UDP端点的port）。

　　 **`events` (array)：包含服务的事件列表

　　　　***`event`：事件id

　　　　***`is_field`：指定事件是否为字段类型。字段是getter、setter和notification event的组合。至少包含一个getter、setter或notifier。通知程序发送一个事件传输更改时字段的当前值的消息。

　　　　***`is_reliable`：分别指定通信是否可靠，事件是否与TCP协议一起发送（有效值：_true_，_false_）。如果值为_false ，将使用UDP协议。

　　**`eventgroups` (array)：事件组列表

　　　　***`eventgroup`：事件组的id

　　　　***`events` (array)：事件id列表

　　　　***`multicast`：指定用于发布事件组的多播

　　　　　　****`address`：多播地址

　　　　　　****`port`：多播端口

　　　　 ***`threshold`：指定何时使用多播以及何时使用单播发送通知事件。此值必须设置为非负数。如果设置为零，则eventgroup的所有事件将通过单播发送。否则，只要订阅数低于阈值事件将通过单播发送，如果订阅数大于或等于阈值，将多播发送。这意味着，阈值为1将导致所有事件正在通过多播发送。默认值为0。

　　**`debounce-times` (object)：用于配置nPDU功能。这将在中详细描述<<npdu,vSomeIP nPDU feature>>.

　　 **`someip-tp` (object)：用于配置SOME/IP-TP功能。这里有一个例子<<someiptp, SOME/IP-TP>>.

　　　　 ***`service-to-client` (array)：包含从节点发送的响应、字段和事件的ID到通过 SOME/IP-TP 分段的远程客户端，如果超过UDP通信的最大消息大小且此处未列出ID否则，将丢弃消息。

　　　　***`client-to-service` (array)：如果超过UDP通信的最大消息大小，包含从节点发送请求的ID到一个通过 SOME/IP-TP 分段的远程服务。如果此处未列出ID且超过最大消息大小，消息将被丢弃。请注意，单播密钥必须设置为服务器的远程提供节点的IP地址，以使此设置生效。

`clients` (array)：用于连接特定服务的客户端端口。对于每个服务，一组端口用于可靠/不可靠的通信。vsomeip将占用列表空闲的端口。如果找不到空闲端口，连接将失败。如果

要求vsomeip连接到没有指定端口的服务实例，端口将由系统选择。这意味着用户已经确保此处配置的端口不会与端口重叠由IP堆栈自动选择。

 　　**`service`：

　　**`instance`:

　　它们一起指定端口配置应用于的服务实例。

　　 **`reliable` (array):用于与给定服务器进行可靠（TCP）通信的客户端端口列表服务实例。

 　　** `unreliable` (array):用于与给定服务器进行不可靠（UDP）通信的客户端端口列表服务实例。此外，还可以配置客户端范围之间的映射远程服务端口的端口和范围。（如果为特定服务/实例配置了客户端端口，则忽略端口范围映射）

　　**`reliable_remote_ports`:指定一系列可靠的远程服务端口

　　**`unreliable_remote_ports`:指定一系列不可靠的远程服务端口

　　 **`reliable_client_ports`:指定要映射到reliable_remote_ports范围的可靠客户端端口的范围

　　 **`unreliable_client_ports`:指定要映射到unreliable_remote_ports范围的不可靠客户端端口的范围

　　**`first`：指定端口范围的下限

　　** `last`：指定端口范围的上限

*`payload-sizes` (array)：数组以限制每个IP和端口允许的最大有效负载大小。如果不指定，允许的有效负载大小是无限的。数组中的设置仅影响TCP上的通信。限制本地有效负载大小可以使用max-payload-size-local。

　　**`unicast`：在客户端：远程服务的IP，其有效负载大小应为要有限度。在服务端：提供的服务的IP，其有效负载大小为接收和发送应该受到限制。

　　** `ports` (array)：其中包含成对的端口和有效负载大小的描述。

　　　　***`port`：在客户端：远程服务的端口，其有效负载大小应为要有限度。在服务端：提供的服务的IP，其有效负载大小为接收和发送应该受到限制。

　　　　***`max-payload-size`：在客户端：发送到客户端的消息的有效负载大小限制（字节）托管在预先指定的IP和端口上的远程服务。在服务端：接收和发送的消息的有效负载大小限制（以字节为单位）通过以前指定的IP和端口提供的服务。如果多个服务托管在同一个端口上，它们都会共享限制明确规定

`max-payload-size-local`：节点内部通信允许的最大有效负载大小（字节）。通过默认情况下，节点内部通信的有效负载大小是无限的。有可能通过此设置进行限制。

`max-payload-size-reliable`：TCP通信允许的最大有效负载大小字节。默认情况下，TCP通信的有效负载大小为无限的可以通过此设置进行限制。

`max-payload-size-unreliable`：通过某些/IP-TP进行UDP通信所允许的最大有效负载大小字节。默认情况下，通过某些/IP-TP通信的UDP有效负载大小为无限的可以通过此设置进行限制。此设置仅适用于一些启用/IP-TP的方法/事件/字段（否则UDP默认值为1400）字节（适用）。有关配置示例，请参见<<someiptp，SOME/IP-TP>>。

`endpoint-queue-limits` (array)：限制每秒缓存的传出消息的最大允许大小（以字节为单位）IP和端口（每个端点的消息队列大小）的数组。如果未另行规定允许的队列大小是无限的。此数组中的设置仅影响外部设置表达要限制本地队列大小`endpoint queue limit local`可以被利用。

　　**`unicast`：在客户端：为其发送队列大小的远程服务的IP请求应该受到限制。在服务端：提供的服务的IP，其队列大小为发送的响应应该是有限的。因此，这个IP地址是与通过网络顶层的“单播”设置指定的IP地址相同json文件。

　　**`ports` (array)：其中包含成对的端口和队列大小描述

　　　　***`port`：在客户端：远程服务的端口，在服务端：所提供服务的端口。

 　　　　***`queue-size-limit`：在客户端：发送到客户端的消息的队列大小限制（以字节为单位）托管在预先指定的IP和端口上的远程服务。在服务端：服务发送的响应的队列大小限制（字节）在以前指定的IP和端口上提供。如果多个服务托管在同一个端口上，它们都会共享限制明确规定。

* `endpoint-queue-limit-external`：设置以限制缓存传出消息的最大允许大小（以字节为单位）用于外部通信（每个端点的消息队列大小）。默认情况下外部通信的队列大小是无限的。它可以通过这个来限制背景在“endpoint queue limits”数组中进行的设置会覆盖此设置。

*`endpoint-queue-limit-local`：设置以限制缓存传出消息的最大允许大小（以字节为单位）用于本地通信（每个端点的消息队列大小）。默认情况下，队列节点内部通信的大小是无限的。它可以通过这个来限制设置。

*`buffer-shrink-threshold`：已处理消息的数量，其大小为分配的缓冲区用于在缓冲区的内存被释放之前处理它们释放并再次开始动态增长。此设置在以下情况下很有用：在这种情况下，只有一小部分的整体消息要大得多然后，剩余的部分和分配给处理它们的内存应该在一段时间内释放及时地。如果该值设置为零，则不会重置缓冲区大小，并且与最大的已处理邮件一样大。（默认值为5）。示例：设置为50。包含500字节的消息必须进行处理，缓冲区相应增长。在此消息之后，连续50次必须先处理小于250字节的消息，然后才能更改缓冲区大小减少，并再次开始动态增长。

* `tcp-restart-aborts-max`：设置以限制由于未完成的TCP握手而导致的TCP客户端终结点重新启动中止的次数。达到限制后，如果连接尝试仍处于挂起状态，则会强制重新启动TCP客户端终结点。

*`tcp-connect-time-max`：用于定义完成TCP客户端端点连接尝试之前的最长时间的设置。如果“tcp连接时间上限”已过，则如果连接尝试仍处于挂起状态，tcp客户端终结点将强制重新启动。

 *`udp-receive-buffer-size`：指定用于存储的套接字接收缓冲区（“SO_RCVBUF”）的大小UDP客户端和服务器端点（字节）。（默认值：1703936）

*`internal_services` (optional array)：指定纯内部服务实例的服务/实例范围。vsomeip使用此信息来避免发送查找服务消息当客户端请求不可用的服务时，通过服务发现-例子它可以在服务/实例级别或服务级别上完成仅包含0x0000-0xffff中的所有实例。

　　**`first`：内部服务范围的最低入口。

　*　　　***`service`：内部服务范围内以十六进制表示的最低服务ID。

　　　　***`instance` (optional)：内部服务实例范围中以十六进制表示的最低实例ID。如果未指定，则最低实例ID为0x0000。

　　**`last`：内部服务范围的最高入口。

　　　　***`service`：内部服务范围中以十六进制表示的最高服务ID。

　　　　 ***`instance` (optional)：内部服务实例范围中以十六进制表示的最高实例ID。如果未指定，则最高实例ID为0xFFFF。

*`debounce` (optional array)：外部设备发送的事件/字段将转发给仅当可配置函数的计算结果为true时，应用程序才会启动。这个函数检查事件/字段有效负载是否已更改，以及自上次转发以来已过指定的时间间隔。

　　**`service`：托管要取消公告的事件的服务ID。

　　 **`instance`：承载要取消公告的事件的实例ID。

　　**`events`：应根据以下内容取消公告的一系列事件配置选项。

 　　　　***`event`：事件ID

　　　　 *******`on_change`：指定是否仅对事件进行预告有效数据是不是变了。 (valid values: _true_, _false_).

　　　　***`ignore`：具有给定位掩码的有效负载索引数组（可选）在有效载荷变化评估中被忽略。不能指定索引/位掩码对，只能定义paylaod索引在评估中应忽略这一点。

　　　　　　 ****`index`：要使用给定位掩码检查的有效负载索引

　　　　　　 ****`mask`：1字节位掩码应用于给定有效负载索引的字节。示例掩码：0x0f忽略给定索引处字节低半字节的有效负载变化

　　　　***`interval`：指定是否应根据经过的时间间隔取消对事件的播音。(valid values: _time in ms_, _never_).

　　　　***`on_change_resets_interval_` (optional)：指定检测到负载变化时是否重置间隔计时器。(valid values: _false_, _true_).

 *`routing`：负责路由的应用程序的名称。

 *`routing-credentials`：充当路由管理器的应用程序的UID/GID。(如果使用_check_credentials_设置为_true_以成功检查在connect上传递的路由管理器凭据，则必须指定凭据检查）

　　**`uid`:路由管理器UID

　　 **`gid`:路由管理器GID

* `shutdown_timeout`:配置本地客户端等待确认的时间（毫秒）他们在关机期间从路由管理器注销。默认为5000毫秒。

*`warn_fill_level`:路由管理器会定期检查发送缓冲区的填充级别，以确保其正常运行客户。该变量以百分比形式定义了导致正在记录警告。默认为67。

* `service-discovery`:包含与主机应用程序的服务发现相关的设置。

　　 **`enable`:指定服务发现是否已启用（valid values: _true_,_false_)。默认值为_true_。

　　**`multicast`:将发送服务发现消息的多播地址,默认值为_224.0.0.1。

　　 **`port`：服务发现的端口。默认设置为_30490 _。

　　 **`protocol`：用于发送服务发现消息的协议(valid values: _tcp_, _udp_)。默认设置为_udp_u。

　　 **`initial_delay_min`：第一次提供信息前的最小延迟。

　　 **`initial_delay_max`：首次提供信息前的最大延迟。

　　**`repetitions_base_delay`：在重复阶段发送要约消息的基本延迟。

　　** `repetitions_max`：在重复阶段的服务范围内提供服务的最大重复次数。

　　**`ttl`：提供的服务以及已使用的服务和事件组的条目的生存期

　　** `ttl_factor_offers` (optional array)：保存传入远程报价的修正系数的数组。如果一个值为服务实例指定的TTL字段大于1相应的服务条目将乘以指定的系数。示例：收到服务要约时，TTL为3秒，TTL为系数设置为5。远程节点停止提供服务，而不发送停止报盘信息。服务将在15秒后过期（标记为不可用）在收到最后一份报价后。

　　　***　`service`：服务的id。

　　　　***`instance`：服务实例的id。

　　　　***`ttl_factor`：TTL校正系数

　　**`ttl_factor_subscriptions` (optional array)：保存传入远程订阅的校正因子的数组。如果为服务实例指定大于1的值，即相应的eventgroup条目将与指定的因子相乘+示例：收到对所提供服务的远程订阅时，TTL为3秒，TTL系数设置为5。远程节点停止重新订阅不发送StopSubscribeEventgroup消息的服务。订阅将然后在收到最后一次重新预订后15秒过期。

　　　　***`service`：服务的id。

　　　　***`instance`：服务实例的id。

　　　　***`ttl_factor`：TTL校正系数

　　**`cyclic_offer_delay`：主阶段中OfferService消息的周期。

 　　**`request_response_delay`：单播消息到多播消息的最小延迟提供服务和活动组。

　　**`offer_debounce_time`：堆栈在进入新服务之前收集新服务的时间重复阶段。这可以用来减少在启动期间发送消息。默认设置为500毫秒。

 //Watchdog

 *anchor:config-watchd*og[]`watchdog` (optional)：看门狗定期向所有已知的本地客户端发送ping。如果客户机在配置的时间内没有响应，则会出现大量的PONG看门狗注销此应用程序/客户端。如果未配置，则不会激活看门狗。

　　**`enable`：指定是启用还是禁用看门狗(valid values: _true, false_), (default is _false_).

　　**`timeout`：指定在ping时启动看门狗的超时时间（毫秒）当地客户在这段时间内没有用乒乓球回答。（有效值：2-2^32），（默认值为5000毫秒）。

　　 **`allowed_missing_pongs`：指定允许丢失的乒乓球数量。（有效值：_1-2^32_uu），（默认值为_3_upongs）。

//CAPI-Selective Broadcasts support

*anchor:config-supports_selective_broadcasts[]`supports_selective_broadcasts` (optional array)：该节点允许添加支持CAPI选择性广播功能的IP地址列表。如果未指定，则无法使用该功能，堆栈的订阅行为与正常事件。

　　**`address`：指定支持“选择性”功能的IP地址（IPv4或IPv6表示法）。可以配置多个地址。

//Security

*anchor:config-policy[]`security` (optional):如果指定，凭证传递机制将被激活。但是，只要_check _credentials uu未设置为_true u，就不会进行凭证或安全检查，但如果指定了安全标签，则必须配置路由管理器客户端ID，并且不应设置为0x6300。如果_check_credentials_uu设置为_true_u，则需要使用_routing-credentials_u标记指定路由管理器UID和GID。

　　**`check_credentials` (optional):指定安全检查是否处于活动状态。这包括对connect的凭据检查，以及在follow中配置的所有策略检查。(valid values: _true, false_), (default is _false_).

　　**`allow_remote_clients` (optional):指定是否允许将传入的远程请求/订阅发送到本地代理/客户端。如果未指定，则默认情况下允许接收所有远程请求/订阅。（有效值为'true'和'false'）

　　** `policies` (array):指定安全策略。每个策略至少需要指定“允许”或“拒绝”。

　　　　***`credentials`:指定将应用安全策略的凭据。如果_check_credentials_uu设置为_true_u，则需要正确指定本地应用程序的凭据，以确保本地套接字身份验证能够成功。

　　　　　　 ****`uid`:将客户端应用程序的LINUX用户id指定为十进制数。作为通配符，可以使用“any”。

 　　　　　　**** `gid`：将客户端应用程序的LINUX组id指定为十进制数。作为通配符，可以使用“any”。

　　　　　　****`allow` / `deny` (optional)：指定策略允许还是拒绝LINUX用户和组ID。

.`uid`（数组）指定LINUX用户ID的列表。这些可以指定为十进制数或范围。范围由第一个和最后一个有效id指定（参见下面的示例）。

 .`gid`（数组）指定LINUX组ID的列表。这些可以指定为十进制数或范围。范围由第一个和最后一个有效id指定（参见下面的示例）。

　　　　*** `allow` / `deny`：此标签指定_allow_uuuu或_deny_uuu，具体取决于所需的白名单或黑名单。因此，不允许在一个策略中指定“允许”和“拒绝”条目。有了_allow u，可以做什么的白名单，这意味着一个空的_allow u标签意味着一切都被拒绝。有了_deny u，允许做的事情就可以被列入黑名单，这意味着一个空的_deny u标签意味着一切都是允许的。

　　　　　　**** `requests` (array)：指定允许/拒绝使用上述凭据的上述客户端应用程序与之通信的一组服务实例对。

. `service`：为请求指定服务

. `instance` (deprecated)：指定请求的实例_作为通配符，可以使用“any”，这意味着从实例ID 0x01到0xFFFF的范围这也意味着方法ID的范围从0x01到0xFFFF。

. `instances` (array)：指定一组允许/拒绝与之通信的实例ID和方法ID范围对。如果下面的'ids'标记未用于指定方法ID级别上的允许/拒绝请求，则还可以仅指定一组允许/拒绝请求的实例ID范围，类似于允许/拒绝“报价”部分。如果未指定方法ID，则默认情况下，允许/拒绝的方法的范围为0x01到0xFFFF。

.. `ids`： 指定一组允许/拒绝与之通信的实例ID范围。还可以将单个实例ID指定为数组元素，而无需给出上限/下限。作为通配符，可以使用“any”，这意味着从实例ID 0x01到0xFFFF的范围。

first` - The lower bound of the method range.

`last` - The upper bound of the method range.

　　　　　　**** `offers` (array)：指定一组服务实例对，客户端应用程序使用上述凭据允许/拒绝提供这些服务实例对。

. `service`：指定offer的服务

. `instance` (deprecated)：指定offer的instance，作为通配符，可以使用“any”，这意味着从实例ID 0x01到0xFFFF的范围。

 `instances` (array)：指定一组实例ID范围，客户端应用程序使用上述凭据允许/拒绝提供这些范围。还可以将单个实例ID指定为数组元素，而无需给出上限/下限。作为通配符，可以使用“any”，这意味着从实例ID 0x01到0xFFFF的范围。

.. `first`：实例范围的下限。

.. `last`：实例范围的上限
