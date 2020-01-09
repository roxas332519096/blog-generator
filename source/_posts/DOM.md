---
title: DOM
date: 2018-05-09 18:52:32
categories:
- JS
tags:
- JS
---
### DOM 

document object model
文档对象模型

### Ndoe

Document <HTML>标签的父元素,但根元素是HTML
Elment 
Text #注意看起来是文本,其实是一个对象
Comment 

页面中的节点通过,构造函数,变成对象

#### Node接口属性

##### childNodes

如果一个节点有父节点，那么该节点就继承了ChildNode接口。

###### 可以用以下方法

1. remove()
2. before()
3. after()
4. replaceWith()

##### parentNode

如果当前节点是父节点，就会继承ParentNode接口。由于只有元素节点（element）、文档节点（document）和文档片段节点（documentFragment）拥有子节点，因此只有这三类节点会继承ParentNode接口。

###### 可以用以下方法

1. children
2. firstElementChild
3. lastElementChild
4. childElementCount
5. append()
6. prepend() //功能与5一样

##### firstChild,lastChild,

##### innerText,outerText,

##### textContent

与innerText区别:

1. textContent获取所有元素内容包括script和style;
2. innerText检查css,不会返回隐藏元素的文本display:none,却性能低;

##### nextSibling,previousSibling,

这个两个可能会获取到文本节点

##### nodeName
获取的都是大写的,只有svg是小写,

##### nodeType

1为标签,3为文本 document.nodeType === Node.DOCUMENT_NODE

确定节点类型可以使用nodeType属性
```` bash
var node = document.documentElement.firstChild;
if (node.nodeType !== Node.ELEMENT_NODE) {
  console.log('该节点是元素节点');
}
````

##### nodeValue 

只有文本节点或注释才能返回值,其余为null

##### ownerDocument

获得根对象

##### parentElement

获得父元素节点,假如父节点不是元素则为null


##### NodeList 与 HTMLCollection 

相同:返回伪数组,不能push和pop

HTMLCollection与NodeList区别:

1. HTMLCollection实例对象的成员只能是Element节点，NodeList实例对象的成员可以包含其他节点。 
2. HTMLCollection实例对象都是动态集合,NodeList实例对象可能是动态集合，也可能是静态集合,目前,只有Node.childNodes是一个动态集合,其他NodeList是静态集合时反映在集合中。
3. HTMLCollection实例对象可以用id属性或name属性引用节点元素，NodeList只能使用数字索引引用。 

#### Node接口的方法

##### appendChild() 

创建子节点

##### insertBefore(节点1,参考节点) 
将节点1插入到参考节点之前,假如要将节点1插入到参考节点之后,要使用 insertBefore(节点1,参考节点.nextSibling),注意参考节点不能省略

##### cloneChild() 

复制节点,但是会丧失监听属性,即addEventListener方法和on-属性

1. 浅拷贝 cloneChild(false) 默认就是false,只拷贝节点,不拷贝子节点

2. 深拷贝 cloneChild(true),不仅拷贝节点,也拷贝子节点

##### removeChild() 

移除节点,不在页面里,还在内存里,注意调用的是父节点

##### replaceChild()

替换节点,之前的节点在内存里

##### contains() 

一个节点是否是参考节点的子节点或其本身

##### hasChildNodes() 

是否有子节点,返回布尔值

##### isEqualNode() 

是否相等节点,看起来一样

##### isSameNode() 
是否相同节点,是否同一个
```` bash
var p1 = document.createElement('p');
var p2 = document.createElement('p');

p1.isSameNode(p2) // false
p1.isSameNode(p1) // true
````

##### normalize() 
常规化
```` bash
var wrapper = document.createElement('div');

wrapper.appendChild(document.createTextNode('Part 1 '));
wrapper.appendChild(document.createTextNode('Part 2 '));

wrapper.childNodes.length // 2
wrapper.normalize();
wrapper.childNodes.length // 1
````
### Document

#### Document接口的属性

##### body 

获取body元素

##### head 

获取head标签

##### images 

获取所有image标签

##### links 

获取所有a标签

##### title 

获取title标签

##### scripts 

获取所有script标签

##### characterSet 

获取字符编码

##### childElementCount 

获取子元素的个数,用数字表示

##### children 

