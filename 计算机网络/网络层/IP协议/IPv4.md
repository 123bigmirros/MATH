### IPv4

**协议格式**    
![](../../picture/IP格式.png)
- 补充
  - 首部长度以4字节为单位，总长度以1字节为单位，片偏移以8字节为单位
  - 标识是一个计数器，不起序号作用，而是标识分片之后的数据是来自同一个数据报的
  - 标志有三位，最低位MF，表示数据后面是否还有分片，为1表示有，为0表示最后一个分片。中间一位是DF，只有为0时才允许分片。
  - 首部校验和只校验分组的首部

**IPv4地址**  
- IPv4分类  
互联网早期采用的IP地址方式。IP地址分成A(8,0)、B(16,10)、C(24,110)、D(,1110)、E(,1111)类。IP地址由网络号和主机号组成。
    - 补充
      - D类地址用于多播地址
      - 主机号全0和全1不分配，全0表示网络本身，全1表示广播地址

- 子网划分和子网掩码  
  - 子网划分基本概念  
  在Ip地址中增加一个“子网号字段”，使两级IP地址变为三级IP地址
  - 子网掩码基本概念  
  用来表明对子网的划分，使用子网掩码来表示对原网络主机号的借位
  - 补充  
    - 子网划分是单位内部的事，对外并不表现
    - 属于一个子网的所有主机及路由器端口，必须设置相同的子网掩码

- 无分类编址CIDR
  - 概念  
  在变长子网掩码的基础上，消除A、B、C类网络划分，并在软件的支持下实现超我那个构造。
  - 补充  
    - IP地址被封为{网络前缀，主机号}
    - CIDR不再IP地址中指明子网段，但组织可根据需要划分子网。
    - 网络前缀系统的IP地址构成"CIDR地址块"，一个CIDR地址块可以表示很多地址，这种地址称为路由聚合，也称构成超网
    - 最长前缀匹配

**网络地址转换NAT**  
- 概念  
通过将专用网络地址转换为公用网络地址，从而对外隐藏内部管理IP地址。  
- 专用网本地IP  
NAT使专用网只需要一个全球IP就可以与因特网连通，专用网本地IP地址可重用。
  - A类 10.0.0.0 ~ 10.255.255.255
  - B类 172.16.0.0 ~ 172.31.255.255
  - C类 192.168.0.0 ~ 192.168.255.255  

- 工作原理  
NAT利用NAT转发表实现本地IP地址到全球IP地址的转换。NAT表存放在{本地IP地址：端口}到{全球IP地址：端口}的映射。

**网络层分组转发过程**  
- 过程
  1. 收到IP分组，提取分组首部中目的主机的IP地址
  2. 若有特定的主机路由，则按照该路由的下一跳转发分组，否则检查转发表
  3. 将转发表中一行的子网掩码和目的地址相与，若结果匹配，则转发，否则若有下一行，则继续匹配，若所有的转发表项都匹配不成功，步骤4
  4. 若转发表中有默认路由，则把分组传送给默认路由，否则，报告转发分组出错。
- 补充  
  - 分组转发是基于目的主机所在的网络
  - 为特定目的主机的IP地址指明一个路由，称为主机路由
  - 使用特殊前缀 0.0.0.0/0表示默认路由