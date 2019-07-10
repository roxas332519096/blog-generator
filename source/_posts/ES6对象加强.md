---
title: ES6对象加强
date: 2019-07-09 09:52:47
categories:
  - ES6
tags:
  - ES6
---

#### 定义属性支持短语法

```bash
var a = 1,
    b = 2,
var obj = {a,b}
obj = {
    a:1,
    b:2
}
```

#### 属性名支持表达式
``` bash
obj = {
        ["baz" + quux()] : 42
    }
```

#### 添加__proto属性,不建议使用