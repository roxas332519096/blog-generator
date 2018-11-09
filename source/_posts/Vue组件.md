---
title: Vue组件
date: 2018-07-13 23:05:25
tags:
---
### vue组件

#### 为什么要使用组件

提高代码的复用性

#### 组件注册

##### 全局注册

优点:都可以使用

缺点:权限太大,容错率降低

```
Vue.component('my-component',{
    template:'<div>...<div>'
})
```

#### 局部注册

``` bash
//实例内包含组件A

var componentA = {
    template:'<div>A</div>'
}

new Vue({
    el:'',
    components:{
        'component-a':componentA
    }
})

//局部组件B内使用局部组件A

var componentB = {
    template:'<div>A</div>',
    components:{
        'compontent-a':componentA
    }
}

```

#### 标签受限下使用组件

table 直接使用会踢出去,因为table只能用tr td tbody 等元素

要使用is属性,把原标签替换成组件

```
//不能正常运行
<table>
    <component-a>/<component-a>
</table>

//使用is属性替换

<table>
    <tbody is="component-a"></tobdy>
</table>

```

#### 组件注意事项

1. 组件名称使用小写字母加-进行命名 如my-component

2. template内只能有一个根元素

3. 组件除了template还可以有data,computed,methods

4. 组件的data必须是一个方法,返回一个对象,因为对象的内存地址不一样

    例
    ```
    template:'<p>{{count}}<p>'
    data:function(){
        return {
            count:0
        }
    }
    ```

#### props

1. 使用props接收从父组件传递的参数,props中定义的属性都可以直接在组件中的使用

``` bash
<div id="app">
    <child-component msg="父组件传递过来的内容"></child-component>
</div>

<script>
    var app = new Vue({
        el:'#app',
        components:{
            'child-component':{
                props:['msg'],
                template:'<p>{{msg}}<p>'
            }
        }
    })
</script>
```

2.props来自父级,而组件中data return的数据是组件自己的数据,两种情况作用域就是组件本身,可以在template,computed,methods中直接使用

``` bash
components:{
    'child-component':{
        props:['msg'],
        data:function(){
            return {
                count:0
            }
        },
        methods:{
            method1:function(){
                return this.count
            }
        },
        computed:{
            computed1:function(){
                return this.count
            }
        },
        template:'<p>{{msg}} {{count}} {{method1()}} {{computed1}}<p>'
    }
}
```

3. props的值是字符串数组与对象

4. 可以v-bind拿到来自父组件的动态数据

``` bash
<div id="app">
    <child-component msg="父组件传递过来的内容"></child-component>
    <child-component v-bind:msg="msg"></child-component>
</div>

<script>
    var app = new Vue({
        el: '#app',
        data:{
            msg:'父组件data中传递过来的内容'
        },
        components: {
            'child-component': {
                props: ['msg'],
                template: '<p>{{msg}}<p>'
            }
        }
    })
</script>
```

v:bind传递一个数组与直接传递一个数组的区别

``` bash
<component arr="[0,1,2]"></component> //输出7,解析成字符串,长度为7

<component :arr="[0,1,2]"></component> //输出3,解析成数组,长度为3

....
props:['arr'],
template:'<p>arr.length</p>'
```

#### 单向数据流

##### 解析:

通过props传递数据是单向的,父组件数据变化会传递给子组件,反过来不行.

##### 目的:

将父子租借解耦,避免子组件无意中修改了父组件的状态

##### 应用场景:

##### 场景1

父组件传递初始值,子组件将它作为初始值保存起来,在自己的作用域下随意使用和修改,这样情况可以在组件data内再声明一个数据,引用父组件的prop

步骤1: 注册组件
步骤2: 将父组件的数据传递尽力啊,并在子组件中用props接受
步骤3: 将传递进来的数据通过初始值保存起来

``` bash
 <div id="app">
     <my-comp v-bind:msg="msg"></my-comp>
 </div>
 <script>
     var app = new Vue({
         el:'#app',
         data:{
             msg:1
         },
         components:{
             'my-comp':{
                 props:['msg'],
                 template:'<p>{{childMsg}}</p>',
                 data:function(){
                     return {
                        childMsg : this.msg
                     }
                 }
             }
         }
     })
 </script>
```

##### 场景2

prop作为需要被转变的原始值传入.这种情况用计算属性

步骤1:注册组件
步骤2:父组件传递数据,子组件props接收
步骤3:传递过来的数据通过计算属性进行重新计算

``` bash
<div id="app">
    <input type="text" v-model="width">
    <my-comp v-bind:width="width"></my-comp>
</div>
<script>
    var app = new Vue({
        el:'#app',
        data:{
            width:0
        },
        components:{
            'my-comp':{
                props:['width'],
                template:'<div :style="style"><div>',
                computed:{
                    style:function(){
                        return {
                            width:this.width + 'px',
                            background:'red',
                            height:'30px'
                        }
                    }
                }
            }
        }
    })
</script>
```

