---
title: url
date: 2020-11-19 22:34
tags:
- http
- 计算机网络
---
定义：URL 相当于一个文件名在网络范围的扩展。因此 URL 是与互联网相连的机器上的任何可访问对象的一个指针  

**常用的一般格式:**
<协议>://<主机>:<端口>/<路径>
**如果省略了路径，即只访问目标主机，则显示的是目标服务器上的主页html**
大多数的URL语法都建立在以下9个部分构成的通用格式上：
```
<scheme>://<user>:<password>@<host>:<port>/</path>;<params>?<query>#<frag>
其中最重要的3个部分是：
1. scheme：协议
2. host：主机
3. path：路径

如下例子：
http://www.baidu.com:80/index.html
方案是http，主机是www.baidu.com（域名），端口号是80，路径是/index.html  
``` 