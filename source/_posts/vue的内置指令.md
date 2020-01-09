---
title: vue的内置指令
date: 2018-07-25 14:36:10
categories:
- vue
tags:
- vue
---

#### v-cloak 

与dispaly:none进行结合使用.

作用:解决初始化慢导致页面闪动.

例:
``` bash
<style>
    *[v-cloak]{
        display:none;
    }
<style>
<comp-a v-show="isShow" v-cloak></comp-a>

data{
    isShow:false
}
```

#### v-once

定义它的元素和组件只渲染一次

#### v-if,v-else-if,v-esle

例:
``` bash
<div id="app3">
    <div v-if="type === 'A'">A</div>
    <div v-else-if="type === 'B'">B</div>
    <div v-else-if="type === 'C'">C</div>
    <div v-else>Not A/B/C</div>
</div>
<script>
    var app3 = new Vue({
        el:'#app3',
        data:{
            type:'A'
        }
    })
</script>
```
弊端:Vue在渲染元素时,出于效率考虑,会尽可能地复用已有的元素而非重新渲染,因此会出现乌龙,只会渲染变化的云阿苏,也就是说input元素被复用了.
解决方法:加key,唯一,提供key值可以来决定是否复用该元素.

#### v-show

只改变了css属性display

v-if:实时渲染,显示就渲染,不显示就销毁.
v-show:元素永远存在于页面中,只是改变了css的display的属性.

#### v-for

遍历数组,每个项渲染到列表之中.
``` bash
  <ul id="example2">
      <li v-for="(item,index) in items">
          {{parentMessage}} - {{index}} - {{item.message}}
      </li>
  </ul>
  <script>
      var example2 = new Vue({
          el:'#example2',
          data:{
              parentMessage:'Parent',
              items:[
                  {message:'Foo'},
                  {message:'Bar'}
              ]
          }
      })
  </script>

  <ul id="example3">
      <li v-for="(value,key,index) in object">
        {{index}}. {{key}} : {{value}}
      </li>
  </ul>
  <script>
      var example3 = new Vue({
          el:'#example3',
          data:{
              object:{
                  firstName:'John',
                  lastName:'Doe',
                  age:30
              }
          }
      })
  </script>
```

##### 数组更新,过滤排序

改变数组的方法:

1. push()在末尾添加元素

2. pop()移除数组最后一个元素

3. shift()删除数组的第一个元素

4. unshift()在第一个元素之前添加一个元素

5. splice()添加或删除函数,返回删除的元素
    第一个参数:开始操作的位置.
    第二个参数:操作的长度.
    第三个可选参数:排序:sort(),reverse()

##### 两个数组变动vue检测不到:

1. 改变数组的指定项
2. 改变数组长度
    过滤:filter

解决方法:
1. set(改变指定项)
    Vue.set(app.arr,1,"car");

2. splice(改变长度)
    app.arr.splice(1)

#### 方法和事件

v-on

methods

##### 修饰符

在vue中传入event对象用$event,方式是冒泡.

stop:阻止单击事件向上冒泡.
prevent:提交事件并且不重载页面.
self:只作用在元素本身而非子元素的时候调用.
once:只执行一次方法.

可以监听键盘事件:
``` bash
<input @keyup.13="fn">----指定的keyCode
```

可以用.enter .tab .delete等

