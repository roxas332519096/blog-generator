---
title: HTML基础
date: 2018-05-07 17:09:52
tags:
---

#### 1.什么是HTML?

全称：HyperText Markup Language（超文本标记语言）。

#### 2.空标签

空标签即不能包含子元素的标签。

如：input;img;meta;link;hr;br;col;colgroup;frame;base;等。

#### 3.可替换标签

CSS 里，可替换元素（replaced element）的展现不是由CSS来控制的。这些元素是一类外观渲染独立于CSS的 外部对象。

如：img;object;video;textarea;input

audio;canvas有时候也是。

#### 4.a

超链接，方法为get
##### 常用的可选属性如下：

##### href 锚（必须属性）
```` bash
<a href="url"></a> url可是绝对路径，可相对路径
<a href="#top"></a> 返回页面顶部
<a href="#"> </a>刷新页面
<a href="//"></a> 无协议,使用当前文件协议
<a href="javascripit:;"></a>伪js协议
````
##### target 
```` bash
<a href="#" target="aaa"> 在aaa窗口打开
<a href="#"  target="_self"></a> 当前页面加载
<a href="#" target="_blank"></a> 新窗口加载
<a href="#" target="_parent"></a> 父页面加载
<a href="#" target="_top"></a> 顶级页面加载，如祖父级，父级
````
##### download 下载
```` bash
<a href="xxx.com" download>
````
#### 5.ifame
镶嵌页面
```` bash
<iframe src="xxx.com" name="xxx"><iframe>
````
#### 6.form
表单
##### 常用属性：
##### action：
提交到哪儿 （必须）
1. 属性值为URL
2. #时是提交到本页面

##### methoh:
方法(必须)

1. get URI中以？作为分隔符，发送给服务器（会暴露）
2. post：发送内容出现在http第四部分。

##### target:
同a标签的target

#### 7.input

##### type属性：

##### text:输入文本
```` bash
<input type="text">
<input type="text"  placeholder="abcd"> #默认输入abcd
````
##### textarea：
```` bash
<textarea>ABCD</textarea>
````
##### password：输入密码
```` bash
<input type="password">
````
##### checkbox:多选 
```` bash
<input type="checkbox" name="g1" value="1" checked> #默认选1
<input type="checkbox" name="g1" value="2">
````
##### radio：单选
```` bash
<input type="radio" name="g2" value="1" checked> #默认选1
<input type="radio" name="g2" value="2">
````
##### 下拉选项
```` bash
<select name="select" multiple>可多选
    <option value="2">1</option>
    <option value="2" selected>2</option>  #默认选2
    <option value="3" disabled>3</option> #不能选3
</select>
````
##### button：
当没有submit时才会变成提交按钮
```` bash
<input type=“button” value=“button”>
<button>button</button>
````
##### sumbit：
提交按钮
```` bash
<input type="sumbit" value="button">
````
##### img：
图片提交按钮，必须使用sirc属性以及alt代替文本
##### color:
选择颜色
##### date：
选择日期(年月日，不包括时间)
##### datetime：
基于UTC时区的日期时间输入空间
##### email:
输入email
##### tel:
电话
##### file：
上传文件（accept属性控制类型）
属性 accept:
控制file的类型，形式如下accept=".jpg,png,doc"  点-格式-逗号
##### range:
用于输入不精确值空间
##### reset:
将表达所有内容设置为缺省值的按钮
##### search：
搜索，换行会自动移除

##### 其他属性:
##### name:
控件名称，用于提交到服务器，后端会识别
##### max：
最大值
##### mix：
最小值
##### maxlength:
最大长度
##### disabled：
不可选

##### laber
关联input：

1.for属性关联input的name属性
```` bash
<laber for="xxx">XXX<laber><input type="text" name="xxx">
````
2.包裹inputype
```` bash
<laber><input type="text"></laber>
````

####  8.table

表格
##### 例:
```` bash
<table>
    <colgroup>
    <col width=100>/colgroup>
    <thead>
        <tr>
            <th>Head<1/th>
            <th>Head2</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1</td>
            <td>2</td>
        </tr>
    </tobdy>
    <tfoot>
        <tr>
            <td>Foot1</td>
            <td>Foot2</td>
        </tr>
    </tfoot>
</table>
````
#### 9.head

##### head标签包含以下标签：

##### meta：
```` bash
<meta charset="utf-8">
````
##### titile：
窗口的标题。
##### base：指定一个文档包含所有相对URL的基本URL，只能有一个。
```` bash
<base href="http;//xxx.com">
<base target="_blank" href="http://xxx.com">
````
#### link：
引入css
```` bash
<link href="xxx.css" rel="stylesheet" title="xxx">
````
##### style：
使用css
```` bash
<style type="text/css">
    h1{color:red}
</style>
````
##### script：使用js
```` bash
<script type="text/javascript">document.write("Hi")</script>
````
##### noscript：
当浏览器不能允许js时允许。

