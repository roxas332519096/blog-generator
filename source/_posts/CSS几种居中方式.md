---
title: CSS几种居中
date: 2018-05-07 17:50:31
categories:
- CSS
tags:
- CSS
---
### 几种居中布局

网页预览:
https://roxas332519096.github.io/center-in-css-demo/%E5%87%A0%E7%A7%8D%E5%B1%85%E4%B8%AD%E5%B8%83%E5%B1%80.html

源码:
https://github.com/roxas332519096/center-in-css-demo/blob/master/%E5%87%A0%E7%A7%8D%E5%B1%85%E4%B8%AD%E5%B8%83%E5%B1%80.html

#### 水平居中

##### 内联元素

子元素是内联元素或文本等,在父元素上设置text-align:center;

代码:
``` bash
.inline-horizontally{
    text-align: center;
}

<div class="inline-horizontally">
    <span>这是一个内联文本</span>
    <nav>
        <a href="#">1</a>
        <a href="#">2</a>
        <a href="#">3</a>
        <a href="#">4</a>
        <a href="#">5</a>
    </nav>
</div>
```

##### 块状元素

##### 拥有固定宽度的块状元素

块状元素拥有固定宽度,可将左右边距设置成auto.

``` bash
.block-horizontally{
    width: 50%;
    margin-left: auto;
    margin-right: auto;
}

<div class="block-horizontally">
    这是一个拥有固定宽度的块状元素
</div>
```

##### 多个没宽度的块状元素居中

多个块状元素没有固定,子元素设置成inline-block,父元素text-algin:center.

``` bash
.block-horizontally-moreThanOne-inline-block{
    text-align: center;
}
.block-horizontally-moreThanOne-inline-block > div {
    display: inline-block;
}

 <div class="block-horizontally-moreThanOne-inline-block">
    <div>One</div>
    <div>Two</div>
    <div>Three</div>
</div>
```

##### 多个没宽度的块状元素居中,flex 

父元素设置成flex,justify-content: center.

``` bash
.block-horizontally-moreThanOne-flex{
    display: flex;
    justify-content: center;
}
```

#### 垂直居中

##### 单行内联元素垂直居中

设置上下padding设置成一样

``` bash
.inline-signle-padding{
    padding-top:50px;
    padding-bottom:50px;
}
```

##### 单行内联元素垂直居中

用line-height = height

``` bash
 .inline-signle-line-heght{
    height: 100px;
    line-height: 100px;
}
```

##### 多行内联元素用flex,垂直左右居中

``` bash
.inline-multiple-flex{
    display: flex;
    justify-content: center;
    flex-direction: column;
}
```

##### 块状元素已知高度

用定位,子元素top 50%

``` bash
.block-height-postion{
    position: relative;
    height: 200px;
}
.block-height-postion div{
    position: absolute;
    top:50%;
    height: 100px;
}
```

##### 块状元素高度未知

用定位+子元素transform:translateY(-50%)

``` bash
.block-unknowheight-postion-transform-translateY{
    position: relative;
    height: 200px;
}
.block-unknowheight-postion-transform-translateY div{
    position: absolute;
    top:50%;
    transform: translateY(-50%);
}
```