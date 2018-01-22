## 1.1 网络与ip的认知

在计算机领域中，**网络是信息传输、接收、共享的虚拟平台，通过它把各个点、面、体的信息联系到一起，从而实现这些资源的共享**。网络是人类发展史来最重要的发明，提高了科技和人类社会的发展。网络会借助文字阅读、图片查看、影音播放、下载传输、游戏、聊天等软件工具从文字、图片、声音、视频等方面给人们带来极其丰富的生活和美好的享受。通俗点讲，网络就像打电话时的电话线一样，连接着电话线两端的人；即**一种辅助双方或者多方能够连接在一起交流的工具**。为了让在不同的电脑上运行的软件之间能够互相传递数据，就需要借助于网络。

![](/assets/ip_img2.png)

![](/assets/ip_img1.png)

所谓网络编程就是，**让在不同的电脑上的软件之间能够进行数据传递，即进程之间的通信**。

和打电话一样，需要有运营商座机终端或者手机终端通过特定的电信号连接，网络之间想要进行握手通信就需要一种每台电脑都遵守的协议，这就是**IP——网络之间互联的协议**。它是能使连接到网上的所有计算机网络实现相互通信的一套规则，规定了计算机在因特网上进行通信时应当遵守的规则。同样，邮寄快递时我们常常需要一个唯一的收发地址，网络通信也需要网络内的每台设备有一个地址，这就是ip地址。**IP地址用来标记网络中的每一台设备**。

![](/assets/ip_img3.png)

如下图所示，路由器对应于广域网中的一个设备，需要一个广域网的ip，电脑主机属于路由器建立的局域网内设备，需要一个局域网ip，同一个网络内的设备ip是不同的。

![](/assets/ip_img4.png)

## 1.2 ip的分类

**ip地址由网络号和主机号组成。  
网络号：用于识别主机所在的网络；  
主机号：用于识别该网络中的主机。**

IP地址分为五类，A类保留给政府机构，B类分配给中等规模的公司，C类分配给任何需要的人，D类用于组播，E类用于实验，各类可容纳的地址数目不同。A、B、C三类IP地址的特征：当将IP地址写成二进制形式时，A类地址的第一位总是0，B类地址的前两位总是10，C类地址的前三位总是110。具体如下：

![](/assets/ip_img5.png)

**A类地址**

（1）A类地址第1字节为网络地址，其它3个字节为主机地址。它的第1个字节的第一位固定为0.  
（2）A类地址网络号范围：1.0.0.0---126.0.0.0  
（3）A类地址中的私有地址和保留地址：  
① 10.X.X.X是私有地址（所谓的私有地址就是在互联网上不使用，而被用在局域网络中的地址）。  
范围（10.0.0.0---10.255.255.255）  
② 127.X.X.X是保留地址，用做循环测试用的。

**B类地址**

（1） B类地址第1字节和第2字节为网络地址，其它2个字节为主机地址。它的第1个字节的前两位固定为10.  
（2） B类地址网络号范围：128.0.0.0---191.255.0.0。  
（3） B类地址的私有地址和保留地址  
① 172.16.0.0---172.31.255.255是私有地址  
② 169.254.X.X是保留地址。如果你的IP地址是自动获取IP地址，而你在网络上又没有找到可用的DHCP服务器。就会得到其中一个IP。  
**191.255.255.255是广播地址，不能分配。**

**C类地址**

（1）C类地址第1字节、第2字节和第3个字节为网络地址，第4个字节为主机地址。另外第1个字节的前三位固定为110。  
（2）C类地址网络号范围：192.0.0.0---223.255.255.0。  
（3） C类地址中的私有地址：  
192.168.X.X是私有地址。（192.168.0.0---192.168.255.255\)

**D类地址**

（1） D类地址不分网络地址和主机地址，它的第1个字节的前四位固定为1110。  
（2） D类地址范围：224.0.0.0---239.255.255.255

**E类地址**

（1） E类地址不分网络地址和主机地址，它的第1个字节的前五位固定为11110。  
（2） E类地址范围：240.0.0.0---255.255.255.254

**每台电脑的本地主机ip为127.0.0.1**

## 1.3 ip查询与ping测试

linux中查看ip的命令：**ifconfig**，windows中查看ip的命令：**ipconfig**

![](/assets/ip_img6.png)

**ping**用来测试远程主机网络连接是否通畅。

![](/assets/ip_img7.png)

## 1.4 端口port

![](/assets/ip_img11.png)

端口就像房间门一样，如果想进入房间则必须要通过门。如果一个程序想要收发网络数据，那就需要操作系统的一个端口。而一般操作系统的端口号很多（linux系统可以达到65536），为了统一管理，操作系统对所有的端口进行整数编号标记，即端口号。根据协议，端口号按照一定规则进行分配：

**知名端口（Well Known Ports）**

知名端口是众所周知的端口号，范围从0到1023。例如，80端口分配给HTTP服务；21端口分配给FTP服务。  
我们可以理解为，一些常用的功能使用的号码是固定的，就像重要的公众电话号码110、10086、10010一样。

**动态端口（Dynamic Ports）**

动态端口的范围是从1024到65535。之所以称为动态端口，是因为它一般不固定分配某种服务，而是动态分配。动态分配是指当一个系统程序或应用程序程序需要网络通信时，它向主机申请一个端口，主机从可用的端口号中分配一个供它使用。当这个程序关闭时，同时也就释放了所占用的端口号。

**查看端口**

用“netstat －an”查看端口状态。

## 1.5 小结

一台拥有IP地址的主机可以提供许多服务，比如HTTP（万维网服务）、FTP（文件传输）、SMTP（电子邮件）等，这些服务完全可以通过1个IP地址来实现。那么，主机是怎样区分不同的网络服务呢？显然不能只靠IP地址，因为IP地址与网络服务的关系是一对多的关系。**实际上是通过“IP地址+端口号”来区分不同的服务的。**总而言之，**IP地址标识网络中的一台主机，端口号标识这台主机上的一个服务\(应用程序\)**。![](/assets/ip_img10.png)
