---
title: Jmeter
date: 2020-03-15 11:20:25
tags:  [Jmeter]
categories: 功能测试
toc: true
---

[TOC]

### Jmeter简介

```PYTHON

	1.1 概念：由Apatch组织使用Java语言开发的一款测试工具
	1.2 作用：
		1. 接口测试
		2. 性能测试
		3. 压力测试
		4. 数据库测试
		5. web测试
		6. Java程序测试
	1.3 优点：
		1. 开源、免费
		2. 跨平台
		3. 小巧
		4. 支持多协议
		5. 功能强大
	1.4 缺点：
		1. 不支持IP欺骗（只有性能测试使用）
		2. 不支持JS和Web自动化Ui操作
```

### Jmeter环境搭建，安装和启动

```PYTHON
# 环境搭建
	1.安装JDK或JRE
		JDK:Java SE Development Kit ,JAVA语言开发工具包+JRE（JAVA程序运行环境）【推荐】
		JRE：Java Runtime Environment ,JAVA程序运行环境(由JAVA语言开发的程序，必须使用JRE去解释，计算机才能识别和执行)
        ##打开终端输入java回车，如果没有安装会弹出提示让你去下载，或直接在百度搜索JDK安装，有很多教程，安装路径可以自定义但不要出现空格和中文，安装完之后在终端中输入java -version 可以看到版本号
        
		
	2.Jmeter环境：
		 a.Jmeter下载地址：https://jmeter.apache.org/download_jmeter.cgi
			版本：1. Binaries(二进制运行程序)【推荐】(zip是Windows电脑)
				 2. Source(源码，需要先编译才能运行)
        Mac电脑下载完成后需要双击解压
        b.安装
			1、打开终端，进入解压完成目录的bin目录
            2、输入启动命令：sh jmeter 若启动成功，客户端自动弹出弹框
        ##Jmeter安装完之后需要修改一下环境变量		
		搭建环境：
        新建  变量名：JMETER_HOME
			 变量值：Jmeter安装目录 (bin目录之前Jmeter的安装路径) 
        编辑：如果有CLASSPATH这个变量名的话直接在该变量值后面复制 .;%JMETER_HOME%\lib\ext\ApacheJMeter_core.jar;%JMETER_HOME%\lib\jorphan.jar;%JMETER_HOME%\lib\logkit-2.0.jar;如果没有该变量名需要新建一个CLASSPATH变量名，对应的值：.;%JMETER_HOME%\lib\ext\ApacheJMeter_core.jar;%JMETER_HOME%\lib\jorphan.jar;%JMETER_HOME%\lib\logkit-2.0.jar;
			
	3.Jmeter目录介绍
		bin: 存放（可以执行文件，如：启动jmeter程序）
			启动方式：
				1. ApacheJMeter.jar(.jar为java的可以执行程序的相当于Windows的可执行程序.exe)【推荐】
				2. jmeter.bat（windows版可执行文件）
                3.jmeter.sh(mac可执行文件)
		docs\api：存放jmeter开发说明文档
		printable_docs：jmeter操作手册
		lib:外部jar包或工具存放地
```

### mac电脑如何汉化Jmeter

```python
打开Jmeter-options-language-chinese simple
```



## Jmeter基本功能介绍

### 元件与组件概念

```PYTHON
组件：单个功能点实现
元件：类似功能组件组合在一起，叫做元件；
```

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200505_25.png)

### 进程与线程

```PYTHON
进程：正在运行的程序
线程：是进程中的执行线索(比如启动QQ可以同时跟三个人聊天，一个进程中有三个线程)
线程组：进程中有许多线程，为了方便管理，可以对线程按照性质进行分组，分组的结果就是线程组

三者之间的关系：一个进程可以包含多个线程组，一个线程组可以包含多个线程；(见下图)

```

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_67.png)

```python
线程执行顺序：
	1. 默认无论是单线程/多线程多个线程组都是并行执行；（单个线程组中有多个取样器，取样器是根据顺序执行）
	2. 修改多个线程组根据顺序执行如何操作？
		解决：勾选 测试计划->独立运行每个线程组 选项(见下图)
```

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_68.png)

