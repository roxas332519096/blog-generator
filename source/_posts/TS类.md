---
title: TS类
date: 2020-01-09 10:56:36
categories:
- TS
tags:
- TS
---


1. 写一个ts的类
``` bash
class Human {
    name: string
    age: number
    constructor(name: string, age: number) {
        this.name = name
        this.age = age
    }
    move(): void {
        console.log('run')
    }
}

let tom = new Human('tom', 18)
```

2. 与interface的比较

``` bash
interface People {
    name: string
    age: number
    move(): void
}

let jack = {
    name: 'jack',
    age: 18,
    move(): void {
        console.log('run')
    }
}
```

3. 类的属性(static)

``` bash
    class Human {
        name: string
        age: number
        static xxx = 1 //在这里定义
        constructor(name: string, age: number) {
            this.name = name
            this.age = age
        }
        move(): void {
            console.log('run')
        }
    }

    let tom = new Human('tom', 18)
    console.log(Human.xxx) //应该这样使用
```

4. 类的继承

``` bash
class Animal {
    kind: string
    constructor(kind: string) {
        this.kind = kind
    }
}

class Human extends Animal {
    name: string
    age: number
    static xxx = 1
    constructor(name: string, age: number, kind: string) {
        super(kind) //执行super实际上是执行被父类的constructor
        this.name = name
        this.age = age
    }
    move(): void {
        console.log('run')
    }
}

let tom = new Human('tom', 18, '哺乳类')
```
5. 私用属性private,共有属性public

private不能外部调用,只能在类自身使用,可以想象成局部变量
public外部可以调用.(默认就是public,可以不加)

``` bash
class Human {
    public name: string
    age: number
    private secret: string
    constructor(name: string, age: number) {
        this.name = name
        this.age = age
        this.secret = 'self'
    }
    move(): void {
        console.log('run')
    }
}

let tom = new Human('tom', 18)
console.log(tom.secret) //报错
```

6. protected保护

只能在子类内使用

``` bash
class Animal {
    kind: string
    protected both: string //定义
    constructor(kind: string) {
        this.kind = kind
        if (this.kind === '哺乳类') {
            this.both = '胎生'
        }
    }
}

class Human extends Animal {
    name: string
    age: number
    static xxx = 1
    constructor(name: string, age: number, kind: string) {
        super(kind) //执行super实际上是执行被父类的constructor
        this.name = name
        this.age = age
    }
    move(): void {
        console.log('run')
    }
    say() {
        console.log(this.both) //在子类使用
    }
}

let tom = new Human('tom', 18, '哺乳类')
tom.say()
```

7. 访问器 get set

``` bash
      class Human {
        name: string
        private _age: number //首先把age变为私有属性
        get age() {//获取值,注意不能跟_age重名
            return this._age
        }
        set age(value: number) {//赋值,按照条件赋值
            if (value < 0) {
                this._age = 0
            } else {
                this._age = value
            }
        }
        constructor(name: string, age = 18) {
            this.name = name
            this.age = age
        }
    }

    let tom = new Human('tom')
    tom.age = -2
    console.log(tom.age) //0
```

8. 抽象类

抽象类是子类的父类,但方法没有写完,不能直接实例化

``` bash
 abstract class Animal {
        kind: string
        abstract say(): void //方法没有写完
    }

    class Human extends Animal {
        name: string
        age: number
        static xxx = 1
        constructor(name: string, age: number) {
            super()
            this.name = name
            this.age = age
        }
        say(): void {//补充完整方法
            console.log('hello')
        }
    }

    let tom = new Human('tom', 18)
```