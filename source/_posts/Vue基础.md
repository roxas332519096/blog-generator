---
title: Vue基础
date: 2018-07-13 23:05:15
tags:
---
### 简介

#### MVVM是什么?

MVVM是Model-View-ViewModel的缩写。MVVM是一种设计思想。Model 层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；View 代表UI 组件，它负责将数据模型转化成UI 展现出来，ViewModel 是一个同步View 和 Model的对象。

在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。

ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。


#### Vue.js优点

Vue.js是一个轻巧,高性能,可组件化的MVVM库.它是MVVM模式,视图层和数据层的双向绑定,让我们无需再去关心DOM操作的事情,更多的精力放在数据和业务逻辑上去.

##### 低耦合:

视图6（View）可以独立于Model变化和修改，一个ViewModel可以绑定到不同的"View"上，当View变化的时候Model可以不变，当Model变化的时候View也可以不变。

##### 可重用性:

你可以把一些视图逻辑放在一个ViewModel里面，让很多view重用这段视图逻辑。

##### 独立开发:

开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计。

##### 可测试:

界面素来是比较难于测试的，而现在测试可以针对ViewModel来写

##### 易用灵活高效






### 数据绑定,指令,事件

#### 引入

``` bash
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
```

#### 实例

最基本实例,其中el是必须的,是一个选择器

``` bash
var app = new Vue({
    el:''
})
```

#### 数据绑定data

声明双向绑定的数据

#### 访问Vue实例的属性

``` bash

var app = new ({
    el:'',
    data:{
        msg:''
    },
    methods:{
        ///
    }
})

//访问el

app.$el

//访问methods

app.$methods

//访问data中的msg

app.msg

```

#### 生命周期钩子

created 实例创建完成后调用,还没挂载到el上. ---还没挂载

mounted el挂载到实例后. ---刚挂载

beforeDestroy 实例销毁之前.主要用于解绑

运用例子:

``` bash
<div id="app">
    {{date}}
</div>

<script>
    var app = new Vue({
        el: '#app',
        data: {
            date: new Date()
        },
        mounted:function(){//挂载成功后进行每秒刷新1次当前时间
            var _this = this;
            this.timer = setInterval(function(){
                _this.date = new Date();
            },1000)
        },
        beforeDestory:function(){//销毁前清除定时器
            if(this.timer){
                clearInterval(this.timer)
            }
        }
    })
</script>
```

####  文本插值和表达式

##### 文本插值:

使用{{表达式}},将data中的数据显示

##### 表达式:

只能是单个表达式,不能是语句

##### 运算

``` bash

{{6 + 6}}

```
##### 三元运算

``` bash
{{ 2>1 ? 'yes' : 'no'}}
```

##### JS:

``` bash
{{Date.now()}}
```

#### 过滤器

Vue尾部插入|,通常用于格式化文本,过滤规则是自定义的,通过给Vue实例添加filters来设置

``` bash
{{ data.数据名 | 过滤器1}}
```
##### 串联:

``` bash
{{ data.数据名 | 过滤器1 | 过滤器2}}
```

##### 过滤器的参数

``` bash
{{date.数据表 | 过滤器1(a,b)}}
```

传入的第一二个参数是过滤器1中的第二三个参数

``` bash
filters:{
    过滤器1:function(val,a,b){
        ///对val进行操作 val是  data.数据名 传入的
    }
}
```


#### 指令和事件

##### v-text

解析文本和作用一样

例:
``` bash
<p v-text="msg"></p>

<p>{{msg}}</p>
...
data{
    msg:'msg'
}

```

##### v-html

解析html

例:
``` bash
<div v-html="html"></div>

...
data{
    html:'<h1>hello</h1>'
}
```

##### v-bind:

动态更新HTML元素上的属性,语法糖v-bind  === :

例:
``` bash
<p v-bind:title="title"></p>

<p :title="title"></p>

<p :class="active"></p>
...
data{
    title:'title',
    class:'active'
}

```


#### v-on

语法:v-on:事件="方法"

其中方法挂载到vue实例用的methods属性内,并且是一个函数,函数内的this指向vue实例本身.
所以可以直接访问或修改data内的数据.
注意:不能用箭头函数,因为会改成this,也就是把this变成对象'methods'

简单例子:
``` bash
<div id="app">
    <button v-on:click="doSomething">点击我</button>
    <p>{{msg}}</p>
</div>

<script>
    var app = new Vue({
        el:'#app',
        data:{
            msg:'this is a msg in data'
        },
        methods:{
            doSomething:function(){
                alert('你点击我了!')
                alert(this.msg)
            }
        }
    })
</script>
```


