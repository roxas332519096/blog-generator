---
title: web图片的使用
date: 2019-04-16 17:34:44
categories:
tags:
---

#### FileReader

FileReader 对象,使用 File 或 Blob 对象指定要读取的文件或数据.

其中 File 对象可以是: 1. input 元素上选择文件后返回的 FileList 对象 2. 拖放操作生成的 DataTransfer 对象 3. 来自 HtmlCanvasElment 上执行 mozGetAsFile()方法后返回的结果.

##### 参数

###### FileReader.error(只读)

表示在读取文件时发生的错误

###### FileReader.readyState(只读)

表示 FileReader 状态数组 1. EMPTY 0 等待 2. LOADING 1 正在被加载 3. DONE 2 已完成全部的读取请求.

###### FileReader.result(只读)

文件的内容.该属性仅在读取操作完成后才生效,数据的格式取决于使用哪个方法来启动读取操作.

##### 事件处理函数

###### FileReader.onabort:

处理 abort 事件.该事件在读取操作被中断时触发.

###### FileReader.onerror：

处理 error 事件.该事件在读取操作发生错误时触发.

###### FileReader.onload：

处理 load 事件.该事件在读取操作完成时触发.

###### FileReader.onloadstart：

处理 loadstart 事件。该事件在读取操作开始时触发.

###### FileReader.onloadend：

处理 loadend 事件.该事件在读取操作结束时(要么成功，要么失败)触发.

###### FileReader.onprogress：

处理 progress 事件.该事件在读取 Blob 时触发.

##### 方法

###### FileReader.abort()：

中止读取操作.在返回时，readyState 属性为 DONE。

###### FileReader.readAsArrayBuffer()：

开始读取指定的 Blob 中的内容.一旦完成，result 属性将包含一个 ArrayBuffer 来表示文件数据.

###### FileReader.readAsBinaryString()：

开始读取指定的 Blob 中的内容.一旦完成，result 属性中将包含所读取文件的原始二进制数据.

###### FileReader.readAsDataURL()：

开始读取指定的 Blob 中的内容.一旦完成,result 属性中将包含一个 data: URL 格式的字符串以表示所读取文件的内容.

###### FileReader.readAsText()：

开始读取指定的 Blob 中的内容.一旦完成，result 属性中将包含一个字符串以表示所读取的文件内容.

```bash
onDrop(files) {
    files.forEach(file => {
        const reader = new FileReader();
        reader.onload = () => {
            console.log(file);
            const fileAsBinaryString = reader.result; //返回文件
            //...
        }
        reader.onabort = () => {
            console.log('aborted')
        }
        reder.onerror = () => {
            console.log('error')
        }
        reader.readAsBinaryString(file); //返回二进制文件
    })
}
```

#### base64(dataURL)格式

base64 编码是使用 64 个字符将二进制数据转换成文本数据的方案,对于非二进制数据,则先转换成二进制,然后每连续 6 比特(2 的 6 次方=64)计算其十进制,该数据值在上面的索引表中找到对应的字符,最终得到一个文本字符串.

base64 格式数据,Data URI scheme.

Data URI scheme 支持类型

```bash
data:,文本数据
data:text/plain,文本数据
data:text/html,HTML 代码
data:text/html;base64,base64 编码的 HTML 代码
data:text/css,CSS代码
data:text/css;base64,base64 编码的 CSS 代码
data:text/javascript,Javascript 代码
data:text/javascript;base64,base64 编码的 Javascript代码
data:image/gif;base64,base64 编码的 gif 图片数据
data:image/png;base64,base64 编码的 png 图片数据
data:image/jpeg;base64,base64 编码的 jpeg 图片数据
data:image/x-icon;base64,base64 编码的 icon 图片数据
```

#### Blob 格式

Blob(Binary large object),二进制大对象,是一个可以存储二进制文件的容器.

Blob 是一个大文件,典型的 Blob 是一张图片或一个声音文件,由于它们的尺寸,必须使用特殊的方式来处理(例如:上传,下载或者存放到一个数据库).

```bash
Blob{
    name:"name",
    preview:"blob:file:///f3823a2a-2908-44cb-81e2-c19d98abc5d1",
    size: 47396,
    type: "image/png",
}
```

上面的 preview 可以直接使用做图片预览.

#### base64 转 Blob

