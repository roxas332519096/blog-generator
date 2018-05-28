---
title: 自制一个简单的jQuery库
date: 2018-05-24 10:47:25
tags:
---
#### 自制一个简单的jQuery库

#### 1.先创建一个选择器函数

``` bash
function(nodeOrSelector){
    let nodes = {}
    if(typeof nodeOrSelector === 'string'){
        let temp=document.querySelectorAll(nodeOrSelector);
        for (let i = 0;i < temp.length;i++){
            nodes[i] = temp[i];
        }
        nodes.length = temp.length
    } else if (nodeOrSelector instanceof Node) {
        nodes = {
            0: nodeOrSelector,
            length: 1
        }
    }
}
```
传入参数
1. 假如参数为string类型,则为一个选择器,那么用dom的api:querySelecotrAll生成伪数组NodeList;
2. 假如参数为Node节点,那么建立伪数组,key 0 的值为参数本身,length=1.与上面保持一致.

#### 2.设置API:addClass

``` bash
return {
        addClass : function(classes) {
            if(typeof classes === 'string'){
              for (let i = 0; i < nodes.length;i++){
                        nodes[i].classList.add(classes)
                    }
            }else if(typeof classes === 'object'){
                classes.forEach(
                    (value) => {
                        for (let i = 0; i < nodes.length;i++){
                            nodes[i].classList.add(value)
                        }
                    }
                )
            }        
        }
}
```
建立选择器后,就可以操作nodes了,通过对函数return一个对象,可以设置方法.
对象的第一个key是addClass,值为一个函数,传入classes参数;
1. 假如classes的类型为stirng,那么classes是单个class.那么遍历nodes,调用DOM API的classList.add();
2. 假如classes的类型是一个数组,那么classes可能是多个class,这是要先遍历classes,对每一项的值遍历nodes,调用classList.add();

#### 3.设置API:setText
对象的第二个key是setText,值为一个函数,传入text参数;
1. 遍历nodes,调用Dom Api的textContent = text;

``` bash
setText : function(text){
            for (let i = 0; i < nodes.length;i++){
                nodes[i].textContent = text;
            }
        }
```

#### 4.完整代码

``` bash
window.jQuery = function(nodeOrSelector){
    let nodes = {}
    if(typeof nodeOrSelector === 'string'){
        let temp=document.querySelectorAll(nodeOrSelector);
        for (let i = 0;i < temp.length;i++){
            nodes[i] = temp[i];
        }
        nodes.length = temp.length
    } else if (nodeOrSelector instanceof Node) {
        nodes = {
            0: nodeOrSelector,
            length: 1
        }
    }
    return {
        addClass : function(classes) {
            if(typeof classes === 'string'){
              for (let i = 0; i < nodes.length;i++){
                        nodes[i].classList.add(classes)
                    }
            }else if(typeof classes === 'object'){
                classes.forEach(
                    (value) => {
                        for (let i = 0; i < nodes.length;i++){
                            nodes[i].classList.add(value)
                        }
                    }
                )
            }        
        },
        setText : function(text){
            for (let i = 0; i < nodes.length;i++){
                nodes[i].textContent = text;
            }
        }
    }
}  
```

#### 5.运行代码
``` bash
window.$ = jQuery;
var $div = $('div')
$div.addClass('blue');
$div.setText('Hi');
```