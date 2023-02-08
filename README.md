# hao_socket
hao_socket
## 01 Socket API
socket()根据指定的地址族、数据类型和协议来分配一个套接口的描述字及其所用资源的函数
```
int socket(int domain, int type, int protocol);
//domain: 协议族/簇 AF_INET(IPv4), AF_INET6(IPv6)
//type: 套接口类型： SOCK_STREAM(TCP), SOCK_DGRAM(UDP)
//protocol: 一般为0
//返回创建成功的socketfd， 如果创建失败返回-1
```
bind()绑定socket到本地地址和端口，通常由服务器调用
```
int bind(int sockfd, const struct sockaddr* addr, socklen_t addrlen);
//socketfd,需要绑定地址的socket fd
//addr, 通常socket地址的指针，需要专用类型强制类型转换
//addrlen, addr的大小， 通常用sizeof取好

//0绑定成功， -1发生错误
```
listen() TCP专用，开启监听模式。服务端socket完成地址绑定后，需要创建监听队列并开始socket监听绑定的端口，将待处理的客户端连接存放在监听队列中。
```
int listen(int sockfd, int backlog);
sockfd: 被监听的socket，因此服务端通过socket函数创建的socket fd一般也叫作listen fd
blacklog： 客户端发起的连接等待accept，在socket fd监听等待队列最大长度。