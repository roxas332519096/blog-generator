---
title: render函数
date: 2018-07-25 16:42:28
categories: 
- vue
tags:
- vue
---

#### 初步了解

定义一个组件,使用template
``` bash
    <div id="app">
        <comp-child :level="level">
            我是组件
        </comp-child>
    </div>

    <script>
        Vue.component('comp-child',{
            props:['level'],
            template:`
            <div>
                <h1 v-if="level===1">
                    <slot></slot>
                </h1>
                <h2 v-if="level===2">
                    <slot></slot>
                </h2>
                <h3 v-if="level===3">
                    <slot></slot>
                </h3>
            </div>
            `
        })
        var app = new Vue({
            el:'#app',
            data:{
                level:1
            }
        })
    </script>
```

再定义一个组件,使用render函数,其效果和上面例子一样

``` bash
        Vue.component('comp-child',{
            props:['level'],
            render:function(createElement){
                return createElement('h'+this.level,this.$slots.default);
            }
        })
```

#### render函数的第一个参数(必须)

在render函数的方法中,参数必须是createElement,它是类型是function.

render函数的第一个参数可以是:

1. String
    html标签
    ``` bash
    Vue.component('child',{
        render:function(createElement){
            return createElement('div')
        }
    })
    ```
2. Object
    一个含有数据选项的对象
    ``` bash
    Vue.component('child',{
        render:function(createElement){
            return createElement({
                template:'<div></div>'
            })
        }
    })
    ```
3. Function
    方法返回含有数据选项的对象
    ``` bash
    Vue.component('child',{
        render:function(createElement){
            var domFn = function(){
                return {
                    template:'<div></div>'
                }
            }
            return createElement(domFn());
        }
    })
    ```

#### render函数的第二个参数

第二个参数是可选,第二个参数是数据对象(只能是Object)

1. class
2. style
3. attrs:正常的html属性
4. domProps:原生的DOM属性
``` bash
Vue.component('child-4', {
    render: function (createElement) {
        return createElement('div',{
            class:{
                active:true,
                danger:false
            },
            style:{
                color:'red',
                fontSize:'16px'
            },
            attrs:{
                id:'foo',
                src:'http://baidu.com'
            },
            domProps:{
                innerText:'Hello World!'
            }
        })
    }
})
```

#### render函数的第三个参数

第三个参数是可选的

1. String:创建文本子节点
2. Array:创建元素子节点(VNODE)

``` bash
Vue.component('child-5', {
    render: function (createElement) {
        return createElement('div',[ //:array创建元素节点
            createElement('span','Hello world!') //string:创建文本节点
        ])
    }
})
```

#### this.$slots(插槽)在render函数中的应用

第三个参数的数组存的是VNODE

``` bash
<child>
    <h3 slot="header">标题</h3>
    <p>第一段</p>
    <p>第二段</p>
    <h5 slot="footer">结尾</h5>
</child>

Vue.component('child', {
    render: function (createElement) {
        var header = this.$slots.header; //返回的内容就是含有VNODE的数组
        var main = this.$slots.default;
        var footer = this.$slots.footer;
        return createElement('div',[
            createElement('header',header),//返回的内容就是VNODE
            createElement('main',main),
            createElement('footer',footer)
        ])
    }
})
```

#### 在rander函数中使用props传递数据

在render函数中,props传递过来的数据,可以用this.绑定的数据直接在render函数中使用.

``` bash
<div id="app">
    <child :color="colorchange"></child>
    <button @click="clickMe">换色</button>
</div>

<script>
    Vue.component('child', {
        props:['color'],
        render: function (createElement) {
            var color
            if(this.color){
                color = 'red'
            }else{
                color = 'blue'
            }
            return createElement('div',{
                style:{
                    color:color
                }
            },'hello world!')
        }
    })

    var app6 = new Vue({
        el: '#app',
        data: {
            colorchange:false
        },
        methods:{
            clickMe:function(){
                this.colorchange = !this.colorchange
            }
        }
    })
</script>
```

#### v-model在render函数中的使用

``` bash
<div id="app">
    <comp v-model="name"></comp>
    {{name}}
</div>
<script>
    Vue.component('comp',{
        render:function(createElement){
            var _this = this;
            return createElement('input',{
                domProps:{
                    value:_this.name
                },
                on:{
                    input:function(e){
                        _this.$emit('input',e.target.value)
                    }
                }
            })
        }
    })

    var app = new Vue({
        el:'#app',
        data:{
            name:''
        }
    })
</script>
```

#### 作用域插槽在render函数中的使用



#### 函数化组件的应用



