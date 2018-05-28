---
title: http基础知识
date: 2018-05-07 16:15:23
tags:
---

#### 1.何为HTTP?

HTTP全称为HyperText Transfer Protocol（超文本传输协议.是服务器（服务端）与浏览器（客户端）之间的协议。
作用是指导浏览器和服务器如何沟通。

#### 2.何为URI?

##### URI

统一资源标识符（Uniform Resource Identifier).
URI包括URN与URL两种.

##### URN

统一资源名称 (Uniform Resource Name).
例如一本书,SBN: 9787115275790 就是一个 URN，通过 URN 你可以确定一个「唯一的」资源.
URN也是独一无二的.

##### URL

统一资源定位符 (Uniform Resource Locator).
也就是我们常说的网址,通过 URL 你可以确定一个「唯一的」地址（网址）。

例如:https://www.baidu.com/s?wd=hello&rsv_spt=1#5 就是一个 URL
``` bash
https://           协议
www.baidu.com      域名
/s                 路径
wd=hello&rsv_spt=1 查询参数
井号5              锚点
```
#### 3.何为DNS?

DNS（Domain Name System，域名系统），，万维网上作为域名和IP地址相互映射的一个分布式数据库，能够使用户更方便的访问互联网，而不用去记住能够被机器直接读取的IP数串。过域名，最终得到该域名对应的IP地址的过程叫做域名解析（或主机名解析）。DNS协议运行在UDP协议之上，使用端口号53。

其作用是输入域名,输出IP.

#### 4.git curl 命令

curl 是一个利用URL规则在命令行下工作的文件传输工具。

语法:

``` bash
$ crulp [option] -- [url]
```

例:

``` bash
curl --"https://www.baidu.com"
```

#### 5.HTTP 请求
##### 格式:
1 动词 路径 协议/版本
2 Key1: value1
2 Key2: value2
2 Key3: value3
3（回车）
4 要上传的数据

例:
```` bash
POST / HTTP/1.1         //动词：POST 路径 / 协议/版本：HTTP/1.1
Host: www.baidu.com     //Key1:value1
User-Agent: curl/7.54.0 //key2:value2
Accept: */*            //Key3:value3             
Frank: xxx             //key4:value4
Content-Length: 10     //key5:value5
Content-Type: application/x-www-form-urlencoded //key6:value6
（回车）
1234567890             //要上传的数据
````

##### 使用Chrome开发者工具查看HTTP请求内容

1.打开 Network
2.地址栏输入网址
3.在 Network 点击，查看 request，点击「view source」
4.点击「view source」
5.如果有请求的第四部分，那么在 FormData 或 Payload 里面可以看到

#### 5.HTTP 响应
##### 格式:
1 协议/版本号 状态码 状态解释
2 Key1: value1
2 Key2: value
3 （回车）
4 要下载的内容

例:
```` bash
HTTP/1.1 302 Found  //协议/版本号：HTTP/1.1 状态码：302 状态解释：OK
Connection: Keep-Alive //Key1: value1
Content-Length: 17931 //Key2: value2
Content-Type: text/html //Key3: value3
Date: Tue, 10 Oct 2017 09:19:47 GMT //Key4: value4
Etag: "54d9749e-460b" //Key5: value5
Server: bfe/1.0.8.18 //Key6: value6
（回车）
<html>.....(省略)...</html>
````

##### 使用Chrome开发者工具查看HTTP响应内容

1.打开 Network
2.输入网址
3.选中第一个响应
4.查看 Response Headers，点击「view source」
5.查看 Response 或者 Preview，你会看到响应的第 4 部分

#### 6.状态码

1XX 信息
2XX 成功
3XX 重定向
4XX 客户端错误
5XX 服务器错误

#### 7.一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？

1. 浏览器地址栏输入url

2. 浏览器会先查看浏览器缓存--系统缓存--路由缓存，如有存在缓存，就直接显示。如果没有，接着第三步

3. 域名解析（DNS）获取相应的ip

4. 浏览器向服务器发起tcp连接，与浏览器建立tcp三次握手

5. 握手成功，浏览器向服务器发送http请求，请求数据包

6. 服务器请求数据，将数据返回到浏览器

7. 浏览器接收响应，读取页面内容，解析html源码，生成DOm树

8. 解析css样式、浏览器渲染，js交互