获取子节点

##### doctype 

获取文档类型

##### documentElement 

获取根元素,即<HTML>

##### domain 

获取域名

##### location 

获取Location对象,其中包含有关文档当前位置的信息.

##### onxxxxxxxxx 

一系列的事件监听

##### origin 

源

##### plugins 

是否有flash插件

##### readyState 

是否下载完成

##### referrer 

引荐者,http发出请求时,可以用referrer拒绝别的访问

##### hidden 

获取隐藏标签

##### scrollingElement

获取正在滚动的元素

##### styleSheets 

获取所有css

##### visibilityState 

获取页面是否被显示

#### Document接口的方法

##### getElementById() 

获取该id的标签

##### getElementsByClassName() 

获取该class的标签

##### getElementsByName() 

获取该name属性的标签

##### getElementsByTagName() 

获取该标签名的标签

##### querySelector() 

获取第一个该选择器的标签

##### querySelectorAll() 

获取所有该选择器的标签,

与childNodes的区别:

1. 相同:都是返回伪数组

2. 区别:
childNodes 是动态集合。所谓动态集合就是一个活的集合，DOM树删除或新增一个相关节点，都会立刻反映在NodeList接口之中
querySelectorAll方法返回的是一个静态集合。DOM内部的变化，并不会实时反映在该方法的返回结果之中。 


##### createElement() 

创建标签

##### createTextNode() 

创建文本节点

##### createAttribute() 

创建新属性

##### createDocumentFragment()

创建一个空的文档片段对象

##### open() 

打开

##### close() 

关闭,当执行doucment.wrtie时,页面会自动先document.open() -> docment.write -> document.close() 假如close之后写用write,会重新调用open,会覆盖之前write

##### write() 

写入文本
##### writeln() 

写入一行文本

##### execCommand() 

执行一个命令

##### exitFullscreen() 

退出全屏

##### getSelection() 

获取用户选择的文本

##### hasFocus() 

用户是否在当前页面上

### Element

#### Element接口的属性

##### 元素特性相关属性

##### id

读写id属性

##### tagName

读写标签名,与nodeName相等,值为大写

##### dir 

读写元素文字当前放向,ltr为从左到右,rtl为从右到左

##### accessKey

读写分配给当前元素的快捷键

##### draggable

元素是否能拖动,返回一个布尔值,可读写

##### lang

读写当前元素的语言

##### title

读写HTML属性title,通常用来指定,鼠标悬浮时单出的文字提示框

##### 元素状态相关属性

##### hidden

返回布尔值,元素是否可见,可以读写,控制元素是否可见;
与CSS独立,CSS可见高于该属性

##### contentEditable,
返回字符串;
设置contentEditable属性，使得元素的内容可以编辑;
"true"可编辑;
"false"不能编辑;
"inherit"继承父元素;

##### isContentEditable

返回布尔值,元素是否可以编辑,只读


##### className

读写元素class属性

##### classList

返回class属性值的数组

###### 可以用以下方法改变classList

1. add()：增加一个 class。
2. remove()：移除一个 class。
3. contains()：检查当前元素是否包含某个 class //返回布尔值
4. toggle()：将某个 class 移入或移出当前元素。
5. item()：返回指定索引位置的 class //使用方法跟数组一样,item[0];item[1]等
6. toString()：将 class 的列表转为字符串。

##### innerHTML

与Node.innerText/textContent的区别:innerHTML会执行HTML标签

##### outerHTML

返回当前元素的所有HTML代码,包括自身和子元素

##### style

返回元素行内css

##### children,childElementCount

返回子元素数组
返回子元素个数

与Node.childNoes区别:它只包括元素节点,不包括其他节点,计数同理;

##### firstElementChild,lastElementChild

获取第一个子元素节点,返回最后一个子元素节点

##### nextElementSibling,previousElementSibling

#### 盒子相关属性

##### clientHeight,clientWidth (元素高宽减去滚动条不可见的部分)

1. Element.clientWidth;Element.clientWHeight表示元素节点的高度/宽度,只对块级元素生效,行内元素返回0;

2. document.documentElement的clientHeight属性，返回当前视口的高度（即浏览器窗口的高度），等同于window.innerHeight属性减去水平滚动条的高度（如果有的话）。document.body的高度则是网页的实际高度。一般来说，document.body.clientHeight大于document.documentElement.clientHeight.

