---
title: TS声明
date: 2020-01-17 01:33:03
categories:
- TS
tags:
- TS
---

#### 如何写一个TS声明文件

test.ts

``` bash
export interface Person {
    name: string
    age: number
}

const a = function (p: Person) {
    console.log(p)
}

export default a

```

``` bash
tsc test.ts -d
```

生成test.d.ts文件,就是声明文件
-d的全称是declaration(声明)

#### 如何提供给别人使用 *.d.ts

库:在package.json添加types字段

``` bash
{
  "name": "ts",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "type":"main.d.ts",//添加这里
}

```
社区:上传到DefinitelyTyped

#### 如何给任意JS添加声明

##### require方式

v.js
``` bash
function add(a, b) {
    return a + b
}

export default add
```

tsconfig.json

``` bash
{
    "compilerOptions": {
        "types": [
            "node"
        ],
        "typeRoots": [
            "node_modules/@types"
        ]
    }
}
```

test.ts
``` bash
{
    interface V {
        (a: number, b: number): number
    }

    const add: V = require('./v.js')

    add(1, 2)
}
```

#### import 方式

test.ts

``` bash
import add from './v.js'

add(1, 2)
```

test.d.ts
``` bash
declare function y(a: number, b: number): number
export default y
```

#### 如何修改window全局变量

``` bash
declare global {
    interface Window{
        server:{
            host:string
        }
    }
}
```