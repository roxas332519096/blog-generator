---
title: 简单server建设
date: 2018-05-07 16:58:44
tags:
---
#### 1.TCP协议

全称：传输控制协议（Transmission Control Protocol）

TCP与UDP：TCP可靠（可知是否成功），面向链接（建立链接），比UDP较慢。UDP不可靠，不面向链接，比TCP快。

##### TCP的三次握手：
1. 客户端：我要连接你了,可以吗
2. 服务端：嗯，我准备好了,连接我吧
3. 客户端：那我连接你咯.
4. 开始后面步骤

#### 2.IP协议

##### 全称：网络协议（Internet Protocol）

1. 内网不能直接访问外网，需要经过路由器（网关）

2. 外网设备可以互相访问

3. 外网不能访问内网，需要经过路由器（网关）

##### 路由器：
既有外网ip 也有内网ip 分配内网ip

127.0.0.1/localhost  设备自己 host文件默认下127.0.0.1 localhost 表示localhost指向127.0.0.1

0.0.0.0 不表示任何设备

#### 3.端口(Port)

不仅要指定ip，还必须指定端口

服务器一个端口提供一个服务

##### 例如：
HTTP 80
HTTPS 443
FTP 21

一共2^16-1=65535个端口

0-1023（2^10-1）端口留给系统用，只有管理员权限才能使用

如果端口正在提供服务（占用），只能先停掉该端口服务，才能再使用

访问http://www.qq.com 没有写端口，是因为浏览器自动补全

实际是http://www.qq.com:80

#### 4.简单node.js server

[代码请点击](https://github.com/roxas332519096/nodejs_server/blob/master/server.js)

##### 使用：

1. git bash输入node server 端口（不能是0-1023）。
2. 别动，然后打开新的git bash窗口。
3. 输入curl http://localhost:端口/xxx或者curl http://127.0.0.1:端口/xxx
4. 使用curl -s -v -- "http://localhost:端口/xxx"可以查看完整的请求和响应
5. 也就可以在浏览器输入http://localhost:端口/xxx或http://127.0.0.1:端口/xxx
6. 按ctrl+c退出server

##### 注意事项：

1. 响应的后缀没有意义，文件内容是由HTTP头部的Content-Type保证的。

2. HTTP路径不是文件路径；/xxx.html不一定对应xxx.html文件