---
title: 手写一个简易的Promise
date: 2023-02-08 23:39:13
categories: 
- JS
tags: 
- JS
---


```bash
class Promises2 {
    #status = 'pending'
    constructor(fn) {
        this.q = []//创建一个队列
        const resolve = (data) => {
            this.#status = 'fulfilled'
            const f1f2 = this.q.shift()//出列，返回第一个
            const x = f1f2[0].call(undefined, data)
            if (x instanceof Promise2) {
                x.then(data => {
                    resolve(data)
                }, (reason) => {
                    reject(reason)
                })
            } else {
                resolve(x)
            }
        };
        const reject = (reason) => {
            this.#status = 'rejected'
            const f1f2 = this.q.shift()
            const x = f1f2[1].call(undefined, data)
            if (x instanceof Promise2) {
                x.then(data => {
                    resolve(data)
                }, (reason) => {
                    reject(reason)
                })
            } else {
                resolve(x)
            }
        }
        fn.call(undefined, resolve, reject)
    }
    then(f1, f2) {
        this.q.push([f1, f2])//入列
    }
}
```
