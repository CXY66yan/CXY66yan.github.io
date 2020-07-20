---
title: Postman操作步骤
date: 2020-04-21 18:51:17
tags:  [Postman1]
categories: Postman1
toc: true
---

[TOC]

## 基本功能介绍

### 教程：<https://www.jianshu.com/p/97ba64888894>

###1.如何新建请求

![首页](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200422_7.png)

```PYTHON
点击左上角的new和页面上方的加号可以新建请求；
history:所有请求过的URL都在里面；
collection:集合，可以新建集合，一般一个功能创建一个集合，集合里可以创建多个请求；
```

### 2.请求方式

```PYTHON
GET:查询数据
POST:增加数据
PUT:替换现有数据
PATCH:更新一些现有的数据字段
DELETE:删除现有数据
```

#### 请求参数

![参数](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200422_8.png)

```PYTHON
查询参数设置的两种方法：
1.在URL后面用？连接，参数以键值对的形式，多个参数之间用&连接
2.直接在Params中添加参数(点击Bulk Edit可以以文本的形式输入参数)
路径参数设置方法：直接在URL后面加上：参数名即可，可以对路径参数值进行编辑
```

### 请求body

![请求体](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200422_11.png)

```PYTHON
一般在post，put的请求方式中需要在body中添加数据,数据分为以下几种类型：
form_data:表格数据
urlencoded:网址编码
raw:原始数据可以选择数据类型:text，json,xml,html,js
binary:二进制数据，像图片，音频，视频等，也可输入文本文件
GraphQL: 在查询区域中输入您的代码，并在GraphQL变量部分中输入任何变量
```

### 请求头

![请求头](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200422_13.png)

```python
请求同种输入的参数接口文档swagger中会提示，边输入会边有提示；
点击Presets可将经常用到请求头类型添加都里面，下次直接点击就可以用了；
点击hidden，里面会有很多推荐的请求头参数，点击请求参数旁边的叹号，里面详细信息将指示在需要时如何禁用或覆盖球球头的值，如果禁用或覆盖推荐的请求头值可能会使您的请求行为异常
```

### 授权请求

![授权](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200423_14.png)

```PYTHON
#Authorization 授权请求，一些API要求您可以在Postman中发送的身份验证详细信息。身份验证涉及验证发送请求的客户端的身份，授权涉及验证客户端具有执行端点操作的权限。打开授权标签以配置您的访问详细信息。

单个请求的授权验证只需要点击Authorization选择下方的类型即可，对于集合的授权请求，鼠标放到集合上有三个点-edit-Authorization,该请求适用于整个集合中的请求

##授权请求有这几种类型可选：
1.Inherit auth from parent
2.No Auth：如果请求不需要授权时选择此项
3.API Key：API密钥，为了提高安全性，输入密钥名和值添加到请求头和查询参数中
4.Bearer Token:不记名令牌，在令牌字段中，输入您的API密钥值-或为了增加安全性，将其存储在变量中并按名称引用该变量
5.Basic Auth：基本认证，选择此类型，输入用户名和密码，为了安全，用户名可以用变量，之后在header-hide header中可以看到，Authorization将向API传递一个代表用户名和密码值的Base64编码的字符串；：
6.Digest Auth:摘要授权
7.OAuth 1.0
8.OAuth 2.0
9.Hawk Authentication
10.AWS Signature
11.NTLM Authentication[beta]
12.Akamail EdgeGrid
```

## 使用标签

```PYTHON
1.预览标签：集合中创建多个请求-点击其中一个/新建请求-此时请求方式是倾斜的，表示处于预览状态;
2.忙碌标签：点击集合中的某一个请求/新建请求-点击发送按钮，请求方式变正，表示处于忙碌状态;
3.未保存标签：点击集合中的某一个请求/新建请求-修改URL，点击发送之后，请求的最上方有一个小橙点，表示未保存;
4.标签冲突：如果在打开选项卡时基础请求本身发生更改，则邮递员中的选项卡将进入“冲突”状态。如果您已经修改了请求并将其保存在另一个选项卡中（可能在另一个工作区中），或者在您的选项卡仍处于打开状态时，团队中其他人正在处理同一请求，则可能会发生这种情况。
```

## 管理标签

![管理标签](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200423_23.png)

```PYTHON
1.打开和关闭标签：点击工作区的+和command+T
2.切换和重新排列标签:鼠标可以进行拖动和点击进行重新排列和切换
3.恢复标签：点击工作区右上角的三个点-Recently Closed-下拉列表中显示最近关闭的10个标签，点击即可恢复
4.复制标签：点击工作区右上角的三个点-Duplicate Current Tab即可复制
5.其他标签设置：
	总是在新标签页中打开请求：点击右上角一个小扳手-setting，把此选项改为ON即可
    关闭未保存的标签时总是询问：点击右上角一个小扳手-setting，把此选项改为ON即可
```

