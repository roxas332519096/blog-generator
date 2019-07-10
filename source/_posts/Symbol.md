---
title: Symbol&迭代器
date: 2019-07-09 09:52:16
categories:
- ES6
tags:
- ES6
---

#### Symbol
唯一值

``` bash
var a = new Symbol();
```

#### 迭代器

它提供一个next()方法,用来返回序列中的下一项.
迭代器对象一旦被创建,就可以反复调用next().

``` bash
function 生成器(){
    var _version = 0
    var max = 10
    return{
        next(){
             _version++
            return {
                version:_version
                done:false
            }
        }
    }
}
```

#### 生成器

迭代器生成的语法糖
``` bash
function* 生成器(){
    var version = 0;
    while(true){
        version += 1
        yield version
    }
}
```

#### for of
访问迭代器的语法糖

数组能迭代,对象不能迭代,因为数组有属性Symbol.iterator

``` bash
for(let key of array){
    console.log(key)
}

array[Symbol.iterator] //有值

for(let key of obj){
    console.log(key)
}//报错

obj[Symbol.iterator] //undefined
```
