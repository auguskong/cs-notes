
RFC 1180 TCP/IP Tutorialhttps://tools.ietf.org/html/rfc1180Basic Logic Structure 
![img](https://lh3.googleusercontent.com/XjAidl6OK2-_CJ-pv9MDIAOisGkfbuTpir6n303KdB4t5Z1gQ9NrLG6OB8f_Xl5eEVO2jkgtE7gr68hCb2LoISxptnoDkzs6Ai8ztS6-EDHDiOr5InA0Vfe3cQ4JOFuI7jcfG1rR)



The "o" is the transceiver. The "*" is the IP address The"@" is the Ethernet address

【不同的命名本质上都是data】The name of a unit of data that flows through an internet is **dependent upon where it exists in the protocol stack**. on an Ethernet - Ethernet frame; between the Ethernet driver and the IP module - a IP packet; between the IP module and the UDP module - a UDP datagram;between the IP module and the TCP module - a TCP segment (more generally, a transport message); in a network application - an application message.
A driver is software that communicates directly with the network interface hardware. A module is software that communicates with a driver, with network applications, or with another module.
![img](https://lh5.googleusercontent.com/Ek7bk0g4X5HMM_GhuKG-4ct82tsmtF2J0OJwkdbzCLWK5ORh2d8o0mfoPj_O21NhoSj6_HzmHWRq_sRSB30b65HRv-HpOUGH15UquzgQ9HIc5Xo9h7CZwIKlcJRsiCDER5GKxp9J)
反向流通(Ethernet -> Application) 的时候: Ethernet frame -> (type field) IP OR ARP -> (protocol field) -> TCP OR UDP -> (port field) -> which application 
正向流通(Application -> Ethernet) 的时候 **路线唯一**: The downwards multiplexing is simple to perform because from each starting point there is only the one downward path; each protocol module adds its header information so the packet can be de-multiplexed at the destination computer.
ARP: Address Resolution Protocol IP: Internet Protocol 
ARP 和 IP 是并列的两个东西? ARP is used to translate IP addresses to Ethernet addresses. The translation is done only for outgoing IP packets, because this is when the IP header and the Ethernet header are created.![img](https://lh4.googleusercontent.com/-iGxTIQg80GaJDrDB5ymUcBpwfEF8WfvoaksCSe3kUJaV_-HCP6vu_rqrr4Veo2DfERGkBFs_-PMJv0jPObHN-oePu_xxwu-NBU61Y8WH531pUzfPd7q4Y1P9C4i5u744KG5cUeY)The IP address is selected by the network manager based on the location of the computer on the internet. When the computer is moved to a different part of the internet, its IP address must be changed. The Ethernet address is selected by the manufacturer based on the Ethernet address space licensed by the manufacturer. When the Ethernet hardware interface board changes, the Ethernet address changes.



![img](https://lh3.googleusercontent.com/pbXTAvzXd_NKwk_He1xbcDLkL_SQPevb4rwyG8y4nZ2cyzFUKmVZ05vY1lpcT3sMnSxx0itbd6_yqpquxoYJfAILtT2aSCvUJ8fw2xKakJs2eERatMvBnqMCIrIa8TC2bmgra4Hc)![img](https://lh5.googleusercontent.com/vxhA-wyqo1JVgP1LjDTAAGbuiqylCfSLkpeW0QL6gKKsoNPhDmjPZ64mESWDLRQI6Vc7dmBM7_OR3tKTrCN4ZvrQgXnCIHRSVPmfKD63lLb3hDjhk4jbzKoA_WOYHRn25yQ087hx)

![img](https://lh3.googleusercontent.com/Q5qwVmMsnYUMHakPvemOxy5_68NRwTQX2BaSzvr0ZUWOdeu3TKJCOwtl91YGk7xYVZejJjXhsor8Moa5HJ4hr2ZXWuYaDikku-mlG4BHDwLYzT7NdFpm1UfI38TMfTpQfRPgb54w)forward IP packet: 将IP包重定向 

什么情况下会需要用到 2 IP address ? AWS EC2 instance? 谁来为新电脑提供IP Address ? Virtualization 虚拟主机和IP address的关系 
When sending out an IP packet, how is the destination Ethernet address determined?ARP translate ARP 最开始如何建的？ Broadcast to every computer in the network 
How does IP know which of multiple lower network interfaces to use when sending out an IP packet?The IP module is central to internet technology and the essence of IP is its route table. IP uses this in-memory table to make all decisions about routing an IP packet.

一根网线就是一个network ?? 
\5. Internet Protocol 


Each computer has an IP address assigned to the IP interface by the network manager, who also has assigned an IP network number to the Ethernet. 这句话中的IP address assigned to the IP interface 怎么理解? 由network manager 随机选择一个IP address ? 
route table 
How does a client on one computer reach the server on another?
Why do both TCP and UDP exist, instead of just one or the other?
What network applications are available?Routing
Direct Routing: 同一根网线(WiFi) 连着的Host

5.2 Indirect Routing: 需要通过Router进行中转的 The figure below is a more realistic view of an internet. It is composed of **3 Ethernets** and **3 IP networks** connected by **an IP-router** called computer D. **Each IP network has 4 computers**; each computer has its own IP address and Ethernet address.
![img](https://lh3.googleusercontent.com/BockuH_Q4sNzvGbR2Zmp4AoUNOmFBHsa8un1blcDJMl8yyNgNVO5GtYkwXxkfNaUM8ZlxDV2dJdjwYTH7Ghy0sHuqPEK1DHTQSLzD1s4CCLYp22D2sbswryXXTnt9Nd8mZwWkNDJ)![img](https://lh4.googleusercontent.com/cNKN0IK8TwKTVD1rjVdpW0jeGx_cT-gfvj5k3xapaF44o04PSwBfLu5zLzDr3y7ILjSg_Yo_VwTY5GCSTUPKbOvv0Tmh7Lcki66cMn5vVXUm0aeV-ps5NYQtZXw2CY42bN-lSSqv)

![img](https://lh3.googleusercontent.com/RWJ3Tp3DUIKH0c8deN2RTKQwFcynyL-NrxLISjblrNxnCkS6hmJxTpzmxQ_FFxQmVxou4lLgzd9NJ-IgUHrMUBtGLMb3pLob0DYZ3L8ca4KHXbTK8N2WFYfwUzaCAGk6Nx1uOLLG)Ethernet frame![img](https://lh6.googleusercontent.com/DEGwPzCdK88GGQGbs7r3vRvT1sDcklJ3Lmdwg9CW0yGO6BhWx3pL_00j80xlPFdfbWOxg2XwqI1OgFqBiPzljrDZNzOVWo3qvAhVgabhXi2QLosKxGc4Y5QNNaWMjj5WpyvkMy00)
5.3 IP Module Routing Rule
5.4 IP Address
The network manager assigns IP addresses to computers according to the IP network to which the computer is attached.
IP address: network number + computer number(host number) 
IP address IP network Router MAC address 怎么区分? 

[**5.5**](https://tools.ietf.org/html/rfc1180#section-5.5) **Names**
就是现在的域名? People refer to computers by names, not numbers. A computer called alpha might have the IP address of 223.1.2.1. For small networks, this name-to-address translation data is often kept on each computes in the "hosts" file.
[**5.6**](https://tools.ietf.org/html/rfc1180#section-5.6) **IP Route Table**
How does IP know which lower network interface to use when sending out an IP packet? It looks it up in the route table using a search key of the IP network number extracted from the IP destination address. 

[**5.7**](https://tools.ietf.org/html/rfc1180#section-5.7) **Direct Routing Details**
[**5.8**](https://tools.ietf.org/html/rfc1180#section-5.8) **Direct Scenario**
**![img](https://lh4.googleusercontent.com/6X4kofPC1rIiXLH6uvXDT1RaBw9DPgsruYjbuHrq2NyRjAYqWEU4QT9Hmx2ZIzlP-dgoCDJ_NnBaGBPHRlq2VMeVUb0gk6W3X2JcBm8EU7iuQdzVm2HDVDkWqFgZhgarMKi3yab0)**
[**5.9**](https://tools.ietf.org/html/rfc1180#section-5.9) **Indirect Routing Details**![img](https://lh4.googleusercontent.com/Y2e55roCOBUvDYaECD0TM9JMfx2S-a0pwSNfUIHtTTkQMmMVp1V1tm49K21fLINA-5HRd-kEB3qorx7La9qiC_ce6FWuisW7dIbBvithz1j4Zs2T-sY8sXVW0fOCNl6ds-s5ryQq)

[**5.10**](https://tools.ietf.org/html/rfc1180#section-5.10) **Indirect Scenario**

[**5.11**](https://tools.ietf.org/html/rfc1180#section-5.11) **Routing Summary**
When an IP packet travels through a large internet it may go through many IP-routers before it reaches its destination. The path it takes is not determined by a central source but is a result of consulting each of the routing tables used in the journey. Each computer defines only the next hop in the journey and relies on that computer to send the IP packet on its way.


[**6**](https://tools.ietf.org/html/rfc1180#section-6)**. User Datagram Protocol**

UDP is a connectionless datagram delivery service that does not guarantee delivery. UDP does not maintain an end-to-end connection with the remote UDP module; it merely pushes the datagram out on the net and accepts incoming datagrams off the net.
UDP adds two values to what is provided by IP. 1. multiplexing of information between applications based on port number. 2. a checksum to check the integrity of the data.

[**6.1**](https://tools.ietf.org/html/rfc1180#section-6.1) **Ports**
[**6.2**](https://tools.ietf.org/html/rfc1180#section-6.2) **Checksum**If the checksum is zero, it means that checksum was not calculated by the sender and can be ignored.




[**7**](https://tools.ietf.org/html/rfc1180#section-7)**. Transmission Control Protocol**

使用TCP的application protocol: TELNET(port 23), FTP(File Transfer Protocol) TCP offers a **connection-oriented** byte stream, instead of a connectionless datagram delivery service. TCP **guarantees delivery**, whereas UDP does not.

TCP 需要先在两个port之间建立连接
When the application first starts using TCP, the TCP module on the client's computer and the TCP module on the server's computer start communicating with each other.These two end-point TCP modules contain state information that defines a virtual circuit.
The virtual circuit is full duplex; data can go in both directions simultaneously.
TCP 读取随机
TCP packetizes the byte stream at will; it does not retain the boundaries between writes.For example, if an application does 5 writes to the TCP port, the application at the far end might do 10 reads to get all the data. Or it might get all the data with a single read. There is no correlation between the number and size of writes at one end to the number and size of reads at the other end.
TCP is a sliding window protocol with time-out and retransmits. Outgoing data must be acknowledged by the far-end TCP.
As with all sliding window protocols, the protocol has a window size. The window size determines the amount of data that can be transmitted before an acknowledgement is required. For TCP, this amount is not a number of TCP segments but a number of bytes.










TCP: Transmission Control Protocol
![img](https://lh5.googleusercontent.com/bn0AfW3x1b8OFqv9JJueE_cNAaJH0a0K5SeiSYRWBf8Bx06P6jPL7FtEkv3dysaYuEY97bsa_mV7oYw1av4ygxtUeak16IeuvOPsePFDBgeifeZBXJde6GoDHVMSzKuNoVfo-xzT)
lower level protocol(internet protocol): which provides a way for the TCP to send and receive variable-length segments of information enclosed in internet datagram "envelopes"

RFC 791 Internet ProtocolThe internet protocol implements two basic functions: addressing and fragmentation.


RFC 7230 Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing