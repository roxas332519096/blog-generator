---
title: WEB性能优化
date: 2018-07-25 02:51:44
categories:
- 业务代码
tags:
- 业务代码
---
#### Web性能优化之分析

优化:用户觉得网站加载速度快.

占用CPU少不算,它属于服务器性能优化.

先来了解用户浏览器输入url,按回车后,前端部分

1. 缓存
2. DNS查询
3. 建立TCP链接
4. 发送HTTP请求
(后台处理),等待中
5. 接收响应
6. 接收完成,得到HTML
7. 浏览器解析HTML,先查看DOCTYPE
8. 逐行解析
9. 如果看到标签,部分浏览器直接渲染,部分浏览器不渲染(因为W3C没有规定以何种形式渲染)
   例如chrome,假如直接渲染那么css下载完毕后,要再次渲染,IE与Firefox则是直接渲染,css下载结束后再渲染一次.
10. 看到CSS,下载CSS,继续往下看还有没有CSS,假如有则同时下载另外的CSS,最多可以同时下载单个域名同时8个(chrome)/4个(ie8).逐个解析.(并行下载,解析串行).
11. 看到JS,并行下载,解析串行,一定阻塞HTML渲染.


#### WEb性能优化之对策

对以上步骤进行分治.
1. DNS查询:
   1. 减少域名,以减少DNS查询时间,把资源放到同一个域名内.

2. 建立TCP链接:
    1. 开启keep-alive,使得TCP链接复用.
    2. 开启HTTP2.0,进行多路复用,效率更高.

3.  发送HTTP请求
    1. 减少Cookie体积,从而减少请求体积.不要滥用Cookie.
    2. 使用CahcheControl(缓存),一定时间内不发请求.
    3. 增加请求域名,可以同时发送更多个请求.(浏览器单域名8/4个).
        与DNS查询优化冲突:权衡利弊,假如文件少则减少域名,从而减少DNS查询时间,假如文件多则增加域名,让其同时下载文件数变多,加快下载时间.
    4. 把多个JS/CSS文件合并成一个,减少请求数.
    
4.  接收响应 
    1. 利用ETAG,返回304响应,不进行下载,直接用上次的文件.
    2. 用Gzip压缩,缺点:耗费CPU.权衡:文件越大收益越高,反之越低,比如文件只有1K.

5. DOCTYPE
    1. 一定要写对,不能写错,或者不写.写错了浏览器会猜.

6. 标签
    1. 尽量减少标签使用

7. CSS/JS文件下载
    1. 尽量把JS放CDN,增加并发下载数,同时让资源分布到全球各地,资源 下载速度更快.
    2. 把CSS放在head里:因为CSS一定会柱塞渲染,就算放最后也会柱塞,所以尽早下载.保证用户看到完整的画面.
        JS放在body最后,尽早显示页面,而且让JS可以获取到之前渲染好的节点.

8. 延迟组件加载
    节约流量

9. 预加载
    还没看的时候就加载了.

10. 加个Loading动画


#### 测试优化

Chrome浏览器,点击Audtis,点击perform,点击run.