```python
线程属性：
		1. 线程数：理解为人数
		2. Ramp-Up时间：启动线程数所需要的总时间
		3. 循环次数：指定次数或勾选永远（注意：配合调度器使用， 不使用调度成死循环）
		4. 调度器：（勾选调度器）
			持续时间：脚本要运行多久（当前线程组中的请求）
			启动延迟：启动后延迟多少秒运行请求
		5. 延迟创建线程直到需要：（建议勾选：节省客户端性能资源）
```

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_69.png)

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_70.png)









## 练习

```PYTHON
1. 学院新增：
		步骤：
			1. 基于测试计划-》线程组
			2. 基于线程组-》添加HTTP请求
			3. 基于测试计划-》添加察看结果树
			4. 基于测试计划-》添加 HTTP信息头管理器（Content-Type:application/json）【重点】（作用：告诉服务器，请求参数类型为json）
		操作：
			1. HTTP请求：
				1). 协议：为空默认http
				2). IP/服务器名：必须只设置ip地址，不能含协议或端口或路径
				3). 端口：默认为80，如果非80，必须设置；
				4). path：资源路径，根据访问的资源实情来写；
				5). 编码：必须指定utf-8，如果不指定，新增数据，在数据库中乱码
			2. 察看结果树：察看请求和响应内容
	2. 学院更新
		三要素：
			1. url+请求方法
			2. 请求参数数据
			3. 响应数据+响应状态码 (200/201+更新后的实体数据)
	3. 查询
		1. 请求url+GET
		2. 响应：200+符合条件的指定数据；
	4. 删除
		1. 请求url+DELETE
		2. 响应：204+空数据
		
```

## 参数化

```PYTHON

	3.1 用定义变量：
		1). 组件方式->..->配置元件->用户定义的变量
		2). 测试计划 -->用户定义的变量 【全局】
		作用：设置变量名和值
		引用：${变量}
	
	3.2 CSV数据设置文件（组件）【重点】
		作用：读取外部的数据存储文件到脚本中（TXT）
		位置：配置元件->CSV数据设置文件
		配置：
			1). 文件名：参数化读取文件路径，推荐使用相对路径（./xxx；注意：参数数据文件和脚本文件要在同一目录）
			2). 文件编码：UTF-8
			3). 变量名：设置接收读取参数化文件的参数值的名称
				注意：
					1. 变量名必须要和接收的数据位置对应。
					2. 变量名的个数要和数据个数相同
			4). 以指定符号分隔字符串，默认逗号
		如何批量运行多条数据？
			方式1. 将线程组循环次数改成数据文件的总行数（静态解决）
			方法2. 首先 将线程组循环次数改成永远，
				   其次 将CSV数据文件设置：遇到文件结束符再次循环？：Fasle；
				   最后 遇到文件结束符停止线程：True
			
	3.3 用户参数
		作用：支持多线程读取不同的测试数据；
		位置：前置处理器->用户参数
		引用：${变量名}，只能引用名称（相当于参数名，而用户相当于：每个用户单独一组数据）
	3.4 函数：
		1). 计数函数
			 True: 每个用户自己单独计数
			 FALSE:全局计数
		2). 随机函数
			设置最小到最大数值，随机生成；
		3). 时间函数
			1). 参数为空，生成1970年到现在的毫秒数
			2). 设置年月日时分秒
				YMD = yyyyMMdd
				HMS = HHmmss
				YMDHMS = yyyyMMdd-HHmmss
科普：
	环境变量path作用：
		说明：就是如果系统在当前目录下找不到要执行的文件，那么就取path变量中设置的路径去找。
		
	设置编码格式：
		1. 打开jmeter.properties文件（bin目录下）
		2. 搜索：sampleresult.default.encoding=utf-8
	
```

## Jmeter基本使用流程

1.启动Jmeter
2.基于测试计划添加线程组，基于线程组添加HTTP请求

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_60.png)

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_61.png)

注：脚本编写过程中养成Ctrl+S保存的习惯



![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_62.png)

3.基于测试计划添加查看结果树

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_63.png)

4.运行并查看结果

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_64.png)

5.新增和修改提交的数据是Json格式，需声明提交的数据文件类型

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_71.png)

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_72.png)

6.当不同的请求使用相同的协议，端口号，域名和编码格式时，可以使http请求默认值实现被复用的字段

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_73.png)

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Jmeter/Snip20200524_75.png)

