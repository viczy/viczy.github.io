---
layout: post
title: "TCP/IP协议"
date: 2015-03-08 10:51:54 +0800
comments: true
categories: 
---

##OSI

层                    |  数据格式                  |  典型设备
:-------------------  | :-----------------------: | :----------:
应用层(Application)    |                           | 
表现层(Presentation)   |                           |
会话层(Session)        |                           |
传输层(Transport)      | 组成数据段(Segment)        |  
网络层(Network)        | 分割组成数据包(Packet)      |  路由器
数据链路层(DataLink)   |  比特信息封装成数据帧(Frame)  |  网桥，网卡，交换机
物理层(Physical)       | 传输比特流(bit)             |  中继器，集线器，线缆与光纤

<br />

TCP/IP | OSI                 | 相关协议与标准
:----- | :-----------------: | :-------------------------:
应用层  | 应用层，表现层，会话层 |  HTTP,FTP,SMTP,POP3,NFS,SSH
传送层  | 传送层               | TCP,UDP
网络层  | 网络层               | IP,ICMP
链接层  | 链路层，物理层        | LAN,ARP,WAN

<br />

####应用层
网络服务与使用者应用程序间的一个借口

####表现层
数据表示，数据安全，数据压缩

####会话层
建立，管理和终止会话

####传送层
用一个寻址机制来标识一个特定的应用程序

####网络层
基于网络层地址（ip地址）进行不同网络系统间的路径选择

####链接层
在物理层上建立，撤销，标识逻辑链接和链接复用以及差错校验等功能。通过使用接受系统的硬件地址或物理地址来寻址

####物理层
建立，维护和取消物理连接

##ARP
地址解析协议（Address Resolution Protocol），其基本功能为通过目标设备的IP地址，查询目标设备的MAC地址，以保证通信的顺利进行。它是IPv4中网络层必不可少的协议，不过在IPv6中已不再适用，并被邻居发现协议（NDP）所替代。

####ARP报文格式

0                | 7                                | 15                 | 31
:----------------| ---------------------:           | :----------------- | --------------------------------------:                       
                 | 硬件类型(Hardware Type)           |                    | 协议类型(Protocol Type)
硬件长度地址(HLEN) | 协议长度(PLEN)                    |                    | 操作类型(Operation)
                 |                                  |                    | 发送方硬件地址(Sender HA(Byte0~3))                      
                 | 发送方硬件地址(Sender HA(Byte0~3)) |                    | 发送方ip地址(Sender IP(Byte0~1))
                 | 发送方ip地址(Sender IP(Byte2~3))   |                    | 接收方硬件地址(Target HA(Byte0~1))
                 |                                  |                    | 接受方硬件地址(Target HA(Byte2~5))
                 |                                  |                    | 接收方ip地址(Target HA(Byte0~3))
                 
<br />

#####硬件类型
指明了发送方想知道的硬件接口类型，以太网的值为1；

#####协议类型
指明了发送方提供的高层协议类型，IP为0800（16进制）；

#####硬件地址长度和协议长度
指明了硬件地址和高层协议地址的长度，这样ARP报文就可以在任意硬件和任意协议的网络中使用；

#####操作类型
用来表示这个报文的类型，ARP请求为1，ARP响应为2，RARP请求为3，RARP响应为4；

#####发送方硬件地址（0-3字节）
源主机硬件地址的前3个字节；

#####发送方硬件地址（4-5字节）
源主机硬件地址的后3个字节；

#####发送方IP地址（0-1字节）
源主机硬件地址的前2个字节；

#####发送方IP地址（2-3字节）
源主机硬件地址的后2个字节；

#####目标硬件地址（0-1字节）
目的主机硬件地址的前2个字节；

#####目标硬件地址（2-5字节）
目的主机硬件地址的后4个字节；

#####目标IP地址（0-3字节）
目的主机的IP地址。


##TCP
传输控制协议（英语：Transmission Control Protocol, TCP）是一种面向连接的、可靠的、基于字节流的传输层通信协议，由IETF的RFC793定义。在简化的计算机网络OSI模型中，它完成第四层传输层所指定的功能，用户数据报协议（UDP）是同一层内另一个重要的传输协议。

####TCP报文格式

偏移     | Byte0~3               | 4~9                  | 10~15                 | 16~31
:------ | --------------------: | ------------------:  | -------------------: |---------------------------:
0       |                       |                      | 源端口号(Source Port) | 目的端口号(Destination Port)
32      |                       |                      |                      | 序号(Sequence Number)
64      |                       |                      |                      | 确认号(Acknowledgemen Number)
96      | 数据偏移(Date Offest)  | 保留(Reserved)        | 标示符                | 窗口大小(Window)
128     |                       |                      | 检验码(Checksum)      | 紧急数据指针(Urgent Pointer)
160     |                                                                     | 选项(options)
192+    |                                                                     | 数据(Data)

<br />

#####源端口号
本地通信端口

#####目的端口号
远地通信端口

