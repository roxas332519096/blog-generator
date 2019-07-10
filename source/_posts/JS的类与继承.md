---
title: JS的类与继承
date: 2018-07-25 02:52:08
tags:
- ES6
---
#### 继承

继承的作用是:子类可以具有父类的属性和方法

JS没有继承,只有原型链引用

一个对象的__proto__指向构造他的函数的protype

``` bash
obj._proto_ = Object.prototype
```

如:
``` bash
var a = new Array();
a.push() //实例属性
a.valueOf() //继承Object
```

push是Array.protoype的属性;
valueOf是继承子Ojbect.prototype的;
因为
``` bash
Array.protoype.__proto__ = Object.protoype
```

隔了两层的才是继承,对于a;push是自身有的,valueOf才是继承的.

#### 类

能产生对象的东西即为类

自己写一个继承类

``` bash
function Human(name){
    this.name = name;
}
Human.prototype.run = function(){
    console.log('跑跑跑');
    return undefined;
}

function Man(name){
    Human.call(this,name); //使子类有父类的属性,假如不写this,那么this就是window
    this.gender = '男';
}

Man.prototype.__proto__ = Human.prototype //插入父类原型链,但是IE不支持

Man.prototype.fight = function(){
    console.log('打击');
    return undefined;
} 

var f = new Man('某个男人'); //假如不写new,那么this就是window,因为new的时候this会绑定到这个对象名为Man的对象上

输出:
f.name  //'某个男人'
f.gender //'男'
f.fight()  //'打击'
f.run() //'跑'

f.__proto__ === Man.prototype;//true
f.__proto__.proto__ === Human.prototype;//true
Man.prototype.__proto__ === Human.prototype;//true
```

##### 构造函数的prototype

prototype属性只有一个功能,存放共有属性对象的地址

##### ES5和ES6的写法

ES5:
``` bash
var f = function(){}
f.protype = Human.protype
Man.protype = new f()
```

为什么?

当var obj = new Fn()时,会做以下几件事

1. 产生一个空对象
2. this = 该空对象
3. this.__proto__ = Fn.protype
4. 执行Fn.call(this,x,y..)
5. return this

Man.prtotype = New Human();会执行this.name,使得有多余属性
因为第4步不想要,所以构造一个空函数,只要他的protype

空函数.protype = Human.protype;
Man.protype = new f() // 1,2,3,5步
f.protype === Human.protype //true
Man.protype.__proto__ === f.protype //true 

ES6:
constructor构造自有属性,共有属性写在constructor外面
``` bash
class Human{
    constructor(name){
        this.name = name
    }
    run(){
        console.log('run')
    }
}

class Man extends Human{//等价于Man.protype.__protype = Human.protype
    constructor(name){
        super(name) //等价于Human.call(this,name),super意为超类,即父类
        this.gender = 'Man'
    }
    fight(){
        console.log('fight')
    }
}

var author = new Man('roxas')
atuhor//{
    name:'roxas',
    gender:'Man'
    __proto__:{
        fight(){},
        ...
        __proto__:{
            run(){}
            ...
        }
    }
}
```