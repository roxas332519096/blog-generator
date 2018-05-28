---
title: JS实现数组去重
date: 2018-05-27 20:38:43
tags:
---

#### ES5 :

``` bash
var  array = [1,5,2,3,4,2,3,1,3,4];
function unique(array){
    let arrayNew = [];
    for (let i = 0;i < array.length;i++){
        if(arrayNew.indexOf(array[i]) === -1){
            arrayNew.push(array[i]);
        }
    }
    return arrayNew;
}
unique(array);
```

indexOf,查询数组是否出现某个值,并返回到其index,假如没有则返回-1.


#### ES6:

使用Set对象,可实现原数组去重.
```bash
var array = [1,5,2,3,4,2,3,1,3,4];
function unique(arr){
  return Array.from(new Set(arr));
}
unique(array);
```
