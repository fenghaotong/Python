
# Python第十一章学习

## 网络编程
- [x] TCP/IP简介
- [x] TCP编程
- [x] UDP编程

## 网络编程
- 自从互联网诞生以来，现在基本上所有的程序都是网络程序，很少有单机版的程序。

- 计算机网络就是把哥哥计算机连接在一起，让网络中的计算机可以互相通信，网络编程就是如何在程序中实现两台计算机的通信。

- 网络编程对所有开发语言都是一样的，Python也不例外。用Python进行网络编程，就是在Python程序本身这个进程内，连接别的服务器进程的通信端口进行通信。

### TCP/IP简介
- 互联网协议中最重要的两个协议就是TCP协议和IP协议，所以把互联网的协议称为TCP/IP协议

- TCP协议是建立在IP协议之上的，TCP协议负责在两台计算机之间建立可靠的链接，保证数据报按顺序到达，它会通过握手建立连接，然后对每个IP包编号，确保对方按顺序收到，如果丢掉，自动重发

- 许多常用的更高级的协议都是建立在TCP协议基础上的，比如用于浏览器的HTTP协议、发送邮件的SMTP协议等。

- 一个IP包除了包含要传输的数据外，还包含源IP地址和目标IP地址，源端口和目标端口。

### TCP编程
- 如果学过计算机网络，应该对Socket编程不陌生，通常我们用一个Socket表示“打开了一个网络链接”，而打开一个Socket需要知道计算机的IP地址和端口号，在指定协议类型即可。

#### 客户端

- 大多数链接都是可靠的TCP连接，主动发起链接的叫客户端，被动响应连接的叫服务器

- 举个例子，我们在浏览器中访问新浪时，我们自己的计算机就是客户端，浏览器会主动向新浪的服务器发起连接，如果一切顺利，新浪的服务器接受了我们的链接，一个TCP连接就建立起来了，后面的通信就是发送网页内容了


```python
# 首先我们要创建一个基于TCP连接的Socket，可以这样做
import socket

#创建一个socket
s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)

#建立连接
s.connect(("www.sina.com.cn",80))
```

创建socket时，AF_INET指定使用IPv4协议，如果要用更先进的IPv6，就要指定AF_INET6。SOCK_STREAM指定使用面向流的TCP协议，这样一个socket对象就创建成功了，但是还没有建立连接

客户端要主动建立连接，必须知道服务器的IP地址和端口号，新浪网站的IP地址可以用域名`www.sina.com.cn`自动转换成IP地址,端口号是80，因为HTTP服务器的端口号是80

所以最后一行代码建立了TCP连接，注意括号里面是一个tuple，包含了IP地址和端口号


```python
#建立连接之后，向服务器发送请求，要求返回首页内容
s.send(b"GET / HTTP/1.1\r\nHost:www.sina.com.cn\r\nConnection:close\r\n\r\n")
```




    58



TCP连接创建的是双向通道，双方都可以同时给对方发数据。但是谁先发谁后发，怎么协调，要根据具体的协议来决定。例如，HTTP协议规定客户端必须先发请求给服务器，服务器收到后才发数据给客户端。


```python
#发送的文本必须符合HTTP标准，之后开始接受数据
buffer = []
while True:
    #每次最多接受1k字节
    d = s.recv(1024)
    if d:
        buffer.append(d)
    else:
        break

data = b"".join(buffer)
```

接收数据的时候，调用recv(max)方法，一次最多接收指定的字节数，因此在一个while循环中反复接收，知道recv()返回数据，表示接收完毕，退出循环。

当接收完数据时，关闭连接，这样一次完整的通信就结束了


```python
s.close()
```

接收到的数据包括HTTP头和网页本身，我们只需要把HTTP头和网页分离一下，把HTTP头打印出来，网页内容保存到文件：


```python
heaer,html = data.split(b"\r\n\r\n",1)
print(header.decode("utf-8"))

#然后把收到的数据写入文件

with open("sina.html","wb") as f:
    f.write(html)
```

    HTTP/1.1 200 OK
    Server: nginx
    Date: Fri, 24 Jun 2016 06:34:54 GMT
    Content-Type: text/html
    Last-Modified: Fri, 24 Jun 2016 06:34:28 GMT
    Vary: Accept-Encoding
    Expires: Fri, 24 Jun 2016 06:35:54 GMT
    Cache-Control: max-age=60
    X-Powered-By: shci_v1.03
    Age: 49
    Content-Length: 582513
    X-Cache: HIT from cernet194-225.sina.com.cn
    Connection: close
    

现在只需要打开浏览器中这个sina.html文件，就可以看到新浪的首页了

#### 服务器
- 和客户端相比，服务器的编程就要复杂一些

- 服务器进程首先要绑定一个端口并监听来自其他客户端的连接。如果某个客户端连接过来了，服务器就与该客户端建立Socket连接，随后的通信就靠这个Socket连接了。

- 所以，服务器会打开固定端口（比如80）监听，每来一个客户端连接，就创建该Socket连接。由于服务器会有大量来自客户端的连接，所以，服务器要能够区分一个Socket连接是和哪个客户端绑定的。一个Socket依赖4项：服务器地址、服务器端口、客户端地址、客户端端口来唯一确定一个Socket。

