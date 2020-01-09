---
title: vue-router与vuex
date: 2018-07-25 16:43:09
categories:
- vue
tags:
- vue
---
#### 前端路由

##### 路由

路由,根据一个指定的路径,返回一个指定的页面.

##### 前端路由

只由前端实现的路由称为前端路由.

##### 用jQuery实现前端路由

例子1:
1. HTML上写上class.
2. 监听点击事件,获取其index,改变index切换事件,并保存到location.hash;
3. 新进入页面时,获取location.hash,切换class

``` bash
<ul class="title">
    <li class="active">1</li>
    <li>2</li>
</ul>
<ol class="context">
    <li class="active">第一项</li>
    <li>第二项</li>
</ol>

//监听点击事件,获取其index,改变index切换事件,并保存到location.hash

$('.title').on('click','li',(e)=>{
    let $li = $(e.currentTarget);
    $li.addClass('active').siblings().removeClass();
    let index = $li.index();
    $('.context >li').eq(index).addClass('active').siblings().removeClass();
    location.hash = index;
})
//新进入页面时,获取location.hash,切换class
let index = location.hash.substring(1) || '#0'
$('.title > li').eq(index).addClass('active').siblings().removeClass();
$('.context > li').eq(index).addClass('active').siblings().removeClass();
```

可以改进成:
1. HTML写上a标签与class.通过点击a的锚点改变url.
2. 每次点击a标签改变hash,监听hash的改变切换tab.

``` bash
<ul class="title">
    <li class="active"><a href="#0">1</a></li>
    <li><a href="#1">2</a></li>
</ul>
<ol class="context">
    <li class="active">第一项</li>
    <li>第二项</li>
</ol>

selectedTab();//读取hash,改变class

window.onhashchange = (e) => {//每次点击a标签改变hash,监听hash的改变切换tab
    selectedTab();
}

function selectedTab() {
    let index = location.hash.substring(1) || '#0'
    $('.title > li').eq(index).addClass('active').siblings().removeClass();
    $('.context > li').eq(index).addClass('active').siblings().removeClass();
}
```

但是假如有其他锚点,会影响到index的获取.

使用history.pushState()实现路由.

1. 点击a标签(禁止默认事件跳转),获取其href,通过pushState改变pathname,读取pathname,改变hash.
2. 读取pathname,改变class.

``` bash
<ul class="title">
    <li class="active"><a href="/tab1">1</a></li>
    <li><a href="/tab2">2</a></li>
</ul>
<ol class="context">
    <li class="active">第一项</li>
    <li>第二项</li>
</ol>

$('.title > li').on('click','a',(e)=>{//点击a标签(禁止默认事件跳转),获取其href,通过pushState改变pathname,读取pathname,改变hash
    e.preventDefault();
    let a = e.currentTarget;
    let path = a.getAttribute('href');
    window.history.pushState(null,null,'/test3.html' + path)
    selectedTab()
})

function selectedTab() {//读取pathname,改变class
    let path = location.pathname || '/test3.html/tab1';
    let index = path.substring(path.length-1);
    $('.title > li').eq(index - 1).addClass('active').siblings().removeClass();
    $('.context > li').eq(index - 1).addClass('active').siblings().removeClass();
}
```

#### vue-router

简单例子:

1. HTML中,使用router-link组件来导航,通过传入to属性指定链接,它默认会被渲染成a标签
2. 路由匹配组件渲染放在router-view组件中
3. 定义组件,也可以从其他文件中improt进来.
4. 定义路由routes,通过路由映射组件.
5. 创建router实例,传递routes.
6. 在Vue实例中挂载router.

