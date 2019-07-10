---
title: ES6模块化
date: 2019-07-09 12:15:07
categories:
- ES6
tags:
- ES6
---

#### import
``` bash
<script type="module" src="main.js"></script>

//main.js

import module1 from './module1.js'
import module2 from './module2.js'
import abc from 'abc.js'

setTimeout(()=>{
    module1(abc);
    module2();
},3000)

//moudule1
export default function(){
    //
}

//moudule2
export default function(){
    //
}

//abc
let a = ['a']
 export default a
```

##### 单纯引入
直接执行模块里的代码,函数不执行,调用函数需要export
``` bash
//module
console.log('code')

function x(){
    console.log('function')
}

//main.js
import './module'

//code
```

#### export
默认导出的,引用时可以任意命名,具体的要使用具体的名字.
``` bash
//modules

let name = 'myname'
let age = 18
let sayhi = function(){
    console.log(hi)
}
export default sayhi
export {name,age}

//main

import xxx {name ,age} from './modules'
console.log(xxx()) //hi
console.log(name,age) // 'myname' 18
```

#### as
当导出命名重复时,需要as,否则报错
``` bash
//modules1
let name = '小明'
export name
//modules2
let name = '小红'
export name

//main.js
import {name as name1} from './module1.js'
import {name as name2} from './module2.js'
console.log(name1,name2) //小明小红
```

#### *

全部导出

``` bash
import * as x from './modules'
```
