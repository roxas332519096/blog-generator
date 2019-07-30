---
title: vue-cli手脚架
date: 2018-07-25 16:42:39
categories:
- vue
tags:
- vue
---
#### 安装

``` bash
npm install -g @vue/cli
```

安装成后可运行次命令检测是否成功

``` bash
vue --version
```

#### 安装vue serve

```
npm install -g @vue/cli-service-global
```

#### 创建一个项目
``` bash
winpty vue.cmd create 项目名称
```

#### 选项

##### 1.选择特性
有两个路线选择如何加载插件,按Enter确定,上下移动,回车选择/取消.

``` bash
1. default 默认
2. Manually select features 手动选择
```

##### 2.1 默认加载
``` bash
```
 
##### 2.2 手动加载

##### 2.2.1 选择加载插件
``` bash
1. Babel
2. TS
3. PWA Support
4. Router
5. Vuex
6. Css Pre-processors 支持CSS预处理器
7. Linter / Formatter 支持代码风格检查和格式化
8. Uint Testing 支持单元测试
9. E2E Testing 支持E2E测试
```
##### 2.2.2 router设置

Use history mode for router?
是否使用history模式(需要后台支持)

##### 2.2.3 CSS预处理器选择

Sass/SCSS
Less
Stylus

##### 2.2.4 配置文件位置

In dedicated config files 根目录
package.json

##### 2.2.5 未来是否使用该配置


#### 启动项目
``` bash
npm run server
```

#### 输出项目
``` bash
npm run build
```

#### 关于vue.config.js

vue.config.js属于可选文件,需要自己手动去创建

#### 如何部署本地(github)

在根目录下创建vue.config.js

``` bash
module.exports = {
    publicPath: './'
  }
```

#### assets 和 static文件夹的区别

assets目录中的文件会被webpack处理解析为模块依赖,只支持相对路径形式

static/ 目录下的文件并不会被Webpack处理:它们会直接被复制到最终的打包目录(默认是dist/static)下.必须使用绝对路径引用这些文件,这是通过在 config.js 文件中的 build.assetsPublicPath 和 build.assetsSubDirectory 连接来确定的
任何放在 static/ 中文件需要以绝对路径的形式引用: /static/[filename]

总的来说：static放不会变动的文件 assets放可能会变动的文件

#### --save-dev和-save的区别
即-d和-s的区别

--save-dev安装依赖的时候会在package.json的devDependencies对象下面

--save安装依赖的时候会在dependencies对象下面

总结:--save是发布后依赖的东西,--save-dev是开发依赖的东西.