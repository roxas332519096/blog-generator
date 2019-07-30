---
title: css3伪类
date: 2019-07-31 00:04:54
categories:
- CSS
tags:
- CSS
---

### :target 选择页面局部

假如锚点与页面的hash匹配(#),那么对应元素可用:target定义样式

``` bash
<h2 id="rotnruin">Rot &amp; Ruin</h2>
<h2 id="romero">Romero Zombies</h2>
<ul>
    <li><a href="#rotnruin">Rot &amp; Ruin</a></li>
    <li><a href="#romero">Romero Zombies</a></li>
    ...
</ul>

h2:target {
    background: rgb(125,104,99);
    border: 0;
    color: rgb(255, 255, 255);
    padding-left: 10px;
}

//如果此时点击href="#romero"的a标签,那么对应的h2会高亮.
```

### :not 过滤掉不符合的元素

:not(x) x可以应用几乎所有选择器的语法
:not可搭配其他伪类使用,如p:not(:empty)选择非空元素
``` bash
<p id="p1">aaa</p>
<p id="p2">bbbb</p>
<p id="p3">ccccc</p>
<p id="p4">dddddd</p>

p:not(#p1):not(#p3) {color: red;}
```

### 根据索引选择元素

索引相对所有同级兄弟元素计算的,而非特定类型

#### :first-child 和 :last-child

``` bash
<div>
    <h1>Hi</h1>
    <h2>Apple</h2>
    <h2>Banana</h2>
    <h2>ApplePen</h2>
    <h2>Pen</h2>
</div>

h1:first-child {} /*Hi*/
h2:first-child {} /*匹配不到*/
h2:last-child {} /*Pen*/
```

#### :nth-child()

接收单一参数,可以是以下值

``` bash
odd 奇数
even 偶数
n 第n个
An+B A为整数,n从0开始算,B为整数,计算结果小于1的忽略
```

``` bash
li:nth-child(3n) //3 6 9 12
li:nth-child(3n+1) //4 7 10 13
li:nth-child(-3n+1) //1
li:nth-child(-n+5) //5 4 3 2 1 
```

#### :nth-last-child()

同上,但从最后一个元素开始反向计算

#### :only-child

匹配相对于父元素类型唯一的子元素

#### :empty

匹配空的元素,假如有空格,则不匹配.

### 根据索引选择特殊类型的元素

:first-of-type
:last-of-type
:only-of-type
:nth-of-type()
:nth-last-of-type()

基本用法和 *-child 一样

和 *-child 不同的是， 索引只针对选择器指定的类型，而非同级的所有兄弟元素

### 表单元素

#### :enabled 和 :disabled

匹配元素是否有disabled属性

#### :required 和 :optional

匹配元素是否有required属性


#### :checkd

只作用于radio 和 checkbox

#### :in-range 和 :out-of-range

作用于type = range/number/date的input

#### :valid 和 :invalid

依赖于 input 的 type类型 和 pattern约束,判断是否校验通过
可以组合使用,如 input:focus:invalid
