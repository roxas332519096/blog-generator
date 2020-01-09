---
title: Axios
date: 2018-07-26 20:21:20
categories:
  - vue
tags:
  - vue
---

#### Axios 的好处

从浏览器中创建 XMLHttpRequests
从 node.js 创建 http 请求
支持 Promise API
拦截请求和响应
转换请求数据和响应数据
取消请求
自动转换 JSON 数据
客户端支持防御 XSRF

#### axios 发送 post 请求

```bash
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

// 可选地，上面的请求可以这样做
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

#### axios 发送 get 请求

```bash
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

#### vue-cli 引入 axios

1. npm install axios
2. 在 vue 的入口文件 main.js 里引入 axios 并使用

```bash
import axios from 'axios'

Vue.prototype.$axios = axios
```