#### 数据验证

可以验证tpye类型可以是
Stiring
Number
Boolean
Object
Array
Function


``` bash
<script>
    var app = new Vue({
        el:'#app',
        components:{
            'my-comp':{
                template:'<div"><div>',
                props:{
                    propA:Number,//数字
                    propB:[String,Number],//字符串或数字
                    propC:{
                        type:Boolean,
                        default:true//当不传入时的默认值
                    },
                    propD:{
                        type:Number,
                        required:true//必须传入
                    },
                    propE:{
                        type:Array,
                        default:function(){//当数组时默认值必须是一个函数并返回一个数组
                            return []
                        }
                    },
                    propF:{
                        validator:function(val){//条件判断
                            return val > 10;
                        }
                    }
                }
            }
        }
    })
</script>
```

#### 组件通信

#### 自定义事件

子组件给父组件传递数据

子组件用$emit()发布事件,父组件用v-on监听子组件的事件

步骤1:自定义事件
步骤2:在子组件用$emit发布事件,第一个参数是事件名,后面参数是传递的数据
步骤3:在自定义事件用一个参数来接受

例:
``` bash
<div id="app">
    <p>库存:{{total}}</p>
    <btn-comp 
        @change="handleTotal"></btn-comp>
</div>
<script>
        var app = new Vue({
            el: '#app',
            data: {
                total: 0
            },
            components: {
                'btn-comp': {
                    template: `
                    <div>
                        <button @click="plusOne">+1</button>
                        <button @click="minOne">-1</button>
                    </div>
                    `
                    ,
                    data: function () {
                        return {
                            count: 0
                        }
                    },
                    methods: {
                        plusOne: function () {
                            this.count++;
                            this.$emit('change', this.count)
                        },
                        minOne: function () {
                            this.count--;
                            this.$emit('change', this.count)
                        }
                    }
                }
            },
            methods:{
                handleTotal:function(val){
                    this.total = val
                }
            }
        })
</script>
```

#### 在组件用使用v-model

$emit发布一个input事件,参数是传递给v-model绑定属性的值

##### v-model是一个语法糖,背后做了两步操作:
1. v-bind绑定
2. v-on给当前元素绑定input事件

v-model其实就是绑定input事件,当触发input时,input事件就会自动接收传递过来的参数,并赋值给v-model绑定的属性

##### 要使用v-model要做到
1. 接收一个value属性
2. 在新的value时触发input事件

例
``` bash
<div id="app">
    <p>库存:{{total}}</p>
    <btn-comp v-model="total"></btn-comp>
</div>
<script>
        var app = new Vue({
            el: '#app',
            data: {
                total: 0
            },
            components: {
                'btn-comp': {
                    template: `
                    <div>
                        <button @click="plusOne">+1</button>
                        <button @click="minOne">+1</button>
                    </div>
                    `
                    ,
                    data: function () {
                        return {
                            count: 0
                        }
                    },
                    methods: {
                        plusOne: function () {
                            this.count++;
                            this.$emit('input', this.count)
                        },
                        minOne: function () {
                            this.count--;
                            this.$emit('input', this.count)
                        }
                    }
                }
            }
        })
</script>
```

#### 非父组件之间的通信

##### 子组件间通信

父组件data中定义
bus:new Vue()
通过this.$root.bus这条链,子组件A emit一个事件并发送数据,子组件B在created的时候订阅事件,并接收数据

``` bash
<div id="app">
    <my-comp-a></my-comp-a>
    <my-comp-b></my-comp-b>
</div>
<script>
    var app = new Vue({
        el:'#app',
        data:{
            bus:new Vue()
        },
        components:{
            'my-comp-a':{
                template:'<button @click="putDatatoB">点击向b组件传递数据</button>',
                data:function(){
                    return{
                        aaa:'A内容'
                    }
                },
                methods:{
                    putDatatoB:function(){
                        this.$root.bus.$emit('atob',this.aaa)
                    }
                }
            },
            'my-comp-b':{
                template:'<div></div>',
                created:function(){
                    this.$root.bus.$on('atob',function(val){
                        alert(val)
                    })
                }
            }
        }
    })
</script>
```

##### 任意组件的通信

``` bash
let eventHub = new Vue();
Vue.prototype.$eventHub = eventHub;
Vue.component('comp-a',{
    template:`
    <div><button @click="aTob">A</button></div>
    `,
    methods:{
        aTo:function(){
            this.$evntHub.$emit('atob','form a');
        }
    }
})
Vue.component('comp-b',{
    tempalte:'
    <div><span>B<span><span ref='formA'></span><div>
    ',
    created:function(){
        this.$eventHub.$on('atob',(data)=>{
            this.$refs.formA.textContent = data;
        })
    }
})
```

