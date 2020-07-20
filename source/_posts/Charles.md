---
title:  Charles
date:  2019-08-27 17:08:05
tags:  [Charles,http,https,激活,打断点]
categories: charles
toc: true
---
#  charles 浏览器和手机抓包
@(charles)[http|https]
[TOC]
##http手机抓包操作步骤

```python
打开Charles，点击proxy-点击Mac OS x proxy取消前面的对勾，对勾保存是电脑抓包-点击proxy setting-在enable transparent http proxy 前面打对勾然后点击ok-点击设置保证跟电脑连接的是同一个局域网点击链接的wifi-选择手动-输入服务器的IP（安装了Charles的电脑的IP地址，可在Charles-help-local IP adress中查看）和端口号-点击Charles（⭕️）开始录制按钮，手机这边操作就可以开始抓包了；
```

##Charles Android/ios手机抓https协议

博客地址：<https://juejin.im/post/5a1033d2f265da431f4aa81f>

```python
1.电脑端打开Charles-help-ssl proxying-install Charles root certificate
2.下载安装证书，默认路径不需要更改，在钥匙串访问中选择证书双击证书文件-选择始始终信任
3.电脑端打开Charles-help-ssl proxying-install Charles root certificate on a mobile  device or remote browers-下载安装证书，默认路径不需要更改，在钥匙串访问中选择证书双击证书文件-选择始始终信任
4.设置手机代理,要抓包的手机与电脑在同一个局域网下（链接同一个Wi-Fi即可），打开手机设置-选择已经连接的Wi-Fi-手动代理-输入安装charles电脑的IP（charles-help-localip address）和端口号（proxy-proxy setting-proxies）
5.手机在浏览器中输入：chls.pro/ssl
6.手机弹出提示：安装配置描述文件，选择允许，即可

```

## Charles过滤

```python
方法一：打开Charles，页面左下方有一个filters，在里面输入自己想要过滤的内容部分即可

方法二：菜单栏选择 “Proxy”->”Recording Settings”，在弹出的窗口中选择 Include 栏，再点击“Add”，在弹出的窗口中输入需要监控的协议，主机地址，端口号等信息，来添加一个项目。

方法三：在想过滤的网络请求上右击，选择 “Focus”，之后在 Filter 一栏勾选上 Focussed 一项

```

##Charles模拟弱网测试

1.proxy-start Throtting ,点击完之后小乌龟变亮；

2.proxy-Throttle Setting如下图所示：

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Charles/Snip20200521_51.png)



3.点击Throttle Setting进入以下页面：

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Charles/Snip20200521_53.png)

配置参数解析：
bandwidth —— 带宽，即上行、下行数据传输速度
utilisation —— 带宽可用率，大部分modern是100%
round-trip latency —— 第一个请求的时延，单位是ms。
MTU —— 最大传输单元，即TCP包的最大size，可以更真实模拟TCP层，每次传输的分包情况。
Releability —— 指连接的可靠性。这里指的是10kb的可靠率。用于模拟网络不稳定。
Stability —— 连接稳定性，也会影响带宽可用性。用于模拟移动网络，移动网络连接一般不可靠。

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Charles/Snip20200521_54.png)



##charles如何打断点，修改response数据

```python
1.打开将要访问的网址，通过Charles抓到想要修改数据的接口,双击接口连接勾选Breakpoints
```

```python
2.点击Charles-proxy-Breakpoints settings
```

```python
3.进入breakpoint settings页面,设置完成之后，点击ok
```

```python
4.重新访问该接口，charles自动跳转到breakpoints页面
```

```pytho
5.此时修改Response数据，点击Edit Response，切换底部tab至Text，修改所需要的数据
```

```pytho
6.修改数据后，点击Execute，查看访问的页面，数据将会显示已修改的Response数据
```

### Charles设置断点

1.选择要设置断点的接口

2.右键选择 Breakpoints

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Charles/Snip20200519_27.png)





3.断点的相关配置， Proxy ——>Breakpoint Settings

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Charles/Snip20200519_28.png)

