# TCP/IP协议族
> TCP/IP协议族学习笔记

了解TCP/IP协议族，需要先学习OSI七层模型

### OSI七层参考模型

OSI参考模型（OSI）的全称是开放系统互连参考模型（Open System Interconnection Reference Model），它是由国际标准化组织ISO提出的一个网络系统互连模型。它是网络技术的基础，也是分析、评判各种网络技术的依据。

* `应用层(Application Layer)` 直接面向用户的一层，该层提供的应用程序和网络之间的接口，向用户提供服务。例如：http、https、FTP、SMTP、POP3、TELNET、SSH等。

    1. HTTP协议：（HyperText Transfer Protocol，超文本传输协议）是互联网上应用最为广泛的一种网络协议，所有的3w文件都必须遵循这个标准。

    2. FTP协议：（File Transfer Protocol，文件传输协议）用于网络上控制文件的双向传输，为server/client模式。

    3. SMTP协议：（Simple Mail Transfer Protocol，简单邮件传输协议）是一组用于邮件由源地址到目的地址传输的规则，控制邮件的中转方式。

    4. POP3协议：（Post Office Protocol-version3，邮局协议版本3）主要用于支持远程客户端管理服务器上的电子邮件。

* `表示层(Presentation Layer)` 处理来自应用层的数据和命令，主要解决用户信息的语法表示问题；例如加密解密、转换翻译、压缩解压缩。

* `会话层(Session Layer)` 用于不同机器上的用户之间建立会话及管理会话。

* `传输层(Transfer Layer)` 负责接收上一层的数据，在必要的时候把数据进行分割，并将这些数据交给网络层，并保证数据的有效到达，传输层协议包括TCP、UDP、SPX等。

* `网络层(Network Layer)` 用于控制子网的运行，如逻辑编址、分组传输、路由选择。网络层协议包括IP、RIP、OSPF等。

* `数据链路层(Datalink Layer)` 负责物理寻址，同时将原始比特流变为逻辑传输线路。数据链路层协议的代表包括STP、PPP、HDLC协议。

* `物理层(Physical Layer)` 为传输数据提供所需要的物理设备。包括了针脚、电压、线缆规范、集线器、中继器、网卡、主机适配器等

### TCP/IP协议族及TCP/IP四层模型

TCP/IP协议族是一个网络通讯模型，以及一整个网络传输协议家族，为互联网的基础通讯架构。因为这个协议家族的两个核心协议，包括`TCP(传输控制协议)`和`IP(网际协议)`，为这个家族中最早通过的标准。

TCP/IP参考模型分为四层，从上到下分别是：应用层、传输层、网络互连层、网络接口层。

* 应用层
  主要面向用户的交互层
  * 对应OSI模型为：应用层/表示层/会话层
  * 协议：HTTP、FTP、TFTP、SMIP、SNMP、DNS

* 传输层
  主要为两台主机上的应用程序提供端到端的通信。在TCP/IP协议族中，有两个互不相同的传输协议：`TCP(传输控制协议)`和`UDP(用户数据报协议)`。下面会进行详解
  * 对应OSI模型为：传输层
  * 协议：`TCP(传输控制协议)`和`UDP(用户数据报协议)`

* 网络层
  处理分组在网络中的活动，进行数据包装、寻址、路由和交换错误报文
  主要包括IP协议，IP协议是网络层上的主要协议。IP协议是不可靠的、无连接的。它仅提供最好的传输服务，必须有上层协议提供可靠性。不可靠是指它不保证IP数据成功的到达目的地。
  * 对应OSI模型为：网络层
  * 协议：ICMP、IGMP、IP

* 链路层
  有时也称作网络接口层，通常包括操作系统中的设备驱动程序和计算机中对应的网络接口卡。它们一起处理与电缆（或其他任何传输媒介）的物理接口细节。
  * 对应OSI模型为：数据链路层/物理层
  * 协议：底层网络协议,如ARP、RARP、IEEE 802.2

可以用一张图将OSI模型和TCP/IP模型对应起来
![Markdown](https://ws1.sinaimg.cn/large/69128027gy1foqidrrulrg20v41830yk.jpg)

### TCP传输控制协议

传输控制协议(Transmission Control Protocol)是一种面向连接的、可靠的、基于字节流的传输层通信协议

* TCP首部，最小为20字节
![Markdown](https://ws1.sinaimg.cn/large/69128027gy1foqil96hx4j20n50f8wf2.jpg)

* TCP通过"三次握手"建立连接。客户端发送请求建立连接；服务器收到请求，发送同意并请求与客户端建立连接；客户端收到请求，发送同意与服务器建立连接。

* TCP"四次握手"断开连接。客户端发送断开请求；服务器收到请求，发送同意断开连接的请求；服务器发送请求断开连接；客户端收到，发送同意断开连接。
![Markdown](https://ws1.sinaimg.cn/large/69128027gy1foqiqeecfvj20ob0r4abz.jpg)

### UDP用户数据报协议
用户数据报协议(User Datagram Protocol)又称使用者资料包协定，是一个简单的面向数据报的传输层协议,UDP为网络层以上和应用层以下提供了一个简单的接口。UDP的传递是**不可靠的**

* UDP首部
![Markdown](https://ws1.sinaimg.cn/large/69128027gy1foqj2vze4yj20j20910tn.jpg)

### 小记
TCP/IP协议族是计算机网络基础知识，是前端开发重要的前置技能

###### 参考资料
* [OSI七层模型详解](http://blog.csdn.net/yaopeng_2005/article/details/7064869)
