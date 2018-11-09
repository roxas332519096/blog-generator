---
title: CSS布局套路
date: 2018-06-16 19:22:42
tags:
---
### CSS布局

#### 流程图:要支持IE8吗?

1. 是:float布局,定宽
2. 否:flex布局,弹性宽

#### Float布局

1. 给子元素加上float:left
2. 给父元素加上clearfix

clearfix

``` bash
.clearfix::after{
    content:'';
    display:block;
    clear:both;
}

 /兼容IE6/

.clearfix{
    zoom:1
}
```

#### 浮动实现平均布局

父元素变成祖先,建新的父元素,父元素加上一个负margin
``` bash
.pic{
    width:800px;
    margin:0 auto;
}
.pic > .item {
    width:194px;
    height:194px;
    margin:4px;
    float:left;
}
变成
.pic{
    width:800px;
    margin:0 auto;
}
.pic .xxx {
    margin-left:-4px;
    margin-right:-8px;
}
.pic > .xxx > .item{
    width:194px;
    height:194px;
    margin:4px;
    float:left;    
}
```

#### Flex布局

1. 给父元素加display:flex;
2. 给父元素加上justify-content:spance-between;

#### FLEX实现平均布局
``` bash
.pic{
    width:800px;
    margin:0 auto;
    display:flex;
    flex-wrap:wrap;
    justify-content:space-between;
}
.pic > .item {
    width:194px;
    height:194px;
    margin:4px;
}
```

##### 使用calc

百分之25,减去8像素

``` bash
width:calc (25% - 8px);
```

##### 如何防止banner图片变型

1. 不要用img标签

用background
``` bash
background:transparent url() no-repeat center;
background-size:cover;
```

2. 也可以搜索固定比例的div

