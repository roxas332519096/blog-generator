---
title: Vue-修饰符
date: 2019-07-21 17:06:14
categories:
tags:
---

#### .stop
阻止事件的传播(冒泡,捕获)

``` bash
<template>
    <div @click.stop>
        <div></div>
        <button @click="a">Click</button>
    </div>
</template>
```

#### .sync
更新绑定属性
``` bash
<comp :title.sync="1"></comp>

//comp
data(){
    title:'childTitle'
},
mounted(){
    this.$emit('update:title',this.title)
}
```

#### native

#### .once
事件只触发一次

``` bash
    <div @click.once="a">
        111
    </div>
```

#### .self
事件是当前元素触发(内部触发不了)

``` bash
<div @click.self="a">
    <div>1</div>
    <div>2</div>
</div>
```