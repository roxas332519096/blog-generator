---
title: 'TS变量,接口,类'
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

定义必须有的属性或者方法

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
    age: number,
    shape: Shape,
    say(word: string): void
    }
```