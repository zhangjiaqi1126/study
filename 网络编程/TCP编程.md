# Socket

Socket是网络编程的一个抽象概念。通常我们用一个Socket表示“打开了一个网络链接”，而打开一个Socket需要知道目标计算机的IP地址和端口号，再指定协议类型即可。

Socket又称"套接字"，应用程序通常通过"套接字"向网络发出请求或者应答网络请求，使主机间或者一 台计算机上的进程间可以通讯。

## 语法

创建套接字

```python
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
#`socket.AF_INET` 表示使用 IPv4 地址族，如果要用更先进的IPv6，就指定为AF_INET6
#`socket.SOCK_STREAM` 表示使用面向连接的流套接字。
```

绑定地址和端口

```python
s.bind(('localhost', 8080))  #`bind()` 方法将套接字绑定到指定的地址和端口上。这里我们将套接字绑定到本地主机的 8080 端口。
```

监听连接

```python
s.listen(5)   #`listen()` 方法使套接字开始监听连接请求。参数 5 表示最多同时接受 5 个连接请求。
```

接受连接

```python
conn, addr = s.accept()#接受客户端的连接请求，并返回一个新的套接字对象，用于与客户端通信。
```

发送和接收数据

```python
conn.sendall(b'Hello, client!') #`sendall()` 方法将数据发送给客户端，
data = conn.recv(1024)#`recv()` 方法从客户端接收数据。这里我们发送了一个简单的字符串，并接收了最多 1024 字节的数据。
```

关闭套接字

```python
conn.close()
s.close()    
#关闭套接字以释放资源。
```

## 实例

**服务器端**

```python
import socket

# 创建一个新的 TCP/IP 套接字
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 将套接字绑定到本地主机的 8080 端口
s.bind(('localhost', 8080))

# 开始监听连接请求，最多同时接受 5 个连接请求
s.listen(5)

# 阻塞并等待直到有客户端连接，然后返回一个新的套接字对象和客户端的地址
conn, addr = s.accept()

# 打印已连接的客户端地址
print('Connected by', addr)

while True:
    # 从客户端接收数据，最多接收 1024 字节
    data = conn.recv(1024)
    
    # 如果没有收到数据，跳出循环
    if not data:
        break
    
    # 将接收到的数据回复给客户端
    conn.sendall(b'Echo: ' + data)

# 关闭与客户端的连接
conn.close()

# 关闭服务器套接字
s.close()
```

**客户端**

```python
import socket

# 创建一个新的 TCP/IP 套接字
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 连接到服务器的 8080 端口
s.connect(('localhost', 8080))

# 发送一条消息给服务器
s.sendall(b'Hello, server!')

# 从服务器接收回复的数据，最多接收 1024 字节
data = s.recv(1024)

# 打印服务器的回复
print(data.decode())

# 关闭与服务器的连接
s.close()
```

## 方法说明

服务端套接字方法

| s.bind()   | 绑定地址(host,port)到套接字， 在AF_INET下, 以元组(host,port)的形式表示地址。 |
| ---------- | ------------------------------------------------------------ |
| s.listen() | 开始TCP监听。backlog指定在拒绝连接之前，操 作系统可以挂起的最大连接数量。该值至少为1， 大部分应用程序设为5就可以了。 |
| s.accept() | 被动接受TCP客户端连接,(阻塞式)等待连接的到 来                |

客户端套接字

| s.connect()    | 主动初始化TCP服务器连接，。一般address的格 式为元组(hostname,port)，如果连接出错，返 回socket.error错误。 |
| -------------- | ------------------------------------------------------------ |
| s.connect_ex() | connect()函数的扩展版本,出错时返回出错码,而不 是抛出异常     |

公用方法

| s.recv()                             | 接收TCP数据，数据以字符串形式返回，bufsize 指定要接收的最大数据量。flag提供有关消息的其 他信息，通常可以忽略。 |
| ------------------------------------ | ------------------------------------------------------------ |
| s.send()                             | 发送TCP数据，将string中的数据发送到连接的套 接字。返回值是要发送的字节数量，该数量可能 小于string的字节大小。 |
| s.sendall()                          | 完整发送TCP数据，完整发送TCP数据。将string 中的数据发送到连接的套接字，但在返回之前会 尝试发送所有数据。成功返回None，失败则抛出 异常。 |
| s.recvfrom()                         | 接收UDP数据，与recv()类似，但返回值是 （data,address）。其中data是包含接收数据的字 符串，address是发送数据的套接字地址。 |
| s.sendto()                           | 发送UDP数据，将数据发送到套接字，address是 形式为（ipaddr，port）的元组，指定远程地址。 返回值是发送的字节数。 |
| s.close()                            | 关闭套接字                                                   |
| s.getpeername()                      | 返回连接套接字的远程地址。返回值通常是元组 （ipaddr,port）。 |
| s.getsockname()                      | 返回套接字自己的地址。通常是一个元组 (ipaddr,port)           |
| s.setsockopt(level,optname,value)    | 设置给定套接字选项的值。                                     |
| s.getsockopt(level,optname[.buflen]) | 返回套接字选项的值。                                         |
| s.settimeout(timeout)                | 设置套接字操作的超时期，timeout是一个浮点 数，单位是秒。值为None表示没有超时期。一 般，超时期应该在刚创建套接字时设置，因为它 们可能用于连接的操作（如connect()） |
| s.gettimeout()                       | 返回当前超时期的值，单位是秒，如果没有设置 超时期，则返回None。 |
| s.fileno()                           | 返回套接字的文件描述符。                                     |
| s.setblocking(flag)                  | 如果flag为0，则将套接字设为非阻塞模式，否则 将套接字设为阻塞模式（默认值）。非阻塞模式 下，如果调用recv()没有发现任何数据，或send() 调用无法立即发送数据，那么将引起socket.error 异常。 |
| s.makefile()                         | 创建一个与该套接字相关连的文件                               |

