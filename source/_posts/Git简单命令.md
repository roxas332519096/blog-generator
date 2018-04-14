---
title: Git简单命令
date: 2018-04-14 10:40:10
tags:
---

#### 1.更新文件到Github相关操作

##### 1.1初始化仓库
``` bash
git init
```

##### 1.2将添加文件放到缓存区
``` bash
git add 文件路径
```
查看缓存区文件
``` bash
git status
```

##### 1.3提交到git仓库

``` bash
git commit -m “提交信息”
```
##### 1.4 PULL
```bash 
git pull
```

##### 1.5 PUSH
```pash
git push
```
#### 2.对文件操作
进入文件夹

```bash
cd
```

查看当前目录

```bash
pwd
```

新建文件夹

```bash
mkdir 文件夹Name
```
新建文件

```bash
touch 文件Name.后缀
```

修改文件
```bash
echo "hi" > 1.txt
echo "hi" >> 1.txt
echo "hi" >! 1.txt
```

复制文件

```bash
cp -r
```

删除文件/文件夹
```bash
rm -rf
```
移动文件/重命名
```bash
mv 旧名字 新名字
mv 源路径 目标路径
```

查看目录

```bash
git ls
git ls -a
git ls -l
git ls -al
```

链接文件

```bash
git cat -file 路径
```
#### 3.查询git命令的网址
[explainshell.com](explainshell.com)

输入框输入所需命令，即可查阅命令的用途与包含的参数
