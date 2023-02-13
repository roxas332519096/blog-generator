---
title: TS类型
date: 2020-01-16 03:07:33
categories:
- TS
tags:
- TS
---

### 类型
```bash
    type Name = String
    type FasleLike = '' | 0 | false | null | undefined
    type Ponit = {x: number,y: number}
    type Ponits = Ponit[]//数组
    type Line = [Ponit, Ponit]//元祖
    type Circle = { center: Ponit, radius: number }
    type Fn = (a: number, b: number) => number
    type FnWithProps = {
        (a: number, b: number): number
        prop: number
    }
```

### 类型别名type

给类型取别名,跟接口很像

区别
    1. interface只描述对象，type则描述所有数据
    2. type只是别名，interface则是类型声明
    3. 对外API尽量用interface，方便扩展，对内API尽量用type，防止代码分散

``` bash
    type Age = number
    const age: Age = 18

    type Name = string
    const name: Name = 'tom'

    type A = {
        name: string
    }

    interface B {
        name: string
    }

```

### 字面量类型

通常用来作可选项

``` bash
    interface Course {
        category: 'task' | 'live'
    }

    const course: Course = {
        category: 'task'
    }

    type Dir = 'east' | 'west' | 'north' | 'south'

    const dir: Dir = 'east'

    type A = 1 | 2 | 3 | 4 | 5 | 6
    const a: A = 1
```

### 索引签名
```bash
type Hash = {
    [k:string]:unknown
    length:number
}

```
### 映射类型
多用于泛型
```bash
type Hash = {
    [k in string]:unknown
}
```
### 且类型(交叉类型)

两种类型都需满足

``` bash
    interface human {
        name: string
        age: number
    }

    interface student {
        name: string
        id: number
    }

    let tom: human & student = {
        name: 'tom',
        age: 18,
        id: 123
    }


```

### 或类型(联合类型)

满足一种类型即可

``` bash
    interface human {
        name: string
        age: number
    }

    interface student {
        name: string
        id: number
    }

    let tom: human | student = {//满足两种
        name: 'tom',
        age: 18,
        id: 123
    }

    let jack: human | student = {//满足一种
        name: 'jack',
        age: 19
    }
    type A1 = number
    type B1 = string
    type C1 = A1 | B1

    type A2 = {name:string}
    type B2 = {age:number}
    type C2 = A2 | B2
    const c2:C2 = {
        name:'John',
        age:18
    }
    const c3:c2 = {
        name:'John'
    }
```
#### 类型收窄

1. js方法：type of instanceof
2. Ts方法：is
3. Ts方法（可辨别联合）：x.kind
```bash
    interface Circle { kind: 'circle', radius: number }
    interface Square { kind: 'square', sideLength: number }
    type Shape = Circle | Square;
    const f1 = (shape: Shape) => {
        if (shape.kind === 'circle') {
            shape //Circle
        } else if (shape.kind === 'square') {
            shape //Square
        } else {
            shape //Never
        }
    }
```
4. Ts方法：断言
```bash
let b :unknown = await axios(...)
(b as number).toFixed();
```

### this类型

自动判断this类型(多态)

``` bash
    class Calc {
        public n: number
        constructor(n: number) {
            this.n = n
        }
        add(n: number) {
            this.n += n
            return this
        }
    }

    let calc = new Calc(1)
    calc.add(2).add(4) //自动判断this是number,可以用add

    console.log(calc) //7
```

ts的this可以推断类型
下面的this返回的是BiggerCalc的this,而不是Calc的this,因为他有sin方法

``` bash
    class Calc {
        public n: number
        constructor(n: number) {
            this.n = n
        }
        add(n: number) {
            this.n += n
            return this
        }
    }

    class BiggerCalc extends Calc {
        sin() {
            this.n = Math.sin(this.n)
            return this
        }
    }

    let calc = new BiggerCalc(1)
    calc.add(2).add(4).sin().add

    console.log(calc) //0.6569865987187891
```

