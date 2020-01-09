---
title: ES6对象
date: 2019-07-08 17:42:13
categories:
- ES6
tags:
- ES6
---

#### 生成空对象

##### 1. es5

```bash
var a = new Object()

var a = {}

{
    _proto_:
}
```

##### 2. es6

```bash
var a = Object.create(null)

{

}
```

es5 的还有原型,es6 是真正的空对象

#### 属性定义

##### 1. key 与属性相同可简写

```bash
var a = 1
    b = 2

var obj ={
    a,
    b
}
//
{
    a:1,
    b:2
}
```

##### 2. 使用变量作为 key

```bash
es5:

var name = 'a'
var obj = {}
obj[name] = 1
{
    a:1
}

es6:
var name = 'a'
var obj = {[name]:1}
{
    a:1
}
```

#### 4 方法定义

对象属性可以是一个函数,getter,setter 方法.

```bash
var obj = {
    _age:18
    get age(){return obj._age}
    set age(value){value < 100 ? obj._age = value : obj._age = 100}
}

obj.age = 1000
obj{
    age:100
}
```

#### 对象拷贝

Object.assign 与...

1. key 相同时,后面定义的覆盖前面的
2. 改变被拷贝对对象的属性假如是对象,只会拷贝引用地址,原对象也会改变
3. 仅拷贝可枚举对象.

```bash
var obj1 = {a:1,b:2,c:3,obj:{name:'a'}}
var obj2 = Object.assign({},obj1)

obj2.a = 100;
obj1.a //1
obj2.obj.name = 'b'
obj1.obj.name //b

var obj3 = {..obj1}
obj3 = {a:1,b:2,c:3}

obj3.a = 100;
obj1.a //1

var obj1 = {a:1,b:2,c:3}
var obj2 = {a:2,b:2,c:3,d4}
var obj3 = {...obj1,...obj2}

obj3 ={
    a:2,
    b:2,
    c:3,
    d4
}
```

#### Oject.definedProperty()

该方法会直接在一个对象上定义一个新属性,或修改一个属性的现有属性,并返回这个对象.

```bash
Object.definedProperty(obj,prop,descriptor)

Object.definedProperty(obj,'x',{
    get(){}
    set(value){}
})
```

##### 属性描述符

1. configurable
   是否可再次配置,默认 false

```bash
Object.definedProperty(o,'age',{writable:fasle})
o.age = 1;
o.age //undefined
Object.definedProperty(o,'age',{configurable:true})//报错
Object.definedProperty(o,'age',{writable:true})//报错

//刷新
Object.definedProperty(o,'age',{configurable:true})
Object.definedProperty(o,'age',{writable:fasle})
Object.definedProperty(o,'age',{writable:true})
```

2. enumrable
   是否能枚举,默认 false

```bash
var a = [1,2,3]
for(let key in a){
    console.log(key)//0,1,2
}

Object.definedProperty(a,'0',{enumrable:fasle})
for(let key in a){
    console.log(key)//1,2
}
```

3. value

4. writable
   属性是否可写入,默认 true

```bash
Object.definedProperty(o,'age',{writable:fasle})
o.age = 1;
o.age //undefined
```

5. get

```bash
Object.definedProperty(o,'age',{get(){
    return '100'
}})
o.age = 1;
o.age //100
```

6. set

```bash
Object.definedProperty(o,'age',{set(val){
    return val < 100 ? val : 100
}})
o.age = 1000;
o.age //100
```

#### Oject.definedProperties()

定义多个属性

```bash
Object.definedProperties(obj,{
    'a':{
        value:1,
        writable:true
    },
    'b':{
        value:2,
        writable:true
    }
})
```
