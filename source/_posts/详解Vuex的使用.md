---
title: 详解Vuex的使用
date: 2019-02-16 17:22:28
categories:
- vue
tags:
- vue
---

#### Vuex的引入

``` bash
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
```

#### vuex的格式

``` bash
new Vuex.Store({
    state: {
        //数据
    },
    getters:{
        //可理解为state的计算属性,同计算属性一样会被缓存,刷新才重新计算
    }
    mutations: {
        //修改state的同步方法
    },
    actions: {
        //异步方法,需要调用mutations修改state
    }
})
```

#### state的使用

由于state是响应式的,所以在组件中使用state时,最简单的方法是用计算属性

``` bash
//vuex
{
    state:{
        list:[1,2,3]
    }
}

//compoment

computed:{
    list(){
        return this.$store.state.list
    }
}

```

#### getters的使用

可理解为state的计算属性,同计算属性一样会被缓存,刷新才重新计算
应用场景:当多个组件属性用到这个属性的时候,可以简化代码

#### 通过属性访问

可以以属性的形式访问这些值
``` bash

//vuex
{
    state:{
        list:[1,2,3]
    },
    getters:{
        count:state=>{
            return state.list.map((item)=>{
                item++
            })
        }
    }
}

//component

computed:{
    count(){
        return this.$store.getters.count
    }
}
```

##### 通过方法访问

可以通过让getter返回一个函数,来实现给getter传参,在对store数组进行查询时非常有用.
注意,getter通过方法访问时,每次都会进行调用,不会缓存.

``` bash

//vuex
getter:{
    getNumber:(state)=>{
        (id)=>{
            return state.list.find((item)=>{
                item === id
            })
        }
    }
}

//compoment

this.$store.getters.getNumber(1)
```

##### mapGetters辅助函数

mapGetters辅助函数仅仅是将store中的getter映射到局部计算属性

``` bash
import {mapGetters} from 'vuex'

computed:{
    //使用对象展开运算符将getter混入原computed对象中
    ...mapGetters([
        'list1',
        'list2',
        'list3',
        //...
    ])
}
```

如想讲getter属性另取名字,使用对象形式

``` bash
mapGetters({
    //把this.newListname映射为this.$store.getters.list1
    newListname:'list1'
})
```

#### Mutation

Mutation是vuex更改state的唯一方法,并且必须是同步的.
每个mutation都有一个事件类型(type)和回调函数(hander),并且以state作为第一个参数

调用只能通过state.commit('type')
``` bash

//vuex
state:{
    count:1
},
mutations:{
    increment(state){
        state.count++
    }
}

//compoment

store.commit('increment')
```

##### 提交载荷(payload)

store.commit传入额外参数,即mutation的载荷(payload)

``` bash
//vuex

mutations:{
    increment(state,n){
        state.count += n
    }
}

//component
store.commit('increment',10)
```

##### mapMutations

同mapGetters

```
//vuex

mutations:{
    increment(state){
        state.count++
    }
}

//compoment

improt {mapMutations} from 'vuex'

methods:{
    ..mapMutations(['increment'])
    //或
    //...mapMutations({
        add:'increment'
    })
}
```

#### Action

vuex需要异步操作时,需要用action,用action调用mutation的方法更改state

``` bash
//vuex

state:{
    count:0
},
mutations:{
    increment(state){
        state.count++
    }
}.
actions:{
    add(context){
        setTimeout(()=>{
            context.commit('increment')
        },1000)
    }
}

//compoment
store.dispatch('add')
```

##### 参数context

action的第一个参数context相当于上下文,可以通过context.state和context.getters获取state与getters
可以用ES6的赋值解构进行简写.

```bash
actions:{
    add({commit}){
        setTimeout(()=>{
            commit('increment')
        },1000)
    }
}
```

##### mapActions

方法同mapMutations