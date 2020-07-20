---
title: linux命令
date: 2019-08-25 20:30:42
tags:  [操作系统,linux,测试]
categories: linux
toc: true
---

[TOC]

#操作系统及其分类

####操作系统

负责协调硬件设备和软件资源的系统软件

#####桌面操作系统

windows界面化

macOS

Linux

#####服务器操作系统

Linux （安全 稳定 免费）

Windows  server （付费）

#####嵌入式操作系统

Linux

##### 移动设备操作系统

Android

iOS

# Linux版本

##### Linux内核版本

稳定版

发行版

##### Linux发行版本

Ubuntu

Centos

Redhat

#### Linux和Windows的区别

windows通过盘符（C/D/E盘）管理文件和目录而Linux没有盘符的概念，所有的文件和目录都在根目录下（/）

# Linux命令大全

##Linux常用的几个基本命令

```python
ls 查看文件夹下的内容
ls -a :显示所有文件包含隐藏文件
ls  -l :显示文件的所有详细信息
ls -lh :人性化显示文件大小
ls -alh :查看某个文件下的所有文件包含隐藏文件并显示文件的详细信息，文件大小人性化显示

ls与通配符一起使用

ls *.txt :匹配任意字符任意次
ls ?.txt ：只匹配一个字符
ls [abc]/[a-f].py ：匹配[]中任意字符相匹的文件名
ls [abc]*.py :匹配以[]中字符开头的文件名

cd :切换到家目录
cd ~ : 切换到家目录
cd . :切换到当前目录
cd .. :切换到上一级目录
cd - :返回上一次所在的目录 

touch 创建文件(eg1:touch 1.txt；eg2:touch 1.txt 2.txt 3.txt)
解释：如果文件不存在创建一个新文件，如果文件存在修改文件的修改时间

mkdir 创建文件夹
mkdir file_name创建一个目录
mkdir {file_name1 file_name2 file_name3}一次创建多个目录
mkdir -p a/b/c 递归创建多级目录
    
rm 删除文件(eg:rm 1.txt)
rm -r ：删除目录及目录下的所有内容
rm -i ：交互式删除，删除时会弹出是否确认删除弹窗
rm -f ：强制删除文件或目录
rm -r 删除目录(rm -r file_name)

clear 清屏
pwd 查看自己在哪
quit() 退出终端

```

#### Linux终端命令格式

命令  [-选项][参数]

[]代表可有可无

####终端中如何查阅帮助信息

-help or man

##Liunx的其他命令

```python
cp 命令：复制文件/目录
mv 命令：删除文件/目录

查看文件内容
cat 文件名：查看⽂文件内容、⽂文件合并、追加⽂文件内容等
more 文件名：分屏显示⽂文件内容
grep 搜索文本文件名：搜索文本文件内容
grep -v  文件名: 反向显现内容
grep -n 文件名: 显示行号
grep -i  文件名:忽略略⼤小写
   
>/>> ：重定向
| ：管道 

find -name "文件名"：查找文件并显示文件的路径信息
ln -s [绝对路路径]源⽂文件 链接⽂文件：创建软链接
ln 源⽂文件 链接⽂文件：创建硬链接
```

### 打包压缩解压的命令

```
tar -zcvf 包名.tar.gz 被打包的⽂文件 作用:打包和压缩
tar -zxvf 包名.tar.gz 作用:解包和解压缩
tar -zxvf 包名.tar.gz -C /home/admin/桌⾯面/tar 作⽤用:包⾥里里 ⾯面的内容解包解压到 tar⽬目录下
（-c : 打包；-v: 显示进度；-f: 指定包名，必须放在最后 ；-t: 查看包内容；-x: 解包）
zip2(two) :压缩 解压缩 
zip ：压缩
unzip ：解压缩
```

### 修改文件权限的命令

```
chmod:修改文件权限
chmod 命令-字母法
chmod u+rw filename 给⽤用户增加权限
chmod g-rw filename 给组⽤用户减少权限
chmod a=x filename 给所有⽤用户设置执⾏行行权限，去掉了了原 有权限
chmod u+rw,g+rw,o+rw filenmae 给三个⽤用户类型增加 读写权限，注意,号分割⽤用户类型
chmod 命令-数字法
chmod 755 文件名(u/g/o=用户/组/其他，r/w/x分别为4/2/1)
```

### 如何从普通用户改为管理员用户

```PYTHON
普通用户，标志是一个$符号
管理员用户，标志是一个#符号
终端中输入： sudo su 然后输入管理员用户的密码（输入密码的时候是不可见的）
然后你就切换到#状态了
```

### 需要管理员权限的命令

```
which ：查找程序的安装位置
su:切换用户
exit：退出当前登录帐号
who:查看当前操作系统的⽤用户信息
reboot :重启 
shutdown:关机(需要root权限) 
ps -aux:显示当前系统的所有进程
ps -aux | grep "进程名":查看某个进程
kill：杀死进程 （kill 进程id）
top:动态查看系统资源
netstat -anptu | grep "进程名"：查看某个端口信息
```



### 查看日志信息的命令

```
head :查看文件前10行内容,如果想查看其他行数就指定一个数字
head 文件名
head -15 ⽂件名
tail:查看文件结尾n行内容
tail 文件名:⼯作中查看⽇志⽂件，查看内容较多的文件结尾几行内容 
tail -f 文件名 :实时监控⽇志文件,⽅便定位bug
ping 127.0.0.1 > 文件名 ：使⽤用ping命令不停向⽂件中写入内容
```

###ls -l 的扩展

ls -l 可以查看⽂文件夹下⽂文件的详细信息，从左到右依次是:
**权限**第1个字符如果是 d 表示⽬目录，如果是 - 表示⽂文件 权限类型:rw- 

**硬连接数**通俗地讲，就是有多少种⽅方式，可以访问到当前 ⽬目录或⽂文件

**拥有者**家⽬目录下 ⽂文件或⽬目录 的拥有者通常都是当前⽤用户 

**组**在linux中，很多时候，会出现组名和⽤用户名相同的情况 ⼤大⼩小
**时间**
**文件名**
    

