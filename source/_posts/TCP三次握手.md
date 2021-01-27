---
title: TCP三次握手
date: 2021-01-27 22:42
tags: 
- 计算机网络
---

# TCP三次握手

工具： wireshark

1. 使用cmd，ping一下学校的在线教育网址：

   ![image-20210126165220094](C:\Users\10922\AppData\Roaming\Typora\typora-user-images\image-20210126165220094.png)

2. 获得网址的ip地址，然后在wireshark中过滤：

   ![image-20210126165256338](C:\Users\10922\AppData\Roaming\Typora\typora-user-images\image-20210126165256338.png)

3. 在浏览器中输入学校的在线教育地址eol.scau.edu.cn

   然后在wireshark出现如下连接：

   1. **第一次握手**。从本地12212端口发送带有SYN的报文，发送到目的服务器的80端口（因为使用的是http连接），序列号seq为3942013096。标志为SYN。

   2. 

      ![image-20210126165944924](C:\Users\10922\AppData\Roaming\Typora\typora-user-images\image-20210126165944924.png)

      ![image-20210127175617540](C:\Users\10922\AppData\Roaming\Typora\typora-user-images\image-20210127175617540.png)

   3. **第二次握手**，紧接着，服务器收到客户端的tcp连接请求之后，发送请求到客户端。从服务器的80端口发送到客户端的12212端口。其中确认号是上一次客户端发送过来的序列号加一即3942013097，序列号seq为2536558822。其中确认号标志位SYN、ACK：

      ![image-20210126173153882](C:\Users\10922\AppData\Roaming\Typora\typora-user-images\image-20210126173153882.png)

      ![image-20210127175552582](C:\Users\10922\AppData\Roaming\Typora\typora-user-images\image-20210127175552582.png)

   4. **第三次握手**。客户端收到服务器发送过来的报文之后，从本地12212端口发送数据到服务器80端口，序列号为3942013097，确认号为2536558822+1=2536558823。标志为ACK：

      ![image-20210126173417730](C:\Users\10922\AppData\Roaming\Typora\typora-user-images\image-20210126173417730.png)

      ![img](file:///C:/Users/10922/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

   5. 之后HTTP连接就成功建立起来：

      ![image-20210126173519629](C:\Users\10922\AppData\Roaming\Typora\typora-user-images\image-20210126173519629.png)

   