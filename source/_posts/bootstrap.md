---
title: bootstrap
date: 2018-08-03 04:19:41
tags:
---

#### 网格系统/栅栏系统

所有代码在container里面

row 会有margin负15px,使容器扩大,不使用row会有bug

row一共12列

col-md-x 占x列

col-md-x col-md-offset-y 占x列 偏移y列(左边空出y列)

默认有4个媒体查询分界值

1200 992 768 0

lg(1200-max) 大屏幕   col-lg-1 大屏幕占1格
md(992-1200) 中等屏幕 col-md-2 中等屏幕占2格
sm(992-768) 小屏幕   col-sm-3 小屏幕占3格 
xs(0-768) 超小屏幕 col-xs-6 超小屏幕占6格
``` bash
<div class="container">
    <div class="row">
        <div class="col-lg-1 col-md-2 col-sm-3 col-xs-6">col</div>
    </div>
</div>
```

隐藏

.hidden-xs

右浮动(要注意宽度)

pull-right

#### 复杂组件

##### css
icon

下拉列表 

导航栏

分页

图片

##### js

弹出框




