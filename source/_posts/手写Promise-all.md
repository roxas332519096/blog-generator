---
title: 手写Promise.all
date: 2023-02-02 23:03:52
categories: 
- JS
tags: 
- JS
---
1. 知道Promise上写而不是在原型上写
2. 知道all的参数（Promise数组）和返回值（新Promise对象）
3. 知道用数组来记录结果
4. 知道只要一个reject就整体reject
   
```bash
Promise.myAll = function (list) {
    const results = []
    let count = 0
    return new Promise((resolve, reject) => {
        list.map((promise, index) => {
            promise.then((r) => {
                results[index] = r
                count += 1
                if (count === list.length) {
                    resolve(results)
                }
            },
                (reason) => {
                    reject(reason)
                }
            )
        })
    })
}
```