---
title: 'mixin,高阶函数,珂里化'
date: 2023-02-11 14:14:26
categories: 
- JS
tags: 
- JS
---

### mixin
将A对象属性给B就是mixin
```bash
const mixin = function(a,b){
    for(let key in b){
        a[key] = b[key]
    }
}

Object.assign(a,b)
```

### 珂里化
将关于x，y的函数，其中之一固定得到新的函数，其过程叫珂里化
一个函数返回另外一个函数
```bash
let f = function(x,y){return x+2*y}

let g = function(y){return f(1,y)}

let g = function(x){return f(x,y)}
//g(1)(2) 输出5

let cache = []
let add = function(n){
    if(n===undefined){
        return cache.reduce(p,n=>p+n,0)
    }else{
        cache.push(n)
        return add
    }
}
add(1)(2)(3)(4)() //输出10
```

### 高阶函数
传入一个函数，返回另外一个函数