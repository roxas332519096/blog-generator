---
title: ES6数组
date: 2019-07-24 16:21:58
categories:
  - ES6
tags:
  - ES6
---

#### Array.from
把不是数组的变成数组,常用语将伪数组变成数组.
```
Array.from({0:1,1:2}) //Array []

Array.from({0:1,1:2,length:2}) //Array [ 1, 2 ]

Array.from({0:1,1:2,length:3}) //Array(3) [ 1, 2, undefined ]

Array.from({0:1,1:2,length:1}) //Array [ 1 ]

Array.from({0:1,1:2,length:3}) //Array(3) [ 1, 2, undefined ]
```

##### ES5的方法
Array.prototype.slice.call()

#### Array.fill

将数组每项填充成传入的值,第一个参数是传入值,第二三参数是开始位置与结束位置

``` bash
[0,1].fill(2) //[2,2]

[0,1].fill(2,1) //[0,2]
['a','b','c','d'].fill('z',1,3) //[ "a", "z", "z", "d" ]
```

##### 生成有n个n的数组

``` bash
let length = Array.from({length:6})
length.fill(6)
[6,6,6,6,6,6]
```

#### Array.find
传入函数,返回匹配结果的项
``` bash
var arr = [{id:1,name:'a'},{id:2,name:'b'}]
arr.find(item=>{
  item.id === 1
})
//{id:1,name:'a'}
```

##### 与filter的区别
filter可找多个
``` bash
var arr = [{age:19,name:'a'},{age:18,name:'b'},{age:19,name:'c'}]
arr.filter(item=>{
  item.age === 19
})
//[{age:19,name:'a'},{age:19,name:'c'}]
```

#### Array.findIndex
返回匹配项的index

#### Array.entries/key/values
这3个api都是可得到数组的可迭代对象
``` bash
let arr = ['a','b','c']
let obj = arr.entries()
console.log(obj.next())[0,'a']
console.log(obj.next())[1,'b']
console.log(obj.next())[2,'c']


let arr = ['a','b','c']
let obj = arr.key()
console.log(obj.next())[0]
console.log(obj.next())[1]
console.log(obj.next())[2]

let arr = ['a','b','c']
let obj = arr.value()
console.log(obj.next())['a']
console.log(obj.next())['b']
console.log(obj.next())['c']
```

#### ...操作符

``` bash
let arr1 = ['a']
let arr2 = ['c']
let arr3 = ['b']

let arr4 = [...arr1,...arr2,...arr3] //['a','b','c']
```