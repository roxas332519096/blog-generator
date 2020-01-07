---
title: TypeScript基础
date: 2019-12-17 22:40:20
categories: 
- TS
tags:
- TS
---

#### 安装

``` bash
npm install typescript -g //安装ts
npm install ts-node@7.0.0 -g //ts-node,让node可以运行ts
```

#### 使用


0. 先创建好ts文件
1. 根目录下创建文件 .vscode
2. .vscode下创建文件launch.json

3. 复制如下代码:

``` bash
{
    "configurations": [
        {
        "name": "ts-node",
        "type": "node",
        "request": "launch",
        "program": "C:/Users/Administrator/AppData/Roaming/npm/node_modules/ts-node/dist/bin.js",//这个是ts-node的安装路径
        "args": ["${relativeFile}"],
        "cwd": "${workspaceRoot}",
        "protocol": "inspector"
        }
    ]
}
```

4. 点击vscode工具栏调试(ctrl+shift+D)
5. 选择ts-node
6. 选好之前创建的ts文件,开启调试

#### 尝试用接口和类写一个简单的函数

``` bash
class Student {//类
    fullName: string;
    constructor(public firstName, public middleInitial, public lastName) {
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
}

interface Person {//接口
    firstName: string;
    lastName: string;
}

function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

const user = new Student("Jane", "M.", "User");

console.log(greeter(user))
```

编译之后

``` bash
var Student = /** @class */ (function () {
    function Student(firstName, middleInitial, lastName) {
        this.firstName = firstName;
        this.middleInitial = middleInitial;
        this.lastName = lastName;
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
    return Student;
}());
function greeter(person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}
var user = new Student("Jane", "M.", "User");
console.log(greeter(user));
```

#### 写一个简单的加法命令行

1. 在根目录下创建package.json
``` bash
npm init -y
```

2. 安装所需npm包

``` bash
npm install @types/node
```

3. 输入代码
``` bash
#!/usr/bin/env ts-node //这句话在写命令行的时候一定要加上
const a: number = Number(process.argv[2])
const b: number = Number(process.argv[3])

if (Number.isNaN(a) || Number.isNaN(b)) {
    console.log('只接受整数类型')
    process.exit(1)
}
console.log(a + b)
process.exit(0)
```

4. 运行命令行
``` bash
./add.ts 1 2

/////////////输出
```

#### 写一个族谱
``` bash
{
    class Person {
        public children: Person[] = []
        constructor(public name: string) { }
        addChild(child: Person): void {
            this.children.push(child)
        }
        introduceFamily(n?: number): void {
            n = n ? n : 1
            let prefix = '----'.repeat(n - 1)
            console.log(`${prefix}${this.name}`)
            this.children.forEach((child) => {
                child.introduceFamily(n + 1)
            })
        }
    }

    const grandpa = new Person('爷爷')
    const child1 = new Person('大儿子')
    const child2 = new Person('二儿子')
    const person11 = new Person('大孙子')
    const person12 = new Person('二孙子')
    const person21 = new Person('三孙子')
    const person22 = new Person('四孙子')
    grandpa.addChild(child1)
    grandpa.addChild(child2)
    child1.addChild(person11)
    child1.addChild(person12)
    child2.addChild(person21)
    child2.addChild(person22)

    grandpa.introduceFamily()
}


///输出
爷爷
----大儿子
--------大孙子
--------二孙子
----二儿子
--------三孙子
--------四孙子
```