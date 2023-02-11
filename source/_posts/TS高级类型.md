---
title: TS高级类型
date: 2020-01-16 03:07:33
categories:
- TS
tags:
- TS
---

1. 且类型(交叉类型)

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

2. 或类型(联合类型)

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
```

3. 类型别名type

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


1. 字面量类型

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

5. this类型

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

6. 索引类型 keyof与T[K]

 索引访问操作符:T[K]表示对象T的key对应的类型的数组

``` bash
    function pluck<T, K extends keyof T>(object: T, keys: Array<K>): T[K][] {
        //T - {name:string,age:number,grade:number}
        //keyof T - 'name' | 'age | 'grade'
        //K extends keyof T - 'name' | 'age | 'grade'
        return keys.map(key => object[key])
    }

    interface Person {
        name: string
        age: number
        grade: number
    }

    type X = keyof Person

    pluck({ name: 'frank', age: 18, grade: 100 }, ['name', 'age'])
    //['frank'.18] => Array<T[K]> => T[K][]
```

7. Readonly 和 Partial

映射类型

``` bash
    interface Person {
        name: string
        age: number
    }

    type ReadonlyPerson = Readonly<Person> //所有key只读
    type PartialPerson = Partial<Person> //所有key可选
```

8. 可识别联合

需求1:从N选1

``` bash
    type Props = {
        actions: 'create'
        name: string
    } | {
        actions: 'update'
        name: string
        id: number
    }
```

需求2:我们需要识别出1还是2

`` bash
    type Props = {
        actions: 'create'
        name: string
    } | {
        actions: 'update'
        name: string
        id: number
    }

    function(props: Props) {
        if (props.actions === 'create') {

        } else {
            console.log(props.id)
        }
    }
```