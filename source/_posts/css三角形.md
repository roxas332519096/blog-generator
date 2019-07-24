---
title: css三角形
date: 2019-07-20 11:18:03
categories:
- CSS
tags:
- CSS
---

#### 普通三角形

利border四边颜色不等画等边三角形

``` bash
.triangle{
    width:0;
    height:0;
    border: 10px solid transparent;
}
.triangle.top{//向上
    border-bottom-color: #000;
}
.triangle.bottom{//向下
    border-bottom-color: #000;
}
.triangle.left{//向左
    border-left-color: #000;
}
.triangle.right{//向右
    border-right-color: #000;
}
```

#### 常见应用:盒子下创建小三角形
利用伪元素
``` bash
.wrapper{
    position: relative;
    width:100px;
    height:100px;
    background:#fff;
    border:1px solid #000;
    &::before,&::after{
        content: "";
        display: block;
        position: absolute;
        width:0;
        height:0;
        border: 10px solid transparent;//三角形边长
    }
    &::before{
        top: 100%;//位于盒子底部
        border-top-color: #000;//三角形边框
    }
    &::after{
        top: calc(100% - 1px);//三角形border宽度
        border-top-color:#fff;//三角形背景
    }
}
```
