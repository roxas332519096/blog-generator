---
title: ES6字面量 Literal
date: 2019-07-09 09:52:39
categories:
- ES6
tags:
- ES6
---

#### 八进制
``` bash
ES5
07 //7

ES6
0o7 //7
```

#### 字符串支持unicode

 ES5部分支持,只能存2字节字符串(16位2进制)
 1字节=16进制

 ``` bash
 '\ud834\udf06' //𝌆

 '\ud834\udf06'.length //2
 ```

ES6

1. String.fromCodePonit
    Unicode码返回对应字符串

2. String.prototype.codePonitAt()
    字符串返回对应Unicode码
