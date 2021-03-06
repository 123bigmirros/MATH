### 移动IP

**概念**  
为移动中保持连接而设计。指移动结点以固定的IP地址实现不同网段的漫游功能，并保证基于网络IP的网络权限在漫游过程中不改变。  

**过程**  
1. 在本地网是，按传统的TCP/IP方式通信
2. 当结点漫游到外地网络，仍使用固定IP地址通信，移动结点向本地代理注册当前位置地址，位置地址是转交地址(外部代理地址或动态分配的地址)
3. 本地地址在接受来自转交地址的注册后，会构建一条通向转交地址的通道，将发给移动结点的IP分组通过通道发送给转交地址处
4. 在转交地址处解除封装，恢复原始的IP分组，最后送到移动结点
5. 移动结点通过外网路由器或外部代理向通信对端发送IP数据包
6. 移动结点到另一个外网时，向本地代理更新转交地址
7. 回到本地网是，移动结点向本地代理注销转交地址