#####序号
数据部分第一字节的序列号

#####确认号
表示本地希望接收得下一个数据字节的序号

#####数据偏移
该TCP段中数据起始的位置

#####保留
该域保留，置位为0

#####标示符

* URG:紧急数据指针有效标志，指示本段中包含紧急数据
* ACK:确认标志，指示段中确认号有效
* PST:复位连接标志，指示本段为复位段
* RSH:PUSH操作标志
* SYN:建立同步连接标志
* FIN:本地数据发送结束，终止链接标志

#####窗口大小
本地接受窗口（接受缓冲区）大小

#####校验和
包括TCP报头和数据在内的校验和

#####紧急数据指针
指示从发送数据序列号开始到紧急数据之后的第一个字节偏移

#####选项
提供任选服务

#####数据
保证TCP报头以32位为边界对齐


##IP
网际协议（Internet Protocol），是用于报文交换网络的一种面向数据的协议。

IP是在TCP/IP协议中网络层的主要协议，任务是仅仅根据源主机和目的主机的地址传送数据。为此目的，IP定义了寻址方法和数据报的封装结构 。第一个架构的主要版本，现在称为IPv4，仍然是最主要的互联网协议，尽管世界各地正在积极部署IPv6。

####IP报文格式

0            | 3             | 7                  | 15        | 18              | 31
:----------- | ------------: | -----------------: | --------: | --------------: | ---------------------------------:
版本         | 标头长度        | 服务类型            |           |                 | 封包总长
             |               | 识别码              | 旗标       |                 | 分割定位
             | 存活时间       | 协定                |           |                 | 标头检验值
             |               |                    |           |                 | 源地址
             |               |                    |           |                 | 目的地址
             | 可选           |                    |           |                 | 填充
             |               |                    |           |                 | 数据

<br />
             
#####版本（Version）
IP规格版本，目前IP多为版本4，所以这里通常为0x4

#####标头长度（Internet Header Length）
在Option和Padding没有设定的情况下，标头只有5行的长度，每行4Byte，共20Byte；所以这里通常为0x14

#####服务类型（Type of Service）
IP封包在传送过程中的服务类型，由8个bit组成，每组bit组合代表不同的意思。

* 000.....  Routine       设定IP顺序，预设为0，否则数值越高越优先
* ...0....  Delay         延迟要求，0为正常值，1为低要求     
* ....0...  Throughput    通讯量要求，0为正常值，1为高要求
* .....0..  Reliability   可靠性要求，0为正常值，1为高要求
* ......00  Not Used      未使用

#####封包总长（Total Length）
通常以Byte做单位来表示该封包的总长度，此数值包括标头和数据的总和

#####识别码 （Identification）
每一个IP封包都有一个16bit的唯一识识别码。当程式产生的数据要通过网络传送时，都会在传送层被拆散成封包形式发送，当封包要进行重组的时候，就是依据这个ID。

#####旗标（Flag）
这是当封包在传送过程中进行最佳组合时使用的3个bit的识别记号。

* 000.  当此值为0的时候，表示目前未被使用。
* .0..  当此值为0的时候，表示封包可以被分割，若为1则不能被分割
* ..0.  当上一个值为0时，此值为0就表示该封包是最后一个封包，如果为1则表示其后还有被分割的封包

#####分割定位（Fragment Offset）
当一个大封包在经过一些传输单位（MTU）较小的路径时，会被切割成碎片（fragment）再进行传送（这个切割和传送层的打包有所不同，它是由网络层决定的）。由于网络情况或其他因素影响，其抵达顺序并不会和当初切割顺序一致的。所以当封包进行切割的时候，会为各片段做好定位记录，如果封包没有被切割，那么值为0

#####存活时间（Time To Live）
当一个封包被赋予TTL值，TTL是以hop为单位，没经过一个router就减一，如果封包TTL值被降为0的时候，就会被丢弃。这样，当封包在传送过程中由于某些原因而未能抵达目的地的时候，就可以避免其一直充斥在网络上面。

#####协定（Protocol）
这里指的是该封包所使用的网络协议类型。各协议的代号如下：

* ip      0       IP              # internet protocol, pseudo protocol number
* icmp    1       ICMP            # internet control message protocol
* igmp    2       IGMP            # Internet Group Management
* ggp     3       GGP             # gateway-gateway protocol
* ipencap 4       IP-ENCAP        # IP encapsulated in IP (officially ``IP'')
* st      5       ST              # ST datagram mode
* tcp     6       TCP             # transmission control protocol
* egp     8       EGP             # exterior gateway protocol
* pup     12      PUP             # PARC universal packet protocol
* udp     17      UDP             # user datagram protocol
* hmp     20      HMP             # host monitoring protocol
* xns-idp 22      XNS-IDP         # Xerox NS IDP
* rdp     27      RDP             # "reliable datagram" protocol
* iso-tp4 29      ISO-TP4         # ISO Transport Protocol class 4
* xtp     36      XTP             # Xpress Tranfer Protocol
* ddp     37      DDP             # Datagram Delivery Protocol
* idpr-cmtp       39      IDPR-CMTP       # IDPR Control Message Transport
* rspf    73      RSPF            #Radio Shortest Path First.
* vmtp    81      VMTP            # Versatile Message Transport
* ospf    89      OSPFIGP         # Open Shortest Path First IGP
* ipip    94      IPIP            # Yet Another IP encapsulation
* encap   98      ENCAP           # Yet Another IP encapsulation


