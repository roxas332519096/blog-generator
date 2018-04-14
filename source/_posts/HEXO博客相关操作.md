---
title: HEXO博客相关操作
date: 2018-04-14 09:58:04
tags:
---


## 1.发布新的博客

git bash 输入以下命令：

``` bash
$ hexo new "标题"
$ start C:\Users\Administrator\desktop\myBlog\source\_posts\标题.md
$ hexo generate
$ hexo deploy
```

## 2.更改博客主题

[主题合集](https://github.com/hexojs/hexo/wiki/Themes)

### 例子：
假如找的是https://github.com/iissnan/hexo-theme-next
输入：
``` bash
cd themes
git clone git@github.com:iissnan/hexo-theme-next.git
cd ..
```
_config.yml 的第 75 行改为 theme: hexo-theme-next，保存
 ``` bash
hexo generate
hexo deploy
 ```

 ## 3.布局相关操作

#### 3.1引入代码块
``` bash
{% codeblock [title] [lang:language] [url] [link text] %}
Hello World
{% endcodeblock %}
```
##### 或:

{% codeblock %}
`` ` bash   \\去掉中间空格
Hello World
`` `        \\去掉中间空格
{% endcodeblock %}

#### 3.2图片

``` bash
{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}
```

#### 3.3链接

``` bash
{% link text url [external] [title] %}
```
##### 或:

```bash
[title](link)
```