```bash
base64ToBlob(b64data, contentType, sliceSize) {
  sliceSize || (sliceSize = 512);
  return new Promise((resolve, reject) => {
    // 使用 atob() 方法将数据解码
    let byteCharacters = atob(b64data);
    let byteArrays = [];
      for (let offset = 0; offset < byteCharacters.length; offset += sliceSize) {
        let slice = byteCharacters.slice(offset, offset + sliceSize);
        let byteNumbers = [];
        for (let i = 0; i < slice.length; i++) {
            byteNumbers.push(slice.charCodeAt(i));
        }
        // 8 位无符号整数值的类型化数组。内容将初始化为 0。
        // 如果无法分配请求数目的字节，则将引发异常。
        byteArrays.push(new Uint8Array(byteNumbers));
      }
      resolve(new Blob(byteArrays, {
        type: contentType
      }))
  })
}
```

调用

```bash
//dataUri就是base64文件
let blob = await this.base64ToBlob(dataUri.split(',')[1], 'image/png');
```

```bash
Blob {
    size: 47396,
    type: "image/png",
}
```

补充:

```bash
Object.assign(blob,{
  // jartto: 这里一定要处理一下
  preview: URL.createObjectURL(blob),
  name: `图片示例：${index}.png`
});
```

#### Blob 转 base64

```bash
blobToBase64(blob) {
  return new Promise((resolve, reject) => {
    const fileReader = new FileReader();
    fileReader.onload = (e) => {
      resolve(e.target.result);
    };
    fileReader.readAsDataURL(blob);
    fileReader.onerror = () => {
      reject(new Error('文件流异常'));
    };
  });
}
```

调用

```bash
const allBase64 = await this.blobToBase64(blobObj);
```

#### URL 转 base64

使用 canvas

```bash
getDataUri(url) {
  return new Promise((resolve, reject) => {
    /* eslint-disable */
    let image = new Image();
    //解决跨域问题
    image.setAttribute("crossOrigin",'Anonymous');
    image.onload = function() {
      let canvas = document.createElement('canvas');
      canvas.width = this.naturalWidth;
      canvas.height = this.naturalHeight;
      canvas.getContext('2d').drawImage(this, 0, 0);
      // Data URI
      resolve(canvas.toDataURL('image/png'));
    };
    image.src = url;
    // console.log(image.src);
    image.onerror = () => {
      reject(new Error('图片流异常'));
    };
  });
}
```

调用

```bash
let dataUri = await this.getDataUri(`image/test/jartto.png`);
```

#### src 转 image

```bash
srctoimage(src){
    return new Promise((reslove,reject)=>{
    let img = new Image()
    img.onload = function(){
      reslove(img)
    }
    img.onerror = function(err) {
      reject(err)
    }
    img.src = src
  })
}
```

调用

```bash
let image = await this.srctoimage(src);
```

#### img 转 canvas

```bash
imgtocanvas(img){
    let canvas = document.createElement("canvas");
    let ctx = canvas.getContext('2d')
    canvas.width = img.width
    canvas.height = img.height
    ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
    return canvas
}
```

调用

```bash
let canvas = this.imgtocanvas(img);
```

#### ImageData 转 canvas

```bash
ImageDatetocanvas(imgData){
    let canvas = document.createElement("canvas");
    let ctx = canvas.getContext('2d')
    canvas.width = imgData.width
    canvas.height = imgData.height
    ctx.putImageData(imgData,canvas.width, canvas.height);
    return canvas
}
```

调用

```bash
let canvas = this.ImageDatetocanvas(imgData);
```

#### canvas 转 ImageData

```bash
canvastoImageDate(canvas){
    let ctx = canvas.getContext('2d')
    return ctx.createImageData(canvas.width,canvas.height)
}
```

调用

```bash
let imgdata = this.canvastoImageDate(canvas);
```

#### canvas 像素操作

```bash
function canvaspixel(canvas,deal) {
  let ctx = canvas.getContext('2d')
  var imgData = ctx.createImageData(canvas.width, canvas.height);
  for (var i = 0; i < imgData.data.length; i += 4) {
    deal(r,g,b,a)
  }
  ctx.putImageData(imgData, canvas.width, canvas.height);
  return canvas
}
```

调用

```
let editcanvas = canvaspixel(canvas,deal)
```

#### base64(DataURL)

```bash
canvas.toDataURL()
```

更多请查看
https://juejin.im/post/5c00e8a66fb9a049db72dbd0
