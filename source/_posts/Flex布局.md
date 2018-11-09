---
title: Flex布局
date: 2018-06-15 20:39:34
tags:
---
### FLEX布局

### flex container的属性

#### flex-direction 方向

##### 属性:

1. row 水平
2. row-reverse 水平反向
3. column 垂直
4. column-reverse 垂直反向


#### flex-wrap 换行

##### 属性
1. nowrap 不换行(默认)
2. wrap 换行

#### flex-flow

direction 与 wrap 的简写

#### justify-content 主轴方向对齐方式

假如是默认或者row主轴就是横着的
假如是column主轴就是竖着的

##### 属性
1. flex-start 主轴起点开始
2. flex-end 主轴起点结束
3. center 主轴居中
4. space-between 空的放在中间 
5. space-around 空的放在两边

#### align-items 子元素对齐方式

#### 属性
1. stretch 默认,把所有元素高度伸长到一样高.
2. flex-start 所有元素往起点靠
3. flex-end  所有元素往终点靠
4. center    所有元素居中对齐

#### align-content 垂直行对齐 

1. stretch 
2. flex-start 靠近起点
3. flex-end  靠近终点
3. center 主轴居中
4. space-between 空的放在中间 
5. space-around 空的放在两边

### flex item 的属性

#### flex-grow 增长比例(空间过多时)

属性数字:按比例分配 默认是0
假如某div是任意数字,其他是0,那么这个div占其余所有空间

#### flex-shrink 收缩比例 (一般不用)

属性数字:比例分配 默认是0

#### flex-basis 默认大小(一般不用)

不写就是原始大小,写了就是写的小

#### flex 上面3个的缩写

#### order 顺序

属性数字:是一个index,改变顺序

#### align-self 自身的对齐方式

item自身的对齐方式

同justify-content,align-content.

### 使用flex布局

1. 手机页面布局 (topbar+main+tabs)

预览:https://roxas332519096.github.io/flex-demo/手机页面布局.html

2. 产品列表(ul>li*9)

预览:https://roxas332519096.github.io/flex-demo/产品列表.html

3. PC页面布局(双飞翼)

预览:https://roxas332519096.github.io/flex-demo/PC页面布局.html

4. 完美居中

预览:https://roxas332519096.github.io/flex-demo/完美居中.html

