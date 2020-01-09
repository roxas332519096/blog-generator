---
title: Promise的使用 & async awit
date: 2019-01-18 21:39:10
categories:
- ES6
tags:
- ES6
---

### Promise

#### Promise 的作用

当一个异步函数执行的时候,需要回调,可使用 Promise 链式操作进行回调.

例子:

```bash
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

```

fn1(()=>{
    fn2(()=>{
        fn3
    })
})
//控制台一秒后输出 fn1,再一秒后输出 fn2,再一秒后输出 fn3
```

因为回调函数复杂的时候非常麻烦,所以我们可以使用 promise 改写上面的函数

#### Promise 语法

```bash
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

构造函数 Promise 接收一个参数 function,function 接收两个参数,一个是成功时执行的函数,一个是失败时执行的函数.
通过链式操作,我们可以分别对不同的结果分别执行不同的回调函数.

通过 promise 改写上面的函数

```bash
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

```bash
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

当有几个 promise 的时候,我们可以用 promise.all 让所有 promise 状态变更之后再回调

then 的第一个参数是所有成功才执行,第二个参数是只要有一个失败就执行

```bash
Promise.all([p1,p2,p3]).then((res1,res2,res3)=>{},(res1,res2,res3)=>{})
```

#### Promise.race

当有几个 promise 的时候,我们可以用 promise.race 来获取最快/成功 promise 的 resolve

```bash
Promise.race([p1,p2,p3]).then(()=>{})
```

#### Promise.reject()

```
Promise.reject("Testing static reject").then((reason)=>{
  // 未被调用
}, (reason) => {
  console.log(reason); // "Testing static reject"
});

Promise.reject(new Error("fail")).then((result)=>{
  // 未被调用
}, (error)=>{
  console.log(error); // stacktrace
});
```

#### finally

当 promise 状态变更的时候时候,不管成功与失败,我们都可以执行同一个方法

```bash
.finally(loading=>{
    loding = false
})

等价于
.then(loading=>{loading = fasle},loading=>{loading = fasle})
```

```bash
promiseFn().finaly({}=>{
    console.log('异步结束')
})
```

#### catch

只处理错误

```bash
.catch(error=>{
    console.log(error)
})

等价于

.then(null,(error)=>{
    console.log(error)
})
```

### async await

#### await

等待 promise 结束,并返回 resolve 的值

```bash
function isDog(name){
    return new Promise((resove,reject)=>{
        setTimeout(()=>{
           if(name === 'dog'){
               resove('yes')
           }else{
               reject('no')
           }
        },1000)
    })
}

 let isWhat = await isDog('dog') //'yes'
```

#### async

所有 async 函数都会隐式返回 promise 对象

```bash
async function test(){
    let isWhat = await isDog('dog')
    console.log(isWhat) //yes
}
```

#### 使用 async 函数,使用 try catch 获取 promise 结果

```bash
function isDog(name){
    return new Promise((resove,reject)=>{
        setTimeout(()=>{
           if(name === 'dog'){
               resove('yes')
           }else{
               reject('no')
           }
        },1000)
    })
}

async function test(name){
    try{
        let isWhat = await isDog(name)
        console.log(isWhat)
    }catch(error){
        console.log(error)
    }

}

test('dog') //yes
test('cat') //no
```

##### 使用 async 函数获取两以个 promise 结果

只有当两个 promise 都成功时,await 才会赋值,否则进入 catch

```bash
function isDog(name){
    return new Promise((resove,reject)=>{
        setTimeout(()=>{
           if(name === 'dog'){
               resove('yes')
           }else{
               reject('no')
           }
        },1000)
    })
}

async function test(name1,name2){
    try{
        let isWhat = await Promise.all([isDog(name1),isDog(name2)])
        console.log(isWhat)
    }catch(error){
        console.log(error)
    }

}

test('dog','dog') //[yes,yes]
test('dog','cat') //no
test('cat','cat') //no
```
