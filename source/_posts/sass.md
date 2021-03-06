---
title: sass
date: 2018-06-13 00:17:03
categories:
- CSS
tags:
- CSS
---
### SASS

#### 安装:
``` bash
npm install  node-sass  -g
```
安装成功
``` bash
node-sass -v
```

#### 编译:
将路径src/css的sass翻译到dist/css,并监听
``` bash
node-sass src/css/ -o dist/css/ -w
```

#### 语法:

##### 1.嵌套

css:
``` bash
 div {
     margin:20px;
 }
 div p {
     padding:20px;
 }
```
scss:
``` bash
div{
    margin:20px;
    p{padding:20px;}
}
```
##### 2.变量
css:
``` bash
a{
    color:#ddd;
}
p{
    color:#ddd;
}
```

scss:
``` bash
$color-test:#ddd;
a{
    color:$color-test;
}
p{
    color:$color-test;
}
```

##### 3.引用,用&引用父选择器
css:
``` bash
a{
    color:#111;
}
a:hover{
    color:#222;
}
a:active{
    color:#333;
}
```
scss:
``` bash
a{
    color:#111;
    &:hover{
        color:#222;
    }
    &:active{
        color:#333;
    }
}
```

##### 4.导入,@import

Sass 的 @import 指令用于导入其他样式模块。

假设现有 _variables.scss _buttons.scss _forms.scss 三个模块，可以通过一个 main.scss 导入这些模块。

scss:
``` bash
// main.scss
@import "variables";
@import "buttons";
@import "forms";
```
子模块文件前面的下划线用于告知 Sass 编译器不要把这个模块编译成单独的 CSS 文件

##### 5.嵌套@import

Sass 的 @import 指令可以嵌套在选择器内，产生嵌套效果

scss:
``` bash
@import "variables";
@import "mixins";

.slamdunk {
  min-width: 320px;
  @import "navbar";
  @import "content";
  @import "players";
}
```

 注意:CSS 也有 @import，在 IE 6-8 上会导致多个 CSS 文件不能同时下载的情况，影响网页性能

 ##### 6.运算

 Sass 支持对数字标准的算术运算(加法 +，减法 - ，乘法 *，除法 / 和取模 %) 并保留单位;

由于 CSS 中 / 可作为分隔符，因此除法运算要稍微注意以下情况。

scss:
 ``` bash
 p {
  font: 10px/8px;                // 原生的CSS，不作为除法
  $width: 1000px;
  width: $width/2;               // 使用了变量, 作为除法
  width: round(1.5)/2;           // 使用了函数, 作为除法
  height: (500px/2);             // 使用了括号, 作为除法
  margin-left: 5px + 8px/2px;    // 使用了 +, 作为除法
  font: (italic bold 10px/8px);  // 在一个列表（list）中，括号可以被忽略。
}
 ```

 css:
 ``` bash
 p {
  font: 10px/8px;
  width: 500px;
  height: 250px;
  margin-left: 9px;
}
 ```

 ##### 7.注释:

 单行注释 // 会在 .scss 被编译成 .css 后移除
 
 scss:
 ``` bash
 // Header
 .header{
     height:60px;
 }
 ```
 css:
 .header {
     height:60px;
 }

