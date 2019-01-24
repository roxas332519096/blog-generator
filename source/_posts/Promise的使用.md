---
title: Promise的使用
date: 2019-01-18 21:39:10
tags:

#### 1. Promise的作用

当一个异步函数执行的时候,需要回调,可使用Promise链式操作进行回调.

例子:
``` bash
function fn1(callback){
    setTimeout(()=>{
        console.log('fn1执行')
    },1000)
}

function fn1(callback){
    setTimeout(()=>{
        console.log('fn2执行')
        callback()
    },1000)
}

function fn1(){
    setTimeout(()=>{
        console.log('fn3执行')
        callback()
    },1000)
}
```

我们以前是这样回调的

fn1(()=>{
    fn2(()=>{
        fn3
    })
})

//控制台一秒后输出fn1,再一秒后输出fn2,再一秒后输出fn3

因为回调函数复杂的时候非常麻烦,所以我们可以使用promise改写上面的函数

#### 2. Promise语法

``` bash
function promiseFn(){
    return new Promise((resolve,reject)=>{
        //当异步函数执行成功时
        resolve();
        //当异步函数执行失败时,
        reject();
    })
}

promiseFn().then(()=>{}).catch(()=>{})
```

构造函数Promise接收一个参数function,function接收两个参数,一个是成功时执行的函数,一个是失败时执行的函数.
通过链式操作,我们可以分别对不同的结果分别执行不同的回调函数.

通过promise改写上面的函数

``` bash
function fn1(){
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log('fn1执行')
            resolve()
        }, 1000)
    })
}

function fn2(){
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log('fn2执行')
            resolve()
        }, 1000)
    })
}

function fn3(){
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log('fn3执行')
            resolve()
        }, 1000)
    })
}

function onerror() {
    console.log('error')
}

fn1().then(fn2).then(fn3).catch(onerror)
```

当异步函数执行时,下一个异步函数需要用上一个异步函数的返回值可以这样写
``` bash
//定义函数获取城市
function getCity(ip){
    return new Promise((resolve,reject)=>{
        let xhr = new XMLHttpRequest();
        xhr.open('GET',url/ip,true)
        xhr.onload = function(){
            var data = JSON.parse(xhr.responseText) //获得数据
            resolve(data)
        }
        xhr.onerror = function(){
            reject('获取失败')
        }
        xhr.send()
    })
}
//定义函数获取天气
function getWeather(city){
    return new Promise((resolve,reject)=>{
        let xhr = new XMLHttpRequest();
        xhr.open('GET',url/city,true)
        xhr.onload = function(){
            var data = JSON.parse(xhr.responseText)
        }
        xhr.onerror = function(){
            reject('获取失败')
        }
        xhr.send
    })
}

//调用

getCity(上海).then((city)=>{
    return getWeather(city)
}).then((res)=>{
    console.log(res)
}).catch((error)=>{
    console.log(error)
})

```

#### Promise.all

当有几个promise的时候,我们可以用promise.all让所有promise状态变更之后再回调

``` bash
Promise.all([p1,p2,p3]).then(()=>{})
```

#### Promise.race

当有几个promise的时候,我们可以用promise.race来执行最快的返回的一个promise对象的函数
``` bash
Promise.race([p1,p2,p3]).then(()=>{})
```

#### finaly

当promise状态变更的时候时候,不管成功与失败,我们都可以执行同一个方法

``` bash
promiseFn().finaly({}=>{
    console.log('异步结束')
})
```
