---
title: 'TS变量,接口'
date: 2020-01-08 14:06:27
categories:
- TS
tags:
- TS
---

#### 类型

跟JS一样

``` bash
let a:string = 's'
let b:number = 1
let c:boolean = true
let d:object = {}
let e:null = null
let f:undefined = undefined

//any(任何类型)

let any1:any = 1
let any2:any = 'b'
any1 = {}
any2 = true
```

### 类型

#### 枚举

1. 不赋值
``` bash
enum Gender {
        Man,
        Woman
    }

let gender: Gender = Gender.Woman
console.log(gender) //1
gender = Gender.Man
console.log(gender) //0
```

2. 赋值

``` bash
enum Gender {
        Man = 'Man',
        Woman = 'Woman'
    }

let gender: Gender = Gender.Woman
console.log(gender) //Woman
gender = Gender.Man
console.log(gender) //Man
```
#### void
函数没有返回值
``` bash

function test():void{
    console.log(1)
}

let a:number = test() //会报错

```


#### never


默认情况下null和undefined是所有类型的子类型.例如,null可以赋值给number类型的变量.

### 断言

自己主观认为变量是哪个类型

``` bash
let a:any = '123'
console.log((<string>a).split(''))
```

### 接口

描述一个对象必须有什么属性(方法)

``` bash
    interface Shape {
        head: string,
        body: string
    }

    interface Human {
        name: string
        age: number,
        shape: Shape,
        say(word: string): void
    }

    let tom: Human = {
        name: 'tom',
        age: 28,
        shape: {
            head: '头',
            body: '身体'
        },
        say(word: string) {
            console.log(word)
        }

    }
    tom.say('hello')
```

1. readonly 

不能更改

``` bash
interface Human {
    readonly name: string
    age: number
```

2. 可选属性

``` bash
interface Human {
    readonly name: string
    age: number,
    like?:Array<string>
```

3. 假如额外传入参数

``` bash
  interface Config {
        color?: string,
        width?: number
    }

    function created(config: Config): void {
        console.log(config)
    }

    created({
        age: 'red'
    })

    //会报错
```

要使用字符串索引签名

``` bash
interface Config {
        color?: string,
        width?: number,
        [propName: string]: any  //添加这一行,意思是key为字符串类型,value为any类型
    }

    function created(config: Config): void {
        console.log(config)
    }

    created({
        age: 'red'
    })
```

4. 使用接口描述一个函数

注意,接口定义参数名只是一个顺序,跟实际函数变量名没有关系

``` bash
    interface Operation {
        (number1: number, number2: number): number
    }

    let add: Operation = function (n1: number, n2: number): number {
        return n1 + n2
    }
    let result: number = add(1, 2)
    console.log(result)
```

5. 接口继承

``` bash
interface Animal {
    move(): void
}

interface Human extends Animal {
    name: string
    age: number
}

let tom: Human = {
    age: 18,
    name: 'tom',
    move() {
        console.log('move')
    }
}

tom.move()
```

一个接口可以继承多个接口
``` bash
    interface Animal {
        move(): void
    }

    interface 有机物 {
        c: true
        h: true
        o: true
    }

    interface Human extends Animal, 有机物 {
        name: string
        age: number
    }

    let tom: Human = {
        c: true,
        h: true,
        o: true,
        age: 18,
        name: 'tom',
        move() {
            console.log('move')
        }
    }
```