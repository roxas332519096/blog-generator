---
title: 动态REM
date: 2018-05-27 22:12:35
categories:
- CSS
tags:
- CSS
---
### 1 什么是 REM

##### px 
像素,网页默认font-size:16px
其他浏览器最小字体像素是6px;
chrome最小字体像素是12px;
##### em 
一个M的宽度,一个汉字的宽度.
##### rem 
root em 根元素(html)的font-size大小.
注意是html,不是body
##### vh 
viewport height 100vh:视口宽度.
##### vm 
viewprot widht 100vw 视口宽度.

### 2 REM 和 EM 的区别是什么

EM:自己font-size大小.

REM:root em 根元素(html)的font-size大小.

### 3 手机端方案的特点

#### 如何做响应式

几款常用手机分辨率大小如下:
iP6S  375x667
iP6+  414x736
ip5   320x568
Nexus 412x732

响应式
0~320    CSS-1
320~375  CSS-2
375~414  CSS-3

#### 1.百分比布局

预览:
https://roxas332519096.github.io/notes-demo/0527-%E5%8A%A8%E6%80%81REM-%E7%99%BE%E5%88%86%E6%AF%94%E7%BC%A9%E6%94%BE.html


例:
``` bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>百分比缩放事例</title>
    <style>
        *{margin: 0;padding: 0;}
        .child{
            background: #ddd;
            margin-top:10px;
            margin-bottom: 10px;
            text-align: center;
            float: left;
            width: 40%;
            margin-left: 5%;
            margin-right: 5%;
        }
        .clearfix::after{
            content: '';
            display: block;
            clear: both;
        }
    </style>
</head>
<body>
    <div class="parent clearfix">
        <div class="child">40%</div>
        <div class="child">40%</div>
        <div class="child">40%</div>
        <div class="child">40%</div>
    </div>
</body>
</html>
```
##### 缺点:高度无法决定.高度与宽度不能关联,以为你宽度是百分比.

#### 2.整体缩放

REM方案:

##### 所有手机显示的界面都是一样的，只是大小不同.

##### 1 rem == html font-size == viewport width

### 4 使用 JS 动态调整 REM

``` bash
 <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
 <script>
     var pageWidth = window.innerWidth
     document.write('<style>html{font-size:'+ pageWidth +'px;}</style>')
 </script>
```

预览:
https://roxas332519096.github.io/notes-demo/0527-%E5%8A%A8%E6%80%81REM-REM%E6%96%B9%E6%A1%88.html


``` bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>REM方案</title>
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
     <script>
         var pageWidth = window.innerWidth;
         document.write('<style>html{font-size:'+ pageWidth/10 +'px;}</style>')
     </script>
     <style>
         *{margin: 0;padding: 0;}
            .clearfix::after{
                content: '';
                display: block;
                clear: both;
        }
        *{box-sizing: border-box;}
        body{
            font-size:16px;
        }
        .child{
            background: #ddd;
            width: 4rem;
            height: 2rem;
            margin: 0.5rem 0.5rem;
            float: left;
            text-align: center;
            line-height: 2rem;
        }
    </style>
</head>
<body>
    <div class="parent clearfix">
        <div class="child">40%</div>
        <div class="child">40%</div>
        <div class="child">40%</div>
        <div class="child">40%</div>
    </div>
</body>
</html>
```
### 5 REM 可以与其他单位同时存在

```bash
font-size: 16px;
border: 1px solid red;
width: 0.5rem;
```

### 6 在 SCSS 里使用 PX2REM
```bash
npm config set registry https://registry.npm.taobao.org/ //从淘宝镜像下载
touch ~/.bashrc //创建一个文件决定从哪里下载
echo 'export SASS_BINARY_SITE="https://npm.taobao.org/mirrors/node-sass"' >> ~/.bashrc //把这句话加入之前的文件里
source ~/.bashrc 
npm i -g node-sass
mkdir ~/Desktop/scss-demo
cd ~/Desktop/scss-demo
mkdir scss css
touch scss/style.scss
start scss/style.scss
node-sass -wr scss -o css //scss代表scss的目录 css代表输出目录
```

编辑 scss 文件就会自动得到 css 文件
在 scss 文件里添加

``` bash
@function px( $px ){
  @return $px/$designWidth*10 + rem; //10代表js取REM的时候页面宽度除以的数
}

$designWidth : 640; // 640 是设计稿的宽度，你要根据设计稿的宽度填写。如果设计师的设计稿宽度不统一，就杀死设计师，换个新的。

.child{
  width: px(320);
  height: px(160);
  margin: px(40) px(40);
  border: 1px solid red;
  float: left;
  font-size: 1.2em;
}
```

即可实现 px 自动变 rem.