- 但是服务器还需要同时响应多个客户端的请求，所以，每个连接都需要一个新的进程或者新的线程来处理，否则，服务器一次就只能服务一个客户端了。

下面我么举个例子，编写一个简单的服务器程序，它接收客户端的连接，把客户端发过来的字符加上hello在发送回去。

首先，创建一个基于IPv4和TCP协议的Socket：


```python
s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
```

然后我们要绑定监听的地址和端口，在这里我们绑定127.0.0.1，这个ip地址比较特殊，表示本机地址，绑定这个地址表示客户端必须同时在本机上运行才能连接，外部的计算机无法连接进来


端口号绑定为9990，小于1024的端口号必须要有管理员的权限才能绑定


```python
#监听端口
s.bind(("127.0.0.1",9990))
```

然后，调用listen（）方法开始监听端口，传入的参数指定等待连接的最大数量：


```python
s.listen(5)
print("waiting for connection...")
```

    waiting for connection...
    

接下来，服务器程序通过一个永久循环来接受来自客户端的连接，accept()会等待并返回一个客户端的连接:

```python
while True:
    # 接受一个新连接:
    sock, addr = s.accept()
    # 创建新线程来处理TCP连接:
    t = threading.Thread(target=tcplink, args=(sock, addr))
    t.start()
```

每个连接都必须创建新线程（或进程）来处理，否则，单线程在处理连接的过程中，无法接受其他客户端的连接：


```python
def tcplink(sock,addr):
    print("Accept new connection from %s:%s..." % addr)
    sock.send(b"welcome!")
    while True:
        data = sock.resv(1024)
        time.sleep(1)
        if not data or data.decode("utf-8") == "exit":
            break
        sock.send(("hello,%s" % data.decode("utf-8")).decode("utf-8"))
    sock.close()
    print("Connection from %s:%s closed" % addr)
```

连接建立后，服务器首先发一条欢迎消息，然后等待客户端数据，并加上Hello再发送给客户端。如果客户端发送了exit字符串，就直接关闭连接。

下面是服务器的完整程序：（server.py）
```python
import socket, threading, time

#TCP socket based on ipv4
#server
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

#listening on port
s.bind(('127.0.0.1', 9999))
s.listen(5)
print("Waiting for connection...")

def tcplink(sock, addr):
    print('Accept new connection from %s:%s...' % addr)
    sock.send(b'Welcome!')
    while True:
        data = sock.recv(1024)
        time.sleep(1)
        if not data or data.decode('utf-8') == 'exit':
            break
        sock.send(('Hello, %s!' %data.decode('utf-8')).encode('utf-8'))
    sock.close()
    print('Connection from %s:%s closed.' % addr)

while True:
    #receive a new connect 
    sock, addr = s.accept()
    #make a new thread dispose TCPlink
    t = threading.Thread(target=tcplink, args=(sock, addr))
    t.start()
```

要测试这个服务器程序，我们还需要编写一个客户端程序：(client.py)
```python
# -*- coding:utf-8 -*-

import socket

#client
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

#establish connection
s.connect(('127.0.0.1', 9999))

#receive a welcome message
print(s.recv(1024).decode('utf-8'))

for data in [b'Lambda', b'Bond', b'alpha']:
    #send data
    s.send(data)
    print(s.recv(1024).decode('utf-8'))
s.send(b'exit')
s.close()
```

上面两个程序可以放在命令行进行测试，需要打开两个命令行窗口，一个运行服务器程序，一个运行客户端程序

### UDP编程
- TCP是建立可靠连接，并且通信双方都可以以流的形式发送数据，相对tcp，udp则是面向无连接的协议，只要知道对方的ip地址和端口号，就可以直接发送数据，但是不知道能不能到达。

- 它的优点就是比tcp速度快，对于不要求可靠到达的数据，就可以使用UDP协议

- 和TCP一样UDP的通信双方也分客户端和服务器


```python
#服务器端首先要绑定接口
import socket
s = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)
s.bind(("127.0.0.1",9900))
```

SOCK_DGRAM指定了socket的类型是UDP，他不用listen()方法监听，而是直接接受来自任何客户端的数据：


```python
print("bind UDP on 9900...")
while True:
    #接收数据
    data,addr = s.recvfrom(1024)
    print("Received from %s:%s." % addr)
    s.sendto(b"hello,%s!" % data,addr)
```

recvfrom()方法返回数据和客户端的地址与端口，这样，服务器收到数据后，直接调用sendto()就可以把数据用UDP发给客户端。

客户端使用UDP时，首先仍然创建基于UDP的Socket，然后，不需要调用connect()，直接通过sendto()给服务器发数据.

下面是完整的例子：

udp服务器端：（udpserver.py）
```python
#socket udp server
import socket

sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
sock.bind(('127.0.0.1', 9999))
print ('Bind UDP on 9999...')

while True:
    data, addr = sock.recvfrom(1024)
    print ('Received from %s:%s' % addr)
    sock.sendto(b'Hello, %s!' %data, addr)
```

udp客户端：（udpclien.py）
```python
# socket udp client

import socket

sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
for data in [b'Michael', b'Tracy', b'Sarah']:
    sock.sendto(data, ('127.0.0.1', 9999))
    print (sock.recv(1024).decode('utf-8'))

sock.close()
```

上面两个程序可以放在命令行进行测试，需要打开两个命令行窗口，一个运行服务器程序，一个运行客户端程序
