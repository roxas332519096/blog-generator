---
title: ES6变量声明
date: 2019-07-08 12:17:27
categories:
- ES6
tags:
- ES6
---

#### let

1. 作用声明局部变量 ,作用域在最近的{}之间.
2. 不会进行变量名声明提升
3. 不能重复声明

在es6之前,声明局部变量要使用立即执行函数

``` bash
{
    let a = 1
}
console.log(1) //报错


{
    let a = 1
    {
        console.log(a)//报错
        let a =2
    }
}

{
    let a = 1;
    let a = 2;//报错
}
```

#### const

同let,但只有一次赋值机会,必须在声明的时候赋值.
{
    const a //报错
}

#### 面试题

1. 
``` bash
for(var i = 0;i < 6;i++){
    ///
}
console.log(i);/6
```
解:
``` bah
变成
var i
for(i = 0;i < 6;i++){
    0,1,2,3,4,5
}
console.log(i);/6
```

2. 
``` bash
for(var i = 0;i < 6;i++){
    function fn(){
        console.log(i)
    }
    button.onclick = fn//因为执行的时候i已经变成6了.
}
6
```
3.
``` bash
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
</ul>

var liTags = document.querySelectorAll('li');
for(var i = 0;i<liTags.length;i++){
    liTags[i].onclick = function(){
        console.log(i);//不管点哪个按钮,都是6
    }
}

改成

for(var i = 0;i<liTags.length;i++){
    (function(){
        var j = arguments[0];//外面的i赋值给j
        liTags[i].onclick = function(){
            console.log(j)//点哪个打印哪个
        }
    })(i)
}

或者

for(var i = 0;i<liTags.length;i++){
    let j = i;
    liTags[j].onclick = function(){
        console.log(j)//点哪个打印哪个
    }
}

或

for(let i = 0;i<liTags.length;i++){
    liTags[i].onclick = function(){
        console.log(i);//点哪个打印哪个
    }
}
```