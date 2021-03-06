---
title: Cookie-注册与登陆
date: 2018-06-10 16:07:22
categories:
- HTTP
tags:
- HTTP
---
### Cookie

#### Cookie是什么?

Cookie 是服务器保存在浏览器的一小段文本信息，每个 Cookie 的大小一般不能超过4KB。浏览器每次向服务器发出请求，就会自动附上这段信息。Cookie 主要用来分辨两个请求是否来自同一个浏览器，以及用来保存一些状态信息。它的常用场合有以下一些。

1. 对话（session）管理：保存登录、购物车等需要记录的信息。
2. 个性化：保存用户的偏好，比如网页的字体大小、背景色等等。
3. 追踪：记录和分析用户行为。

#### Cookie属性

名称 name (必须)
值 value 
域 domain
路径 path
失效时间 expires
安全标志 secure 一个带有安全属性的 cookie 只有在请求使用SSL和HTTPS协议的时候才会被发送到服务器
HttpOnly 设置该属性js不能从document.cookie;XMLHttpRequest;Request APIs访问Cookie

#### Cookie 特点

1. 服务器通过 Set-Cookie 响应头设置 Cookie
2. 浏览器得到 Cookie 之后，每次请求都要带上 Cookie
3. 服务器读取 Cookie 就知道登录用户的信息,例如:account,email,password等.
4. 不同的浏览器对Cookie数量和大小限制不一样,一般来说,单个域名的Cookdie不应超过30个,每个大小不超过4KB.

#### 问题

1. 我在 Chrome 登录了得到 Cookie，用 Safari 访问，Safari 会带上 Cookie 吗?
    不会,Cookie只有用之前获得Cookie的浏览器才会有.

2. Cookie 存在哪?
    Windows 存在 C 盘的一个文件里

3. Cookie会被用户篡改吗？
    可以,Session 来解决这个问题，防止用户篡改.

4. Cookie 有效期吗？
    默认有效期20分钟左右，不同浏览器策略不同
    后端可以强制设置有效期，具体语法看 MDN

5. Cookie 遵守同源策略吗？
    当请求 qq.com 下的资源时,浏览器会默认带上 qq.com 对应的 Cookie,不会带上 baidu.com 对应的 Cookie;
    当请求 v.qq.com 下的资源时,浏览器不仅会带上 v.qq.com 的Cookie,还会带上 qq.com 的 Cookie;
    二级域名,三级域名的Cookie都会带上.
    另外 Cookie 还可以根据路径做限制,这个功能用得比较少.;

6. .服务器端可以通过设置 Expires、max-age 两个标签将 Cookie 设置为过期状态;JavaScript 可以通过document.cookie API 删除 Cookie.


下面是一个带Cookie响应头
``` bash
HTTP /1.1 200 OK
Content-type:text/html
Set-Cookie:name=value; expires = Mon, 22-Jan-07 07:10:24 GMT; domain=.wrox.com path=/; secure; HttpOnly
```

#### 用户注册过程中浏览器与服务器发生了什么?

##### 前端(浏览器)

1. HTML里做一个Form表单,填入账号,Email,密码,确认密码等信息.
2. HTML表单里每行隐藏一个span标签,显示error属性.
3. 用JS获取用户填入的信息后,先进行前端认证,如填入的格式,密码是否相同等
4. 假如错误,将错误信息返回给error标签,显示信息.
5. 假如正确,用AJAX发送post请求(这是一个Promise对象),路径为服务器端注册页面,内容为用户提交的数据.
6. 服务器处理信息,返回给浏览器,假如正确执行XXX,假如错误则返回错误信息,前端把信息翻译后传到浏览器上.

##### 后端(服务器)

1. 如果请求为GET,读取数据库数据,返回状态码200,并返回html字符串给浏览器.
2. 如果请求为POST,先解析浏览器发送过来的request字符串,变为对象,分析传过来的数据,如格式,长度,密码是否相同等,账号是否存在,假如错误,则返回状态码400,并返回错误信息给浏览器.
3. 假如都正确,则写入数据库,返回状态码200.

#### 用户登录程中浏览器与服务器发生了什么?

##### 前端(浏览器)

1. HTML里做一个Form表单,填入账号,Email,密码,确认密码等信息.
2. HTML表单里每行隐藏一个span标签,显示error属性.
3. 用JS获取用户填入的信息后,先进行前端认证,如填入的格式,密码是否相同等
4. 假如错误,将错误信息返回给error标签,显示信息.
5. 假如正确,用AJAX发送GET请求,路径为服务器端登陆页面,内容为账号密码.
6. 服务器处理信息,返回给浏览器,并给浏览器一个Cookie假如验证成功则转跳页面,假如失败则错误提示.
7. 以后每次进入该页面,HTTP请求头都会包含之前服务器所返回的Cookie.
8. 页面渲染服务器传来这个Cookie的信息.

##### 后端(服务器)

1. 假如用第一次登陆,服务器在数据库查询该账号的信息是否匹配.
2. 假如不匹配,则返回401.
3. 假如匹配.则返回200状态码,并返回一个Cookie给浏览器.并返回该Cookie对应的信息,渲染页面.
4. 用户发送请求,请求中带该Cookie,则服务器返回相应的Cookie的信息的页面信息,给浏览器渲染.
5. 用户发送请求,不带有该Cookie,则服务器返回共用的页面信息,交给浏览渲染.

