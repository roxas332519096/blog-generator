---
title: 截图插件vue-cropper的使用
date: 2019-03-04 12:47:12
categories: 
- 库
tags:
- 库 
---

#### 介绍

vue-cropper是基于cropper.js封装的一个vue组件.功能强大.

[cropper.js链接](https://github.com/fengyuanchen/cropperjs#options "文档链接")

#### 安装

[官方链接](https://github.com/roxas332519096/vue-cropperjs "文档链接")

``` bash
npm install --save vue-cropperjs

// Global
import Vue from 'vue';
import VueCropper from 'vue-cropperjs';
Vue.component(VueCropper);

// Local
import VueCropper from 'vue-cropperjs';
export default {
  components: { VueCropper}
}

<vue-cropper
  ref="cropper"
  :src="imgSrc"
  alt="Source Image"
  :cropmove="cropImage"
/>
```
#### 配置

vue-cropper通过绑定属性进行配置

例如:

``` bash
<vue-cropper
    :viewMode="2"
/>
```

#### 初始化

``` bash
<vue-cropper
    :viewMode="2"
    drag-mode="crop"
    :background="true"
    ref="cropper"
    :src="imgSrc"
    key="cropKey" //由于cropper初始化时,option已决定截图框大小等,所以变换key使视图重新渲染
/>

<img :src="cropImg" />

data(){
  return {
    imgSrc:'图片url',
    cropKey:0,
    cropImg:'',
  }
}

const reader = new FileReader();
reader.onload = event => {
  this.imgSrc = event.target.result;
  this.$refs.cropper.replace(event.target.result);
};
reader.readAsDataURL(this.file);
```

#### 属性

##### vieMode显示模式

Type:number
Default:0

0:裁剪框只能在图片内移动
1:裁剪框能在容器内移动
2:裁剪框只能在图片内移动,并且图片最大缩小不能超出裁剪框(图片不平铺满容器,存在间隙)
3:裁剪框只能在图片内移动,并且图片最大缩小不能超出裁剪框(图片平铺满容器,不存在间隙)

##### dragMode 拖动模式

Default:'crop'
'crop':当鼠标点击一处时根据这个点重新生成一个裁剪框,不可拖动图片
'move':可拖动图片
'none':不可拖动图片

##### aspectRatio
Type:numbe
Default:NAN
可设置n/n,比例为n:n

##### preview
Type:string,element
Default:''
是一个选择器,必须被Document.querySelectorAll获取到

##### responsive
Type:Boolean
Default:true
在调整窗口大小的时候重新渲染cropper

##### modal
Type:Boolean
Default:true
截图时图片上方的黑色遮罩层

##### guides
Type:Boolean
Default:true
截图框虚线

##### center
Type:Boolean
Default:true
截图框在图片中烟

##### highlight
Type:Boolean
Default:true
突出截图框

##### background
Type:Boolean
Default:true
显示网格背景

##### autoCrop
Type:Boolean
Default:true
自动显示截图框

##### autoCropArea
Type:number
Default:0.8
截图框与图片的比例

##### movable
Type:Boolean
Default:true
是否可允许移动图片

##### rotatable
Type:Boolean
Default:true
是否可旋转图片

##### scalable
Type:Boolean
Default:true
是否可缩放图片

##### zoomable
Type:Boolean
Default:true
是否可放大图片

##### zoomOnTouch
Type:Boolean
Default:true
是否可通过触摸放大图片

##### zoomOnWheel
Type:Boolean
Default:true
是否可通过光标放大图片

##### wheelZoomRatio
Type:number
Default:0.1
用鼠标移动图像时，定义缩放比例

##### cropBoxMovable
Type:Boolean
Default:true
截图框是否可拖动

##### toggleDragModeOnDblclick
Type:Boolean
Default:true
点击两次可切换拖动模式与移动图片模式

##### minContainerWidth
Type:number
Default:200
容器最小宽度

##### minContainerHeight
Type:number
Default:100
容器最小高度

##### minCanvasWidth
Type:number
Default:0
canvas最小高度

##### minCanvasHeight
Type:number
Default:0
canvas最小高度

##### minCropBoxWidth
Type:number
Default:0
截图框最小宽度

##### minCropBoxHeight
Type:number
Default:0
截图框最小高度

##### ready
Type:function
Default:null
插件准备时执行的函数

##### cropstart
Type:function
Default:null
截图框开始移动执行的函数

##### cropmove
Type:function
Default:null
截图框移动执行的函数

##### cropend
Type:function
Default:null
截图框移动结束的函数

##### crop
Type:function
Default:null
截图框发生变化执行的函数

##### zoom
Type:function
Default:null
截图框缩放时执行的函数

#### 方法

``` bash
this.cropImg = this.$refs.cropper.getCroppedCanvas().toDataURL();
```
##### crop() 手动显示裁剪框

##### reset() 将图像和裁剪框重置为初始状态

##### clear() 清除截图框

##### replace(url[, onlyColorChanged]) 替换图像的src并重新构建cropper
url Type:string
onlyColorChanged Type:Boolean;Default:false
如果只是改变颜色，而不是大小，那么cropper只需要改变所有相关图像的src，不需要重新构建cropper。这可以用于应用过滤器。（意思是：改成true，图像的比例会发生变化自适应父盒子的大小；会失真的）

``` bash
this.$refs.cropper.replace('/img.jpg',true)
```

##### enable() 解锁锁定的截图框

##### disable() 锁定截图框

##### destroy() 销毁cropper并从图像中删除整个cropper

##### move(offsetX[,offsetY]) 使用相对偏移量移动图像(截图框不移动)

##### moveTo(x[,y]) 将容器移动到一个绝对点

##### zoom(ratio) 放大图片,并使用相对比例 (截图框不变化)
ratio type:number 

##### rotate(degree) 旋转图像以一定的角度
degree type:number

##### rotateTo(degree) 旋转图像到固定的角度
degree type:number

##### scale(scaleX[, scaleY]) 翻转图像
scaleX type:number 水平方向翻转 default:1
scaleY type:number 垂直方向翻转 假如不存在则与x相同

##### scaleX(scaleX) 缩放图像的横坐标

##### scaleY(scaleY) 缩放图像的纵坐标

##### getData([rounded]) 输出最终裁剪的区域位置和大小数据(根据原始图像的自然大小)
rounded 
Type:Boolean
Default:false 设置true可获得数据
返回数据
Type:Object
- x 截图框距离左边的距离
- y 截图框距离顶部的距离
- width 截图框的宽度
- height 截图框的高度
- rotate 截图框的旋转的角度
- scaleX 缩放图像的横坐标
- scaleY 缩放图像的纵坐标 

##### setData(data) 用新数据改变裁切区域的位置和大小(以原始图像为基础)
data
Type:Object

##### getContainerData() 输出container 容器大小数据
返回数据
Type:Object
- Width 当前容器宽度
- Height 当前容器高度

##### getImageData() 输出图像image位置,大小和其他相关数据
返回数据
Type:Object
- left image距离左边的距离
- top image距离顶部的距离
- width image的宽度
- height image的高度
- naturalWidth image的原始宽度
- naturalHeight image的原始高度
- aspectRatio image的纵横比
- rotate image的旋转的角度
- scaleX 缩放图像的横坐标
- scaleY 缩放图像的纵坐标

##### getCanvasData() 输出画布Canvas(图像包装器)位置和大小数据
返回数据
Type:Object
- left canvas距离左边的距离
- top canvas距离顶部的距离
- width canvas的宽度
- height canvas的高度
- naturalWidth canvas的原始宽度
- naturalHeight canvas的原始高度

##### setCanvasData(data) 使用数据更改画布Canvas(图像包装器)位置和大小
返回数据
Type:Object
- left canvas距离左边的距离
- top canvas距离顶部的距离
- width canvas的宽度
- height canvas的高度

##### getCropBoxData() 输出截图框的位置和大小数据
返回数据
Type:Object
- left 截图框距离左边的距离
- top 截图框距离顶部的距离
- width 截图框的宽度
- height 截图框的高度

##### setCropBoxData(data) 改变截图框的位置和大小数据
返回数据
Type:Object
- left 截图框距离左边的距离
- top 截图框距离顶部的距离
- width 截图框的宽度
- height 截图框的高度

#####  getCroppedCanvas([options])—画一张剪裁的图片,如果没有剪裁，则返回一个绘制整个im的画布
options
Type:Object
options 类型Object
- width 输出Canvas的宽度
- height 输出Canvas的高度
- minWidth 输出Canvas的最小宽度；默认值是0
- minHeight 输出Canvas的最小高度；默认值是0
- maxWidth 输出Canvas的最大宽度；默认值是Infinity（无穷大）
- maxHeight 输出Canvas的最大高度；默认值是Infinity（无穷大）
- fillColor 在输出画布Canvas中填充任何alpha的颜色，默认值是透明的
- imageSmoothingEnabled 如果图像被设置为平滑(true，默认)或不设置(false)。
- imageSmoothingQuality 设置图像的质量，一个“low”(默认)、“medium”或“high”

返回数据：
Type：HTMLCanvasElement画布绘制出了剪裁过的图像
注意：输出canvas画布的宽高比将自动适应剪切框的纵横比.
如果你打算从输出画布canvas中获得一个JPEG图像，您应该首先设置填色选项,否则,JPEG图像中的透明部分将在缺少情况下变为黑色.
为了避免获得空白的输出图像,您可能需要将maxWidth和maxHeightproperties设置为有限的数字,从而来画布元素的大小限制.

##### setAspectRatio(aspectRatio) 改变裁切框的宽高比
aspectRatio:
Type:number 是一个正数

##### setDragMode([mode]) 设置拖拽模式,鼠标显示的是十字还是那种带箭头的十字
mode:
Type:string (none,crop,move)
Default:null
