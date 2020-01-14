---
title: TS泛型
date: 2020-01-11 20:37:55
categories:
-TS
tags:
- TS
---

#### 代表广泛的类型

``` bash
function identity<T>(arg:T):T{
    return arg
}

let string = identity('hi')
```

#### 接口使用泛型

``` bash
    function returnIt<T>(arg: T): T {
        return arg
    }

    interface Human {
        name: string
        age: number
    }

    let human = returnIt<Human>({ name: 'tom', age: 18 })
```

#### 数组泛型
``` bash

    interface Human {
        name: string
        age: number
    }

    function returnArray<T>(array: T[]): T[] {
        return array
    }

    let array = returnArray<string>(['a', 'b', 'c'])

    let humanArray = returnArray<Human>([{ name: 'tom', age: 18 }, { name: 'jack', age: 19 }])
```

#### 泛型类型

``` bash
    function returnIt<T>(arg: T): T {
        return arg
    }

    let myReturnIt: <T>(arg: T) => T = returnIt
    let myReturnIt2: { <T>(arg: T): T } = returnIt
```

#### 泛型接口

``` bash

    interface AnyAdd<T> {
        (a1: T, b1: T): T
    }

    let numberAdd: AnyAdd<number> = (a1: number, b1: number): number => {
        return a1 + b1
    }

    let stringAdd: AnyAdd<string> = (a2: string, b2: string): string => {
        return a2 + b2
    }
```

#### 泛型约束

满足某些条件的约束

假如这样写,会报错,因为不一定有length,那么我们需要对泛型进行约束

``` bash
    function returnIt<T>(arg: T): T {
        console.log(arg.length) //这里报错
        return arg
    }
```

引用接口,找到约束的类型

``` bash
    interface hasLength {
        length: number
    }

    function returnIt<T extends hasLength>(arg: T): T {//T继承接口hasLength
        console.log(arg.length)
        return arg
    }
```

#### 在泛型里使用类


``` bash
 function create<T>(c: { new(): T }): T {
        return new c()
    }
```

看不懂?那先转化为js代码

``` bash

    function create(c) {
        return new c()
    }
```

``` bash
 function create<T>(c: { new(): T }): T {
        return new c()
    }

    class Human {

    }

    class Animal {

    }

    let tom = create<Human>(Human)
    let jack = create<Human>(Animal) //报错,因为是Human
```