## history

![历史](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200423_24.png)

```python
历史中存放的是之前发出过的请求，可以进行以下操作：
1.浏览请求:电脑上下键浏览请求
2.查找请求:历史中的请求按照时间倒序排列，如果请求比较多的话可以直接在左上方的Filter中输入关键词进行快速搜索；
3.多选请求：按住CMD键（在Windows上为CTRL），然后单击要选择的每个请求。您可以通过列表顶部的操作来启动诸如保存，共享，文档编制，模拟，监视或删除请求之类的操作
```

## 变量

![变量](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200424_29.png)

```python
快速入门：点击眼睛按钮-点击Globals旁边的Edit,输入变量名和值，点击保存，在URL中输入https://postman-echo.com/get?var={{my_variable}}URL。将鼠标悬停在变量名称上，您将看到该值。
   
如果多个请求中具有相同的base_url，之后后面的参数或资源路径不同，则可以将base_url存到全局变量中，用的时候直接在url中用{{base_url}},见下图
```

![变量](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200424_31.png)

### 环境

```python
一般我们会有多个环境：本地环境，测试环境，开发环境，如何何止多个环境
1.点击右上角的眼睛，选择环境编辑，如下如，可以分享，复制，删除该环境
2.创建完环境之后可在下拉列表中进行选择
```

![环境](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200424_36.png)



## 变量

```python
变量的几种类型：
1.global:全局变量
设置：点击右上角的眼睛-编辑-global
2.collection：集合变量
设置：点击集合的...选择编辑-即可设置
3.environment：环境变量
设置：在对应环境下设置
4.data：来自外部CSV和JSON文件
5.local：本地变量也叫局部变量是临时的，局部变量值的范围仅限于单个请求或收集运行，并且在运行完成后不再可用。

注意：全局变量可以作用于所以集合，如果选择完对应的环境，则环境变量高于全局变量，设置完变量之后，只需要在引用的地方{{变量名即可}}
```

## 请求前的脚本设置和断言

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200426_47.png)

```PYTHON
Pre-request-Script:接口请求之前操作的脚本
一般情况下我们会用到get和set方法，如果想用更多的话可以直接点击上方的获取更多
Tests:主要做接口自动化的断言，在接口请求之后执行
    想要断言的值比较难获取：列表嵌套字典，字典嵌套字典或者想要在控制台看一下实际结果对不对，可以用：console.log(jsonData.value),控制台在左下角的第三个即可
```

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200429_1.png)

## 当上一个请求的结果需要作为下一个请求的参数使用时

1.在断言中设置一个环境变量(变量的值不需要家双引号)

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200501_18.png)

2.新建一个环境，将刚刚设置的键名放进去，不需要添加值保存，切换到刚刚设置的环境点击发送就可以看到值中自动填充了需要的值

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200501_22.png)



3.比如上一个接口获得的返回值是TOKEN，下一个接口请求的时候需要使用，需要先执行一下上一个接口再执行一下需要执行的接口

## 集合的运行

```PYTHON
方法：
1.点击左上方的Runner
2.点击左边的集合-三角型-run，见下图
```

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200429_2.png)

点击run test进入下面这个页面

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200429_3.png)



## Postman数据驱动

```PYTHON
#一个请求中不一定只有一组数据没可能有多组数据，这时我们可以从外部导入数据,注意：
1.文件必须是CSV或json格式的文件
可以先在Excel中创建数据另存为CSV格式，然后用Notepad++等文本编辑器把编码格式改为utf-8；
文件的第一行为变量名，下方为变量名对应的值；
2.请求参数中的值：{{文件中的变量名}}
3.在测试沙箱中(tests中)参数的获取，使用data.文件中的参数名
4，运行时，如果进行数据驱动，导入数据之后，应先Preview一下，看数据是否正常显示再运行
```

## 如何安装Postman Interceptor？

```python
1.打开谷歌浏览器在左上角有一个应用，点击进入应用商店中搜索Postman Interceptor，点击下载or在谷歌浏览器下载一个谷歌访问助手，在访问助手的应用商店中搜索Postman Interceptor，点击下载

2. 然后就可以看到浏览器右上角的postman interceptor 工具图标
3.打开postman，点击右上角的第二个图标，如下图：即可添加域名，访问该域名时即可自动添加cookies
```

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Postman/Snip20200503_24.png)

