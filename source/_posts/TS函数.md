---
title: TS函数
date: 2020-01-10 23:50:49
categories:
- TS
tags:
- TS
---

函数:可以被调用的对象

#### 函数的几种写法

```bash
    //先写类型再赋值
     type F = {
        (a: number, b: number): number
    }
    let f: F = (a, b) => a + b

    type F1 = (a: number, b: number) => number
    let f1: F1 = (a, b) => a + b

    interface F2 {
        (a: number, b: number): number
    }
    let f2: F2 = (a, b) => a + b


    //先写函数，再获取类型
    const f1 = function (a: number, b: number): number {
        return a + b
    }
    type F1 = typeof f1

    function f2(a: number, b: number): number {
        return a + b
    }
    type F2 = typeof f2

    const f3 = (a: number, b: number): number => {
        return a + b
    }
    type F3 = typeof f3
```

#### 类型谓词

类型收窄

```bash
    type Person = {
        name: string
    }
    type Animal = {

    }
    function f1(a: Person | Animal) {
        if (isPerson(a)) {
            a//类型是Person
        }
    }
    function isPerson(x: Person | Animal): x is Person {
        return 'name' in x
    }
```

#### 可选参数

```bash
    function addEventListener(
        eventType: string, fn: (e: Event, el: Element) => void, useCaptrue?: boolean
    ) {
        if (useCaptrue === undefined) {
            useCaptrue = false
        }
        const element = {} as Element
        const event = {} as Event
        fn(event, element)
        console.log(event, fn, useCaptrue)

    }
    addEventListener('click', (e, el) => { })
```

#### 珂里化

```bash
    const add = (a: number, b: number) => a + b

    const createAdd = (a: number) => (b: number) => a + b
    
    createAdd(1)(2)
```

#### 重载(overload)

同名的函数，参数不同（类型不同或者参数个数不同）

``` bash
    function add(n1: number, n2: number): number
    function add(n1: string, n2: string): string
    function add(n1, n2) {
        return n1 + n2
    }

    add(1, 2)
    add('a', 'b')
    add(1, '2') //报错

    function createDate(n: number): Date;
    function createDate(y: number, m: number, d: number): Date;
    function createDate(a: number, b?: number, c?: number): Date {
        if (a !== undefined && b !== undefined && c !== undefined) {
            return new Date(a, b, c)
        } else if (a !== undefined && b === undefined && c === undefined) {
            return new Date(a)
        } else {
            throw new Error('error')
        }
    }
```

#### 指定函数的this

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

#### 剩余参数

```bash
    function sum(...array: number[]) {
        return array.reduce((n, p) => n + p, 0)
    }
    sum(1)
    sum(1, 2)
    sum(1, 2, 3)
```

#### 展开参数

```bash
    function sum(name: number, ...array: number[]) {
        f(...array)
    }
    function f(...array: number[]) {
        console.log(array)
    }
```

#### 参数析构

```bash
    type Config = {
        url: string,
        method: 'GET' | 'POST'
        data: unknown,
        headers: unknown
    }
    function ajax({ url, method, ...rest }: Config) {
        console.log(url, method)
    }
    //加默认值
    function ajax({ url, method, ...rest }: Config = { url: '', method: 'GET' } as Config) {
        console.log(url, method)
    }
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