##### 父组件获得子组件数据

父链this.$parent
子链this.$refs
提供了为子链提供索引的方法,用特殊的属性ref为其增加一个索引

``` bash
<div id="app2">
        {{msg}}
        <child-comp ref="a"></child-comp>
        <button @click="getChildData">点我拿到B组件数据</button>
        {{formChild}}
</div>
<script>
    var app2 = new Vue({
        el:'#app2',
        data:{
            bus:new Vue(),
            msg:'数据还没修改',
            formChild:'还未拿到'
        },
        methods:{
            getChildData:function(){
                this.formChild = this.$refs.a.msg //从子组件拿数据
            }
        },
        components:{
            'child-comp':{
                template:'<button @click="setFatherData">点我修改父组件数据</button>',
                methods:{
                    setFatherData:function(){
                        this.$parent.msg = '数据已修改了' //修改父组件数据
                    }
                },
                data:function(){
                    return{
                        msg:'我是子组件数据'
                    }
                }
            }
        }
    })
</script>
```

#### 插槽

为了让组件可以组合,我们需要一种方式来混合父组件的内容与子组件自己的模板,这个过程被称为内容分发.
Vue实现了一个内容分发api,使用特殊的slot元素作为原始内容的插槽.

父组件的内容在父组件作用域内编译,
子组件的内容在子组件作用域内编译

例:
``` bash
<comp v-show="childshow"></comp>//这里的childshow是父组件data里的

data:{
    childshow:fasle
},
component:{
    'comp':{
        template:'<div v-show="childshow"></div>' //这里的childshow是子组件data例的
    },
    data:function(){
        return {
            childshow:false
        }
    }
}


```

##### 插槽用法:

父组件的内容与子组件相混合,从而弥补了试图的不足

混合父组件的内容与子组件自己的模板

##### 单个插槽:

``` bash
<div id="app">
    <my-comp>
        <p>父组件内容</p>
    </my-comp>
</div>
<script>
    var app = new Vue({
        el:'#app',
        data:{
            
        },
        components:{
            'my-comp':{
                template:`
                <div>
                    <slot>假如父组件没有内容,我就默认出现</slot>
                <div>`,
            }
        }
    })
</script>
```

##### 具名插槽:

下面的<p solot="heaer">与<slot  name="header">替换
变成 <h1><p></p></h1>

``` bash
<div id="app">
    <my-comp>
        <p slot="header">标题</p>
        <p>内容</p>
        <p slot="footer">底部</p>
    </my-comp>
</div>
<script>
    var app = new Vue({
        el:'#app',
        data:{
            
        },
        components:{
            'my-comp':{
                template:`
                <div>
                    <h1>
                        <slot name="header"></slot>
                    </h1>
                    <div>
                        <slot><slot>
                    </div>
                    <footer>
                        <slot name="footer"><slot>
                    <footer>
                <div>`,
            }
        }
    })
</script>
```

##### 作用域插槽

作用域插槽是一种特殊的slot,使用一个可以复用的模板来替换已经渲染的元素---从子组件获取数据

slot-scope的属性值指向插槽中的属性值,2.5.0版本下要使用template元素包裹

例:

``` bash
<div id="app3">
    <my-comp-abc>
        <p slot="abc" slot-scope="props">
            {{props.a}} ---
            {{props.b}}
        </p>
    </my-comp-abc>
</div>
<script >
    var app3 = new Vue({
        el:'#app3',
        components:{
            'my-comp-abc':{
                template:`
                <div>
                    <slot a="子组件a属性内容" b="子组件b属性内容" name="abc"></slot>
                </div>
                `
            }
        }
    })
</script>
```

#### 访问slot

通过this.$slots.name

``` bash
mounted:function(){
    let header = this.$slots.header;
    let text = header[0].elm.innerText;
    let html = header[0].elm.innerHTML;
}
```

#### 动态组件

Vue提供一个元素教component
作用是:用来动态挂载不同的组件
实现:使用is属性来进行实现

v-bind:is="组件名",可以把compoent变成该组件名的组件

通过动态组件切换视图的小demo:
``` bash
<div id="app">
    <components :is="view"></components>
    <button @click="handview('a')">A</button>
    <button @click="handview('b')">B</button>
    <button @click="handview('c')">C</button>
    <button @click="handview('d')">D</button>
</div>
<script>
    var app = new Vue({
        el:'#app',
        data:{
            view:'comp-a'
        },
        components:{
            'comp-a':{
                template:'<div>A<div>',
            },
            'comp-b':{
                template:'<div>B<div>',
            },
            'comp-c':{
                template:'<div>C<div>',
            },
            'comp-d':{
                template:'<div>D<div>',
            },
        },
        methods:{
            handview:function(tag){
                this.view = 'comp-' + tag
            }
        }
    })
</script>
```