#####标头检验值（Header Checksum）
这个数值主要是用来检错用的，用以确保封包被正确无误的接收到。如果一切无误，就会发出确认信息，表示接收正常。

#####源地址（Source IP Address）
发送端IP地址。

#####目的地址（Destination IP Address）
接收端IP地址。

#####可选&填充（Options&Padding）
Options长度不定，可用来扩充功能。
Padding是为了让表头刚好是4Byte的倍数。

#####数据（Data）

##ICMP
ICMP（Internet Control Message Protocol）是Internet控制报文协议。它是TCP/IP协议族的一个子协议，用于在IP主机、路由器之间传递控制消息。控制消息是指网络通不通、主机是否可达、路由是否可用等网络本身的消息。这些控制消息虽然并不传输用户数据，但是对于用户数据的传递起着重要的作用。

####ICMP报文格式

ICMP报头从IP报头的第160位开始（例外：除非使用了IP报头的可选部分）

0            | 7                   | 15                              | 31
:----------  | ------------------: | ------------------------------: | ----------------------------------------:
类型          | 代码                |                                 | 检验和
             | 标识符               |                                 | 序列号  
             |                     |                                 | 选项
<br />
             
#####类型（type）
ICMP的类型

#####代码（code）
进一步分割ICMP的类型；

type | code | description
:--: | :--: | :-----------------------------------------------------------
0    | 0    | Echo Reply —— 回显应答（Ping 应答）
3    | 0    | Network Unreachable —— 网络不可达
3    | 1    | Host Unreachable —— 主机不可达
3    | 2    | Protocol Unreachable —— 协议不可达
3    | 3    | Port Unreachable —— 端口不可达
3    | 4    | Fragmentation needed but no frag bit set —— 需要进行分片但设置不分片比特
3    | 5    | Source routing failed —— 源站选路失败
3    | 6    | Destination network unknown —— 目的网络未知
3    | 7    | Destination host unknown —— 目的主机未知
3    | 8    | Source host isolated（obsolete）—— 源主机被隔离（作废不用）
3    | 9    | Destination network administratively prohibited —— 目的网络被强制禁止
3    | 10   | Destination host administratively prohibited —— 目的主机被强制禁止
3    | 11   | Network unreachable for TOS——由于服务类型TOS，网络不可达
3    | 12   | Host unreachable for TOS——由于服务类型TOS，主机不可达
3    | 13   | Communication administratively prohibited by filtering——由于过滤，通信被强制禁止
3    | 14   | Host precedence violation——主机越权
3    | 15   | Precedence cutoff in effect——优先中止生效
4    | 0    | Source quench——源端被关闭（基本流控制）
5    | 0    | Redirect for network——对网络重定向
5    | 1    | Redirect for host——对主机重定向
5    | 2    | Redirect for TOS and network——对服务类型和网络重定向
5    | 3    | Redirect for TOS and host——对服务类型和主机重定向
8    | 0    | Echo request——回显请求（Ping请求）
9    | 0    | Router advertisement——路由器通告
10   | 0    | Route solicitation——路由器请求
11   | 0    | TTL equals 0 during transit——传输期间生存时间为0
11   | 1    | TTL equals 0 during reassembly——在数据报组装期间生存时间为0
12   | 0    | IP header bad (catchall error)——坏的IP首部（包括各种差错）
12   | 1    | Required options missing——缺少必需的选项
13   | 0    | Timestamp request (obsolete)——时间戳请求（作废不用）
14   |      | Timestamp reply (obsolete)——时间戳应答（作废不用）
15   | 0    | Information request (obsolete)——信息请求（作废不用）
16   | 0    | Information reply (obsolete)——信息应答（作废不用）
17   | 0    | Address mask request——地址掩码请求 
18   | 0    | Address mask reply——地址掩码应答


<br />

#####检验和（checksum）
这个字段包含有从ICMP报头和数据部分计算得来的，用于检查错误的数据，其中此校验码字段的值视为0。

#####标识符（Identifier）
这个字段包含ID值，在Echo Reply 类型的消息中要返回这个字段。

#####序列号（sequence）
这个字段包含一个序号，同样要在echo reply类型的消息中要返回这个字段。

#####选项
可无。


####参考资料
* <http://www.study-area.org/network/networkfr.htm>
* <http://zh.wikipedia.org/wiki/TCP/IP%E5%8D%8F%E8%AE%AE%E6%97%8F>
