---
title: DOM事件
date: 2018-05-29 15:23:37
categories:
- JS
tags:
- JS
---
### DOM level 0: 

onclick = "要执行的代码"  //一旦用户点击,浏览器就eval("要执行的代码")

例:
``` bash 
<script>
    function print(){console.log(''hi)}
</script>
<button id = X onclick = "print()">
```
``` bash
<script>
X.onclick = print  //类型为函数对象,对
Y.onclick = print() //undefined,错
</script>
```

### DOM level 1:同DOM level0;

### DOM level 2:
```bash
X.addEventListener('click',function(){}) //队列,先进先出,先绑定先触发
```
#### 与 X.onclick = function(){}区别:
这是一个属性,是唯一的,只能绑定一个onclick;
一次事件监听 X.one('click',fn(){}) //添加后移除事件

``` bash
X.removeddEventListener('click',function(){})
```
祖先元素绑定事件模型:
``` bash            
<div id="grand1">
    爷爷
    <div id="parent">
        爸爸
        <div id="child1">儿子</div>
    </div>
</div>
<script>
    grand1.addEventListener('click',function f1(){
        console.log('爷爷')
    })
    parent1.addEventListener('click',function f2(){
        console.log('父亲')
    })
    child1.addEventListener('click',function f3(){
        console.log('儿子')
    })
</script>
```
1.  当我点击儿子时,也相当于点击父亲和爷爷
2.  当我点击儿子时,也相执行其绑定事件,执行f1 f2 f3;
3.  X.addEventListener('click',function f1(){},参数)
    添加参数,默认是false
    假如是false:从小到大(冒泡) f3 f2 f1 ,假如是true:从大到小(捕获) f1 f2 f3

4.   假如同一个事件本身存在冒泡捕获,那么按照写的顺序执行
     X.addEventListener('click',function f1(){},false) //冒泡
     X.addEventListener('click',function f1(){},ture) //捕获
   

### 阻止祖先DOM事件触发

#### 点击其他地方关闭浮层

#### 方案1:
通过stopPropagation()方法阻止事件传播;
代码如下:

预览:
https://roxas332519096.github.io/notes-demo/0528-点击其他地方关闭浮层方案1.html


```bash
<script>
    clickMe.addEventListener('click',function(e){
        popover.style.display = 'block';
    })
    wrapper.addEventListener('click',function(e){
            e.stopPropagation();
    })
    document.addEventListener('click',function(e){
        popover.style.display = 'none';
    })
</script>
```

#### 方案2:
用jQuery的监听一次事件one()与setTimeout()

预览:
https://roxas332519096.github.io/notes-demo/0528-点击其他地方关闭浮层方案2.html

代码如下:

``` bash
<script>
    $(clickMe).on('click',function(){
        $(popover).show();
        setTimeout(function(){
            $(document).one('click',function(){
                $(popover).hide();
            })
        },0)
    })
</script>
```

#### 做一个Demo理解DOM事件:

预览:
https://roxas332519096.github.io/notes-demo/0528-理解DOM事件DEOM.html


过程:

第一次点击时,先事件监听最后的参数为true,所以传播方式为捕获,从父元素到子元素传播;
其后,事件监听最后的参数为默认值,false,所以传播方式为冒泡,从子元素到父元素上传播;

代码如下:

``` bash
<script>
    let divs = $('div').get()
    let n = 0
    for (let i = 0; i < divs.length; i++) {
    divs[i].addEventListener('click', () => {
        setTimeout(() => {
        divs[i].classList.add('active')
        }, n * 500)
        n += 1
    }, true)
    }


    for (let i = 0; i < divs.length; i++) {
    divs[i].addEventListener('click', () => {
        setTimeout(() => {
        divs[i].classList.remove('active')
        }, n * 500)
        n += 1
    })
    }
</script>
```