该例子是hash模式(改变url锚点)
``` bash
    <div id="app">
        // HTML中,使用router-link组件来导航,通过传入to属性指定链接,它默认会被渲染成a标签
        <router-link to="/tab1">To tab1</router-link>
        <router-link to="/tab2">To tab2</router-link>

        // 路由匹配组件渲染放在router-view组件中
        <router-view></router-view>
    </div>

    <script src="https://unpkg.com/vue/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>

    <script>
        //定义组件,也可以从其他文件中improt进来.
        //因为没有improt,所以使用命名空间
        window.tab1 = {
            template: `<div>{{msg}}</div>`,
            data(){
                return {
                    msg:'tab1'
                }
            }
        }

        window.tab2 = {
            template: `<div>{{msg}}</div>`,
            data(){
                return{
                    msg:'tab2'
                }
            }
        }

        Vue.component('tab1',window.tab1);
        Vue.component('tab2',window.tab2);

        //创建router实例
        let router = new VueRouter({
            routes: [
                { path: '/tab1', component: tab1 },
                { path: '/tab2', component: tab2 }
            ]
        })

        //在Vue实例中挂载router.
        let app = new Vue({
            el: '#app',
            router: router
        })
    </script>
```

##### 在vue-cli使用vue-router

进入根目录

``` bash
npm install --save vue-router
``

在入口文件main.js里引用vue-router

``` bash
improt router form 'vue-router'
improt 组件名 form '组件地址'
Vue.use(router)
```

在入口文件main.js中的vue实例中注入

``` bash
var myrouter = new router({
    routes:[{
        path:'/路径',//指定跳转路径
        component:组件名//指定要跳转的组件
    }]
})

new Vue({
    el:'#app',
    component:{App},
    template:'<App/>'
    router:myrouter
})

<router-link to="/路径"></router-link>
```



##### vue-router路由参数传递

在路由内假如路由的name,在path后面加:/:+传递的参数
``` bash
//
routes:[
    {
        name:'路由名'
        path:'/路径/:参数名',
        component:组件名
    }
]
```

传递参数,在使用router-link的组件中使用
``` bash
//组件中

<router-link :to="{name:'路由名',params:{参数名:参数内容}}">   
</router-link>
```

读取参数:$route.params.参数名
``` bash
//路由到的组件中
<p>$route.params.参数名<p>
```

#### vuex

用来状态管理,共享数据,在各个组件之间管理的外部状态.

##### 安装
``` bash
npm install vuex
```

##### 使用vuex

1. 引入vuex,通过use使用它.
2. 创建Vuex.Store实例
3. 组件都可以通过this.$store.state.key拿到数据

``` bash
improt Vuex from 'vuex'

Vue.use(Vuex)

var store = new Vuex.Store({
    state:{
        key:value
    }
})

new Vue({
    el:'#app',
    router,
    state,
    components:{App}
})

////某个组件中

this.$store.state.key 可以直接使用
```

##### 组件中改变state-mutation

mutation只能进行同步操作

1. 在vuex实例中定义mutations属性
2. muations里定义方法,并传入state
3. 组件中使用this.$store.commit('方法')去改变state
4. 注意commit传入的是字符串

``` bash
var store = new Vuex.Store({
    state:{
        num:0
    },
    mutations:{
        add(state){
            this.state.num += 1;
        }
    }
})

////子组件中
this.$store.commit('add')
<button @click="$store.commit('add')">add</button>
```

##### 组件中改变state-actions

actions可以进行异步操作(也可以同步)
它不能直接操作state,只能通过commit mutation中的方法.

1. vuex实例中加入actions属性
2. acitons属性中定义方法,方法传入参数context表示上下文对象
3. 通过context.commit('mutations中的方法')
4. 组件中通过$this.stote.dispatch('方法')使用

``` bash
var store = new Vuex.store({
    state:{
        num:0
    },
    mutations:{
        add(state){
            state.num += 1;
        }
    },
    actions:{
        add(context){ //同步
            context.commit('add');
        },
        addAfter(context){ //异步
            setTimeout(()=>{
                context.commit('add');
            },1000)
        }
    }
})

///子组件中

this.$store.dispatch('add')

<button @click="$store.dispatch('add')">添加</button>
```

##### vuex状态管理流程

view -> actions -> mutations -> state -> view
------------------------^
其中actions可以忽略

##### getters选项,获取并计算state中的状态

一般组件都是用getters来获取状态的,而不是用state

1. vuex实例中定义getters属性
2. getters属性定义方法,传入参数state
3. 方法操作state
4. 组件通过this.$store.getters.方法 获取数据

``` bash
var store = new Vuex.Store({
    state:{
        num:1
    },
    getters:{
        getNum(state){
            return state.num + '元'
        }
    }
})

//子组件中
this.$store.getters.getNum
```

