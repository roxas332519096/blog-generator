---
title: Websocket
date: 2019-04-18 10:29:19
categories:
tags:
---

#### 什么是 websocket

websocket 是 HTML5 新增的一种通信协议,服务端可主动给客户端推送消息,客户端也可向服务端主动发送消息.

使用 websocket api 浏览器与服务器只需要做一个握手动作,两者形成通道,实现持久化的双向通讯.

#### websocket 的优点

当还不存在 websocket 的时候,以前用 ajax 轮询与 http long poll 实现该功能.

##### ajax 轮询

浏览器定时给服务器发送 ajax 请求,当服务器有新消息时候,返回数据.

流程如下:

浏览器:我要获取新数据.
服务器:没有.
浏览器:我要获取新数据.
服务器:没有.
浏览器:我要获取新数据.
服务器:没有.
浏览器:我要获取新数据.
服务器:有了,给你.

##### http long poll

http long poll 是通过阻塞模型(拨打电话之后不挂断),浏览器与服务器建立链接后,假如没有新消息则不返回数据,知道有消息才返回,再重新建立链接.

浏览器:等有数据的时候给我吧.
...
...
...
服务:有数据了,给你.
浏览器:等有数据的时候给我吧.
...
...
...
服务:有数据了,给你.

以上两者方法是非常消耗资源的,第一种需要更快的服务器,第二种则需要服务器能处理更多的请求.

#### websocket 的作用

websocket 的出现解决了这个问题.首先,websocket 是双向通信协议,服务器可获得新消息主动给浏览器发送消息.

##### websocket 握手过程

浏览器通过调用 new websocket(url)方法与服务器建立链接.

1. 浏览器与服务器进行三次握手,假如失败则不继续,并报错.
2. 建立连接成功后,浏览器通过 http 协议传送 websocket 的版本号,协议的字版号,原始地址,主机地址等字段给服务器.
3. 服务器接收浏览器的请求,假如上述字段正确,则接受本次握手,并返回对应数据,包含 http 相关的信息.
4. 浏览器接收数据,假如成功则触发 open 事件,浏览器可通过 send 方法发送数据,假如失败则触发 error 事件.

#### websocket api

使用 websocket api 建立与服务器的连接.

```bash
const socket = new Websocket(url);
```

#### 事件

##### open

```bash
socket.onopen = (e)=>{
    socket.send('hello')
}
```

##### message

服务器有响应信息

```bash
socket.onmessage = (e)=>{
    console.log(e.data)
}
```

##### error

当触发错误时,会关闭连接,并返回错误信息.

```bash
socket.onerror = (e)=>{
    console.log('error')
}
```

##### close

当关闭时触发

```
socket.onclose = (event) => {
    debugger;
}
```

event 的参数

```bash
1. event.wasClean [boolean],假如为true,表示客户端或服务端调用close主动关闭.
2. event.code [number] 关闭的状态码
3. event.reason [string] 关闭的原因

//主动close的方法
socket.close(code,reason)
```

##### send

send(data),发送 data,可以是 string/blob/ArrayBuffer/ByteBuffer 等
send 必须在建立链接成功之后,一般在 open 事件后触发.

```bash
socket.onopen = ()=>{
    soclet.send('hello')
}
```

判断是否还连接着

```bash
if(socket.readyState == WebSocket.OPEN){
    socket.send(data)
}
```

#### 常量

CONNECTING 0 连接还未开启
OPEN 1 连接开启可以通信
CLOSING 2 连接正在关闭中
CLOSED 3 连接已经关闭

#### 属性

binaryType String
表示连接传输的二进制数据类型的字符串。默认为"blob"。

bufferedAmount Number
只读。如果使用 send()方法发送的数据过大，虽然 send()方法会马上执行，但数据并不是马上传输。浏览器会缓存应用流出的数据，你可以使用 bufferedAmount 属性检查已经进入队列但还未被传输的数据大小。在一定程度上可以避免网络饱和。

protocol String/Array
在构造函数中，protocol 参数让服务端知道客户端使用的 WebSocket 协议。而在实例 socket 中就是连接建立前为空，连接建立后为客户端和服务器端确定下来的协议名称。

readyState String
只读。连接当前状态，这些状态是与常量相对应的。

extensions String
服务器选择的扩展。目前，这只是一个空字符串或通过连接协商的扩展列表。

#### Socket.io

Socket.io 是一个跨浏览器支持 websocket 的实时通讯的 js.

http://socket.io/docs/

##### 安装与引入

```
npm install --save socket.io
```

```bash
<script src="/socket.io/socket.io.js"></script>
const socket = io(url);

或者

improt io from 'socket.io-client'

const socket = io(url);
```

##### API

官方文档:
https://socket.io/docs/client-api/
