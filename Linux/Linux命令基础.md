# Linux基础

[TOC]

## 1 ls命令

| 命令 | 说明 |
| :--: | :--: |
|`ls`|显示当前目录下所有的非隐藏文件|
|`ls -a`|显示当前目录下所有文件，包含隐藏文件|
|`ls -l`|显示当前目录下所有的非隐藏文件的详情|
|`ls -al`|显示当前目录下所有文件，包含隐藏文件 的详情|
|`ls -lh`|以列表形式显示当前目录下所有的非隐藏文件的大小(K  M  T)|
|`ls -alh`|以列表形式显示所有文件，包含隐藏文件的文件大小(K M T)|

## 2 pwd命令

用来显示当前路径

## 3 mkdir命令

| 命令 | 说明 |
| :--: | :--: |
|`mkdir -p 111/222/333`|一次创建多级文件夹|
|`mkdir /root/mydemo`|使用绝对路径来创建|
|`mkdir mydemo2`|使用相对对路径来创建|

## 4 rm命令

用于删除文件或目录

| 命令 | 说明 |
| :--: | :--: |
|`rm a.txt`|删除时，会给出提醒确认，输入y删除，n不删除|
|`rm -f b.txt`|强制删除 等价于 rm -f /root/b.txt|
|`rm a.java b.java c.java`|一次可以删除多个文件|
|`rm -rf *.java`|可以删除当前目录下的所有.java文件|
|`rm * -rf`|删除当前目录的所有内容|

## 5 cd命令
   cd 命令可以进入一个目录

| 命令 | 说明 |
| :--: | :--: |
|`cd`|直接cd 可以从任何一个目录回到/root目录|
|`cd /root`|进入root目录|
|`cd ..`|回到上一级目录|
|`cd ../..`|回到上上一级目录|
|`cd -`|可以在最近的两次目录之间切换|

## 6 touch命令

用于在当前路径创建一个空文件，也可以加上绝对路径在对应的位置创建

## 7 mv命令

常用于移动和重命名文件

## 8 cat命令

常用于显示文件内容

## 9 cp命令

| 命令 | 说明 |
| :--: | :--: |
|`cp user.txt user2.txt`|在当前位置创建一个user.txt副本，名称为user2.txt|
|`cp user.txt /home/`|将当前目录的user.txt 复制到/home目录，文件名保持不变|
|`cp user.txt /home/user2.txt`|将当前目录的user.txt 复制到/home目录，文件名改为user2.txt|
|`cp /home/b.txt ./`|将指定目录里的文件复制到当前目录(.后边的/可以去掉)|

## 10 压缩与解压缩

### zip

压缩：将test目录压缩为test.zip

```bash
zip -r test.zip test
```

解压：将test.zip解压为到test2

```bash
unzip test.zip -d test2
```

### tar.gz

压缩：将test目录压缩为test.tar.gz

```bash
 tar -cvzf  test.tar.gz test
```

解压：将test.tar.gz解压为到test

```bash
tar -xvzf test.tar.gz
```

## 11 find命令

查找文件

## 12 grep命令

查找文件内容

```bash
grep hello HelloWorld.java
```

## 13 ps命令

常用方式 `ps -ef`

## 14 kill命令

`kill -9 <pid>`

## 15 useradd和userdel

### 添加用户

useradd admin

### 删除用户

userdel -r admin

### 修改用户密码

passwd admin