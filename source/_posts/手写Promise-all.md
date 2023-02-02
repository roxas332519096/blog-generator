---
title: 手写Promise.all
date: 2023-02-02 23:03:52
categories: 
- JS
tags: 
- JS
---

```bash
Prmise.myAll = function (list) {
    const results = []
    let count = 0
    return new Promise((resolve, reject) => {
        list.map((promise, index) => {
            promise, then((r) => {
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