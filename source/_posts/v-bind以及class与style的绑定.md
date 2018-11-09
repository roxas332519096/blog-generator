---
title: v-bind以及class与style的绑定
date: 2018-07-25 13:42:41
tags:
---

#### 了解bind指令

作用:绑定vue实例里的data或者computed属性

1. 变量语法

``` bash
:title="message"

data:{
    message:'abc'
}

title="abc"
```

2. 对象语法

``` bash
:title="msgObj"

data:{
    msgOjb:{
        msg1:true,
        msg2:false
    }
}

title="msg1"
```

3. 数组语法
``` bash
:title=[msg1,msg2]

data:{
    msg1:1,
    msg2:2
}

title="msg1=1 msg2=2"
```

#### 绑定class的几种方式

##### 对象语法

1. 用表达式
``` bash
:class="{'active':isActive,'danger':isDanger}"

data:{
    isActive:true,
    isDanger:false
}
```
2. 1. 对象变量名

    ``` bash
    :class="classObject"

    data:{
        classObject:{
            active:true,
            danger:false
        }
    }
    ```
   2. 对象变量名+计算属性
   ``` bash
   :class="classObject"

   data:{
       isActive:true,
       error:null
   },
   computed:{
       classObject:function(){
           return {
               active:this.active && !this.error,
               danger:this.error && this.error.type === 'fatal'
           }
       }
   }
   ```

##### 数组语法

``` bash
:class="[activeClass,errorClass]"

data:{
    activeClass:'active',
    errorClass:'text-danger'
}
```

#### 绑定style的几种方式

1. 表达式

``` bash
:style="{color:activeColor,fontSize:fontSize + 'px'}"

data:{
    activeColor:'red',
    fontSize:30
}
```

2. 对象变量名

``` bash
:style="styleObject"

data:{
    styleObject:{
        color:red,
        fontSize:30px
    }
}
```

3. 数组

``` bash
:style="[styleObject1,styleObject2]"

data:{
    styleObject1:{
        color:'red',
        background:'blue'
    }
    styleObject2:{
        fontSize:'30px',
        fontWeight:'bold'
    }
}
```