4.双击刚刚已经设置的断点接口，进行设置

1.把参数删掉，写*

2.勾选请求，可修改请求

3.勾选返回，可修改返回



![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Charles/Snip20200519_32.png)

5.点击ok, 客户端再重新请求一下接口， 当跑到设置断点的接口时，网页会暂停，这个时候Charles进入breakpoints 

![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Charles/Snip20200519_31.png)

6. 点击Edit Request 修改请求参数。这里根据你要测试的数据来修改,修改好参数后，点击Execute （执行）。 另外 Abort （中止）， Cancel （取消）

   ![](/Users/qingclass/Desktop/CXY66yan.github.io/CxyBlogs/source/_posts/Charles/Snip20200519_33.png)

7.点击执行后，来到返回的页面，这个时候在Charles可以查看返回的数据。也可以对其进行修改，好了之后 点击 Execute 

8.这个时候页面就可以执行完成啦，可以看到 修改过后的请求返回是什么效果，达到测试的目的。

在请求上：即从应用程序发送请求之后，但后端接收到请求之前
在响应上：即在后端发送响应之后但在响应之前


##Charles的破解方法：

**1.修改charles.jar文件或者替换掉原来的软件。**
从官网上下载Charles，安装完毕，需要点击运行一起，command + q 彻底退出一次
在命令行终端输入 sudo spctl --master-disable 信任任何来源 （避免软件提示破损问题）
在命令行终端输入 open /Applications/Charles.app/Contents/Java/ 打开并替换 charles.jar（最好备份一下源文件, 我修改源文件名charles.jar.bak）
替换完成后，在此打开charles软件
替换 charles.jar的文件的下载地址
百度云：链接:https://pan.baidu.com/s/1_-Qsq_BzpQiqCStaD8XjUQ 密码:vsgq
**2.注册码**
按照常规安装好charles软件之后，打开软件，点击工具栏中的help --> register
输入如下信息： 
Registered Name: https://zhile.io
License Key: 48891cf209c6d32bf4
使用Charles进行手机抓包（iOS）
**注意：对某个手机进行抓包的时候，该手机的安全证书必须是跟该电脑连接同一个Wi-Fi安装的**

###IOS上安装安全证书：（iOS-iphonex）

```python

1.在浏览器中输入http://chls.pro/ssl

2.设置-通用描述文件-点击安装

3.设置-通用-关于本机-证书信任设置点击开启

```




###Android上安装安全证书：（android-vivox27）

```python

如何将之前的安全证书删除：

设置-安全与隐私更多安全设置-用户凭据-点击证书-删除

重新安装证书：

1.电脑和手机连接同一个网络，打开Charles,Help -> SSL Proxying -> Save Charles Root Certificate...，将这个保存到桌面（只要记住在哪里即可），选择哪个格式的都可以，命名为1.cer

2.将1.cer文件发送到Android手机上,进入手机设置，点击“安全和隐私----更多安全设置->从存储设备安装->Download->.crt文件->确定”，在弹出窗，对证书命名为：Charles，点击确定（首次安装证书会让输入锁屏密码）。至此证书安装成功！立即在电脑端对手机网络进行抓包吧！
上述步骤不同厂商的手机还是稍微有些区别的
在Android手机上找到1.cer文件，打开手机的密码，然后重新命名1.cer文件即可。
```

## 荣耀10青春版如何设置代理

```python
1.连上需要连接的网络，长按网络几秒会弹出选项，选择修改网络；
2.勾选显示高级选项，将【IP设置】改成【静止】
3.点击代理选择手动
```



####Charles中一个手机可以在不同网段下安装多个证书

#####charles抓包iOS手机报服务器开小差？

```python
电脑和手机连接同一个网段，电脑上点击help-安装证书到手机-OK-手机浏览器中输入chls.pro/ssl-下载-设置-通用-描述文件-安装-设置-通用-关于本机-证书信任设置-开启即可
```

## 手机连上网络但显示没网

```python
1.检查手机的代理有没有打开，如果代理开着需要把代理关了看一下
```

