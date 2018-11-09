---
title: v-model的使用
date: 2018-07-25 15:14:20
tags:
---

#### v-model:

vue提供了v-model指令,用于在表单类元素上双向绑定.

#### input和textarea

可以用于input框以及textarea等.

注意:所显示的值只依赖于所绑定的数据,不再关系初始化时插入的value.

#### 单选按钮

1. 单个单选按钮,直接用v-bind绑定一个布尔值,用v-model是不可以的.
2. 如果组合使用,就需要v-model来配合value使用,绑定所选中你的单选框的value值,此处所绑定初始值可以随意给

``` bash
<div id="app5">
    <input type="radio" id="one" value="One" v-model="picked">
    <label for="one">One</label>
    <input type="radio" id="two" value="Two" v-model="picked">
    <label for="two">Two</label>
    <br>
    <span>{{picked}}</span>        
</div>
<script>
    var app5 = new Vue({
        el:'#app5',
        data:{
            picked:''
        }
    })
    </script>
```

#### 复选框

1. 单个复选框,直接用一个布尔值,可以用v-model,也可以用v-bind.
2. 多个复选框,如果是组合使用,就需要v-model来配合value使用,v-model绑定一个数组,如果绑定是字符串,则会转化为true.与所有绑定的复选框的checked属性相对应.

``` bash
    <div id="app3">
        <input type="checkbox" name="" id="checkbox" v-model="checked">
        <label for="checkbox">{{checked}}</label>
    </div>
    <script>
        var app3 = new Vue({
            el:'#app3',
            data:{
                checked:false
            }
        })
    </script>

    <div id="app4">
        <input type="checkbox"  id="jack" value="Jack" v-model="checkedNames">
        <label for="jack">Jack</label>
        <input type="checkbox"  id="john" value="John" v-model="checkedNames">
        <label for="john">John</label>
        <input type="checkbox"  id="mike" value="Mike" v-model="checkedNames">
        <label for="mike">Mike</label>
        <br>
        <span>{{checkedNames}}</span>
    </div>
    <script>
        var app4 = new Vue({
            el:'#app4',
            data:{
                checkedNames:[]
            }
        })
    </script>
```

#### 下拉框

1. 如果是单选,所绑定的value值初始化可以为数组,也可以为字符串,有value直接有限匹配一个value值,没有value就匹配一个text值.
2. 如果是多选,就需要v-model来配合value使用,v-model绑定一个数组,与复选框类似.
3. v-model一定是绑定在select标签上.

``` bash
<div id="app6">
    <select v-model="selected">
        <option disabled value="">请选择</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
    </select>
    <span>{{selected}}</span>
</div>
<script>
    var app6 = new Vue({
        el:'#app6',
        data:{
            selected:''
        }
    })
</script>
```

#### 绑定值

1. 单选按钮,只需要v-bind给单选框绑定一个value值,此时,v-model绑定的就是他的value值.
2. 复选框
3. 下拉框,在select标签上绑定value值对option并没有影响.


#### 修饰符

1. lazy v-model默认是在input输入时实时同步输入框的数据,而lazy修饰符,可以使其爱失去焦点或敲回车后更新.
2. number 将输入的字符串转化为number类型.
3. trim 自动过滤输入过程中首尾的空格.
