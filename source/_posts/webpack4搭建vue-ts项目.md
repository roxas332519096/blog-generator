---
title: webpack4搭建vue-ts项目
date: 2020-01-13 22:24:51
categories:
- TS
tags:
- TS
---

1. 创建根目录

``` bash
mkdir webpack-demo
cd webpack-demo
npm init -y
npm install webpack webpack-cli --save-dev
```

2. 创建index.js

``` bash
|- /src
   |- index.js
```

index.js

``` bash
var div = document.createElement('div')
div.id = 'app'
document.body.appendChild(div)
```

3. 创建webpack.config.js

``` bash
|- webpack.config.js
|- /src
    |- index.js
```

``` bash
//webpack.config.js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  mode:'development',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist'),
  },
};
```

4. 运行打包项目

``` bash
npx webpack --config webpack.config.js
```

5. 安装sever
``` bash
npm i  -D webpack-dev-server
```

在package.json添加

``` bash
"scripts": {
    "dev": "webpack-dev-server --open",
}

//在终端中输入
npm run dev
启动项目
```

6. 安装HtmlWebpackPlugin

``` bash
npm i --save-dev html-webpack-plugin
```
webpack.config.js
``` bash
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
    entry: './src/index.js',
    mode: 'development',
    output: {
        filename: 'main.js',
        path: path.resolve(__dirname, 'dist'),
    },
    plugins: [
        new HtmlWebpackPlugin()
    ]
};
```

至此项目已经可以正常运行了

7. 安装vue

``` bash
npm i vue
npm i -D vue-loader
npm i -D vue-template-compiler
```

创建一个组件main.vue,这个很简单就不说了.

index.js

``` bash
import Vue from 'vue'
import main from './main.vue'

new Vue({
    render: h => h(main)
}).$mount('#app')
```

webpack.config.js

``` bash
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin')
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module.exports = {
    entry: './src/index.js',
    mode: 'development',
    resolve: {
        extensions: [".ts", ".tsx", ".js"]
    },
    module: {
        rules: [
            {
                test: /\.vue$/,
                loader: 'vue-loader'
            }
        ]
    },
    plugins: [
        new HtmlWebpackPlugin(), new VueLoaderPlugin()
    ]
};
```

至此,可以运行vue了.

8. 安装TS

``` bash
npm i typescript
npm install ts-loader --save-dev
```

创建tsconfig.json
``` bash
{
    "compilerOptions": {
        "sourceMap": true
    }
}
```

修改webpack.config.js
``` bash
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin')
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module.exports = {
    entry: './src/index.ts',   //这里改成ts
    mode: 'development',
    output: {
        filename: 'main.js',
        path: path.resolve(__dirname, 'dist'),
    },
    resolve: {
        extensions: [".ts", ".tsx", ".js"] //读取ts文件
    },
    module: {
        rules: [
            {
                test: /\.vue$/,
                loader: 'vue-loader'
            },
            {
                test: /\.tsx?$/, //新增规则
                loader: "ts-loader"
            }
        ]
    },
    plugins: [
        new HtmlWebpackPlugin(), new VueLoaderPlugin()
    ]
};
```

此时index.ts引入vue文件会报错

9. 在TS里引入vue

创建shims-vue.d.ts

``` bash
declare module '*.vue' {
    import Vue from 'vue'
    export default Vue
}
```

10. 在vue里使用ts

修改webpack.config.js
新增两个loader的options
``` bash
    module: {
        rules: [
            {
                test: /\.vue$/,
                loader: 'vue-loader',
                options: {
                    esModule: true
                }
            },
            {
                test: /\.tsx?$/,
                loader: "ts-loader",
                options: {
                    appendTsSuffixTo: [/\.vue$/]
                }
            }
        ]
    },
```

