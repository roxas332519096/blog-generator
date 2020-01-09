---
title: 自动化测试&发布npm包
date: 2019-04-09 15:49:19
categories:
- 库
tags:
- 库
---

#### 1. 自动化测试

1. kama一个测试运行器,可呼起浏览器,加载测试脚本,运星测试用例.
2. mocha是一个单元测试框架/库,可以用来写测试用例.
3. sinon是一个spy/stub/mock库,用以辅助测试.

运行
``` bash
npm i -D karma karma-chrome-launcher karma-mocha karma-sinon-chai mocha sinon sinon-chai karma-chai karma-chai-spies
```

创建karma配置,karma.conf.js

输出目录:*代表加载所有文件
``` bash
    files: [
        'dist/**/*.test.js',
        'dist/**/*.test.css'
    ]
```
运行浏览器

``` bash
browsers: ['ChromeHeadless'],
```

代码:

``` bash
    module.exports = function (config) {
         config.set({

             // base path that will be used to resolve all patterns (eg. files, exclude)
             basePath: '',

            // frameworks to use
            // available frameworks: https://npmjs.org/browse/keyword/karma-adapter
            frameworks: ['mocha', 'sinon-chai'],
            client: {
                chai: {
                    includeStack: true
                }
            },


            // list of files / patterns to load in the browser
            files: [
                'dist/**/*.test.js',
                'dist/**/*.test.css'
            ],


            // list of files / patterns to exclude
            exclude: [],


            // preprocess matching files before serving them to the browser
            // available preprocessors: https://npmjs.org/browse/keyword/karma-preprocessor
            preprocessors: {},


            // test results reporter to use
            // possible values: 'dots', 'progress'
            // available reporters: https://npmjs.org/browse/keyword/karma-reporter
            reporters: ['progress'],


            // web server port
            port: 9876,


            // enable / disable colors in the output (reporters and logs)
            colors: true,


            // level of logging
            // possible values: config.LOG_DISABLE || config.LOG_ERROR || config.LOG_WARN || config.LOG_INFO || config.LOG_DEBUG
            logLevel: config.LOG_INFO,


            // enable / disable watching file and executing tests whenever any file changes
            autoWatch: true,


            // start these browsers
            // available browser launchers: https://npmjs.org/browse/keyword/karma-launcher
            browsers: ['ChromeHeadless'],


            // Continuous Integration mode
            // if true, Karma captures browsers, runs the tests and exits
            singleRun: false,

            // Concurrency level
            // how many browser should be started simultaneous
            concurrency: Infinity
        })
    }
```

创建test/button.test.js文件

``` bash
const expect = chai.expect;
 import Vue from 'vue'
 import Button from '../src/button'

 Vue.config.productionTip = false
 Vue.config.devtools = false

describe('Button',()=>{
    it('xxx',()=>{
        //测试代码
    })
})
```
创建测试脚本

在 package.json 里面找到 scripts 并改写 scripts
``` bash
"scripts": {
     "dev-test": "parcel watch test/* --no-cache & karma start",
     "test": "parcel build test/* --no-minify && karma start --single-run"
 },
```

运行测试脚本

1. npm run test 一次性运行
2. npm run dev-test 进行watch运行

#### 2.使用Mocha&Chai做单元测试

BDD  行为驱动测试

descrube 描述
expect 期待
eq 输出
deep 深相等
not 不
with 并且

descrube 'people'

it has a head 
it can run

expect('xxx').eq('yyy')

文档: www.chaijs.com

#### 3. 使用TravisCI做持续集成

注册travis账户.

根目录下创建 .travis.yml 文件

每次提交后可在travis上查看测试结果.

``` bash
language: node_js
node_js:
  - "8"
addons:
  chrome: stable
sudo: required
before_script:
  - "sudo chown root /opt/google/chrome/chrome-sandbox"
  - "sudo chmod 4755 /opt/google/chrome/chrome-sandbox"
```

#### 为什么一个空数组不等于空数组
 
因为引用不同,是两个数组

``` bash
[] == [] //false

var a = []
a == [] //false
a == [] //true
```

#### 4. 发布npm包

根目录下创建index.js
导入组件 导出组件
``` bash
improt cp from './src/cp'
exprot {cp}
```

查看自己当前npm源路径
``` bash
npm config list
```

要改成默认源才能发布npm包
每次发布需要更改package.json里的版本
```bash
//添加用户
npm adduser

//公开代码
npm publish
```

由于引擎不能识别improt 所以要babel转移或者直接给他转义好

转义

``` bash
//packjson输出目录修改成dist/index.js

运行

npx parcel build index.js --no-cache --no-minify
```

#### 5. 使用npm link

由于每次更新都需要更改package.json里的版本,然后npm publish,所以我们可以用本地调试,在项目目录使用npm link,在所用目录运行npm link xxx.

#### 6. 书写README

shields.io生成图标

#### 7. 安装git open

```  bash
npm i -g git-open
```

#### 8. git会到之前版本

``` bash
git reset --hard xxx
```