##### clientLeft,clientTop

1. clientLeft属性等于元素节点左边框（left border）的宽度（单位像素），不包括左侧的padding和margin。如果没有设置左边框，或者是行内元素（display: inline），该属性返回0。该属性总是返回整数值，如果是小数，会四舍五入。

2. clientTop属性等于网页元素顶部边框的宽度（单位像素）

##### scrollHeight,scrollWidth (包括滚动条不可见的部分)

同clientHeight,clientWidth;但是包括滚动条外不可见的部分

##### scrollLeft,scrollTop

滚动条滚动的像素数

##### offsetParent

返回当前最靠近的元素

##### offsetHeight,offsetWidth

##### offsetLeft,offsetTop

##### scrollIntoView()

滚动当前元素
1. true:元素顶部与当前区域的可见部分的顶部对齐
2. false:元素的底部与当前区域的可见部分的尾部对齐

##### getBoundingClientRect()

返回一个对象，提供当前元素节点的大小、位置等信息，基本上就是 CSS 盒状模型的所有信息

具有以下属性:

    x：元素左上角相对于视口的横坐标
    y：元素左上角相对于视口的纵坐标
    height：元素高度
    width：元素宽度
    left：元素左上角相对于视口的横坐标，与x属性相等
    right：元素右边界相对于视口的横坐标（等于x + width）
    top：元素顶部相对于视口的纵坐标，与y属性相等
    bottom：元素底部相对于视口的纵坐标（等于y + height）

由于元素相对于视口（viewport）的位置，会随着页面滚动变化，因此表示位置的四个属性值，都不是固定不变的。如果想得到绝对位置，可以将left属性加上window.scrollX，top属性加上window.scrollY.

getBoundingClientRect方法的所有属性，都把边框（border属性）算作元素的一部分。也就是说，都是从边框外缘的各个点来计算。因此，width和height包括了元素本身 + padding + border

##### getClientRects()

返回二维伪数组,一维里面是当前元素的所有矩形,二维数组是每个矩形的bottom、height、left、right、top和width六个属性，表示它们相对于视口的四个坐标，以及本身的高度和宽度


获取同级下一个元素节点,返回同级上一个元素节点

#### Element接口的方法

#### 属性相关的操作

##### attributes 这是方法

返回元素所有的属性节点

##### getAttribute()

获取属性值

##### getAttributeNames()

获取该元素所有属性名,是一个数组

##### setAttribute()

设置当前节点属性,如存在则替换

##### hasAttribute()

该元素是否有某属性

##### hasAttributes()

该元素是否存在属性值

##### removeAttribute()

移除该元素指定属性

##### dataset  这是方法

自定义date属性
格式date-xxx="abc";
````bash
var article = document.getElementById('foo'); 
foo.dataset.columns // data-columns="3" 
foo.dataset.indexNumber // data-index-number="12314"
foo.dataset.parent //data-parent="cars"
````

##### querySelector() 

同document

##### querySelectorAll()

同document

##### getElementsByClassName()

同document

##### getElementsByTagName()

同document

##### closest()

接受一个 CSS 选择器作为参数，返回匹配该选择器的、最接近当前节点的一个祖先节点（包括当前节点本身）

##### matches()
是否匹配CSS选择器,返回布尔值

##### 事件相关方法

##### addEventListener()

添加事件的回调函数

##### removeEventListener()

移除事件监听函数

##### dispatchEvent()

触发事件

##### insertAdjacentElement(position, element)

在指定位置插入元素,成功返回true,失败返回false

position表示插入位置,其取值为

    beforebegin：当前元素之前
    afterbegin：当前元素内部的第一个子节点前面;
    beforeend：当前元素内部的最后一个子节点后面
    afterend：当前元素之后

element表示标签名

##### 

##### insertAdjacentHTML(position, text),insertAdjacentText(position, text)

在指定位置插入HTML字符串/插入字符串

position, text的值同上;

##### remove()

移除元素

##### focus(),blur()

focus()将当前页面的焦点，转移到指定元素上

blur()将焦点移除

document.activeElement属性可以得到当前获得焦点的元素

##### click()

模拟一次鼠标点击,相当于触发click事件





