---
title: TS函数
date: 2020-01-10 23:50:49
categories:
- TS
tags:
- TS
---

函数:可以被调用的对象

#### 强制this

``` bash
    interface Human {
        name: string
        age: number
    }

    function fn(this: Human) {
        console.log(this)
    }

    fn.call({ name: 'tom', age: 18 }) //需要call
    
    fn() //报错
```

#### 重载

重载:一个函数有不同的调用形式
只支持不同类型的重载,不支持不同长度参数的重载.
如声明一个参数,那么只支持一个参数的重载.

``` bash
    function add(n1: number, n2: number)
    function add(n1: string, n2: string)
    function add(n1, n2) {
        return n1 + n2
    }

    add(1, 2)
    add('a', 'b')
    add(1,'2') //报错
```

#### 类型推断

TS会自己猜类型

``` bash
    function add(n1: string, n2: string) {
        return n1 + n2
    }

    let result = add('tom', 'jack').split('') //由于两个规定类型为string的参数相加为string,所以ts推断结果为string,拥有split方法
```

#### 类型兼容


``` bash
    interface Human {
        name: string
        age: number
    }

    let tom: Human = { name: 'tom', age: 18, gender: 'f' }//直接赋值会报错
    -----------------------
    let temp = { name: 'tom', age: 18, gender: 'f' } //使用中间变量,会触发TS的类型兼容
    let tom: Human = temp
```

