---
title: Web自动化测试
date: 2020-01-22 18:51:28
tags:  [web,自动化测试]
categories: 自动化测试
toc: true
---

[TOC]

## Web自动化测试环境的安装

1.安装Pycharm；

2.安装selenium；

3.安装浏览器（goole/firefox）;

4.安装浏览器驱动

goole驱动的下载地址：

火狐驱动的下载地址：https://github.com/mozilla/geckodriver/releases（插件：chropath）

谷歌驱动的下砸地址：https://sites.goole.com/a/chromium.org/chromedriver/downloads(不同的浏览器版本需要下载对应的驱动版本)

## 什么样的项目适合自动化？

```PYTHON
需求变更不频繁，项目周期长，项目需要回归测试
```

##web元素定位的8种方法

```
id是唯一的
name属性是可以重复的
class_name可以重复，取得=的时元素的class属性，如果有多个只能取其中一个
用某个方法时前提时该元素有这个属性，没有不能用
tag_name利用标签名定位，一个页面会有多个标签相同的标签，只能用于模糊定位，很少用
link_text专门用于定位超链接的（<a>标签<a>），通过超链接中的全部文本内容来定位元素
partial_link_text也是专门用于定位超链接的（<a>标签<a>），可以通过超链接中的全部/部分文本内容定位元素
xpath
(1.路径定位：相对路径/绝对路径；绝对路径很少用，一般用相对路径，相对路径以//*：任意层级任意标签
2.利用元素属性：//*[@属性名=属性值]；属性与逻辑结合//*[@属性名1=属性值1 and @属性名2=属性值2]
3.层级和属性结合：通过该元素很难定位到，可以通过先找到其父级再找到该元素//*[@属性名=属性值]/标签名）
css_selector
id选择器：#id属性值
class选择器：.class属性值
元素选择器：根据元素的标签名选择
属性选择器：[属性名=属性值]
层级选择器：先找到其父级再找到其子级
element1 > element2; element1  element2

find_elements_by_xxx()定位一组元素
```

代码如下：

```python
#导包
from selenium import webdriver
from time import sleep
#初始化浏览器对象
driver=webdriver.Chrome()
#打开百度网页
driver.get("http://www.baidu.com")
#input_box=driver.find_element_by_id('kw')
#input_box.send_keys("手机")
#driver.find_element_by_name('tj_trhao123').click()
#driver.find_element_by_class_name('bri').click()
#driver.find_element_by_link_text('新闻').click()
#睡2秒
sleep(2)
#退出浏览器
driver.quit()
```

## 常用操作元素的方法

```python
click():单击

send_keys():模拟输入

clear():清除文本

```

## 常用操作浏览器的方法

```python
maximize_window()                 最大化浏览器窗口
set_window_size(width,height)     设置浏览器窗口的大小
set_window_position(x,y)          设置浏览器窗口的位置
back()                            后退-模拟浏览器的后腿操作
forword()                         前进-模拟浏览器的前进操作
refresh()                         刷新-模拟浏览器的刷新操作
close()                           关闭当前浏览器窗口
quit()                            关闭浏览器驱动对象
title                             获取页面标题
current_url                       获取当前的url
```

代码如下：

```python
#导包
from selenium import webdriver
from time import sleep
#初始化浏览器对象
driver=webdriver.Chrome()
#打开百度网页
driver.get("http://www.baidu.com")
driver.find_element_by_link_text('新闻').click()
sleep(1)

#driver.maximize_window()
#driver.minimize_window()
#driver.set_window_size(100,100)
#driver.set_window_position(1000,500)
#driver.back()
#driver.forword()
#print(driver.title)
#print(driver.current_url)
#睡2秒
sleep(1)
#退出浏览器
#driver.close()
driver.quit()
```

## 常用获取元素信息的方法

```python
size                     返回元素的大小
text                     获取元素的文本内容(超链接上的文本内容)
get_attribute("xxx")     获取元素的属性值，括号中传的为属性名
is_displayed             判断元素是否可见
is_enabled               判断元素是否可用
is_selected              判断元素是否被选中，用来检查复选框或单选框是否被选中

```

代码见下：

```python
#导包
from selenium import webdriver
from time import sleep
#初始化浏览器对象
driver=webdriver.Chrome()
#打开百度网页
driver.get("http://www.baidu.com")
sleep(1)
#elemen1t=driver.find_element_by_id('kw')
#print(element1.size)
#element2=driver.find_element_by_id('su')
#print(element2.text)
#print(driver.find_element_by_link_text('新闻').text)
#print(driver.find_element_by_link_text('新闻').size)
#print(driver.find_element_by_id("su").get_attribute("id"))
#print(driver.find_element_by_id('su').is_displayed())
#print(driver.find_element_by_id('su').is_enabled())
print(driver.find_element_by_id('su').is_selected())
#睡2秒
sleep(1)
#退出浏览器

driver.quit()
```

##常用鼠标操作的方法

```python
在selenium中将鼠标的操作方法封装在ActionChains类中
实例化对象：action=ActionChains（driver）
context_click(element)              右击-模拟鼠标的右击操作
double_click(element)               双击-模拟鼠标的双击操作
drag and drop (source,target)       拖动-模拟鼠标的拖动效果
move to element(element)            悬停
perform                             执行，此方法用于执行以上所有鼠标操作
```

代码见下：

```python
#导包
from selenium import webdriver
from time import sleep

from selenium.webdriver import ActionChains


#初始化浏览器对象
driver=webdriver.Chrome()
#打开百度网页
driver.get("http://www.baidu.com")
sleep(1)

#实例化ActionChains对象
action=ActionChains(driver)
#定位元素
element=driver.find_element_by_id('xxx')
#调用右击的方法
action.context_click(element)
#执行
action.perform()

#action.context_click(element).perform()
#睡2秒
sleep(1)
#退出浏览器

driver.quit()
```

##常用键盘操作方法

```python
selenium中将键盘的操作方法都封装在Keys类中
send_keys(Keys.BACK_SPACE)             删除键
```

代码见下：

```python
#导包
from selenium import webdriver
from time import sleep

from selenium.webdriver.common.keys import Keys
#初始化浏览器对象
driver=webdriver.Chrome()
#打开百度网页
driver.get("http://www.baidu.com")
sleep(1)
#定位元素
element=driver.find_element_by_id('kw')
element.send_keys('福')
sleep(1)
#删除键
element.send_keys(Keys.BACK_SPACE)
#空格键
element.send_keys(Keys.SPACE)
#制表键
element.send_keys(Keys.TAB)
#回退键
element.send_keys(Keys.ESCAPE)
#回车键
element.send_keys(Keys.ENTER)
#复制键
element.send_keys(Keys.CONTROL,'c')
#粘贴键
element.send_keys(Keys.CONTROL,'v')
#全选键
element.send_keys(Keys.CONTROL,'a')
sleep(1)
element.send_keys('到了')
#睡2秒
sleep(1)
#退出浏览器

driver.quit()
```

##元素等待

#### 显式等待

```python
定位元素时如果能定位到元素则直接返回该元素，不触发等待，如果定位不到该元素，则过一段时间再去定位，如果在达到最大时长还没有找到该元素，则抛出超时异常TimeoutException
```

代码如下：

```
#step1：selenium中把显示等待的相关方法封装在WebDriverWait类中
from selenium.webdriver.support.wait import WebDriverWait
#初始化浏览器对象
driver=webdriver.Chrome()
#step2 poll_frequency,检测间隔时间，默认0.5s
WebDriverWait(driver,timeout,poll_frequency=0.5)
"""step3调用方法until(method)直到...才；method函数名称，该函数用来实现对元素的定位，一般用匿名函数来实现:
lambda x: x.driver.find_element_by_id('id')"""
#step4
element=WebDriverWait(driver,3,1).until(lambda x: x.find_element_by_id('id'))
显示等待作用于元素
```



#### 隐式等待

```PY
定位元素时如果能定位到元素则直接返回该元素，不触发等待，如果定位不到该元素，则过一段时间再去定位，如果在达到最大时长还没有找到该元素，则抛出元素不存在的异常NoSuchElementException
```

代码如下：

```PYTHON
driver.implicitly_wait(timeout)
timeout为等待最大时长，单位：秒；
隐式等待为全局设置，只需要设置一次，就作用于全部元素
```

##下拉选择框的操作

```PYTHON
Select类是selenium为操作select标签特殊封装的
实例化对象：
select=Select(element)；element，<select>标签对应的元素，通过元素定位方式获取
```

方法：

```PYTHON
select_by_index(index)                  根据option索引来定位，索引从0开始
select_by_value(value)                  根据option属性value值来定位
select_by_visible_text(text)            根据option显示文本来定位
```

代码如下：

```PYTHON
#导包
from selenium import webdriver
from time import sleep
#step1：导包
from selenium.webdriver.support.select import Select
#初始化浏览器对象
driver=webdriver.Chrome()
#打开网页
driver.get("http://www.baidu.com")
#step2：实例化对象
select=Select(driver.find_element_by_id('selectA'))
#step3：调用方法
select.select_by_index(2)
sleep(2)
select.select_by_value('sh')
sleep(2)
select.select_by_visible_text("A北京")
sleep(1)
#退出浏览器
driver.quit()
```

##弹出框处理

```python
网页种常见的弹出框有三种：
alert    警告框
confirm   确认框
prompt    提示框
```

方法：

```PYTHON
1.获取弹出框的对象；
alert=driver.switch_to.alert
2.调用；
alert.text         返回弹出框中的文字信息
alert.accept       接受弹出框选项
alert.dismiss      取消弹出框选项
```

代码如下：

```python
#step1：获取弹出框对象
alert=driver.switch_to.alert
#step2：调用方法
print(alert.text)
alert.accept()
alert.dismiss()
```

##滚动条处理

```py
1.设置JS脚本控制滚动条；
js=window.scrollTo(0,1000)
0:左边距，1000：上边距，单位：像素
2.selenium调用执行JS脚本的方法
driver.excute_script(js)
```

代码如下：

```python
#step1最底层
js1="window.scrollTo(0,10000)"
driver.execute_script(js1)
sleep(2)
#step1最顶层
js2="window.scrollTo(0,0)"
driver.execute_script(js2)
sleep(2)
```

##Frame切换

```python
Frame：HTML页面中的一中框架，主要作用是在当前页面指定区域显示另一页面元素；
有两种形式：frameset,iframe
```

代码如下：

```python
driver.switch_to.frame(frame_reference)     切换到指定frame的方法
frame_reference   可以为frame框架的name，id,或者是定位到的frame元素

driver.switch_to.default_content()    恢复默认页面的方法
在frame中操作其他页面，必须先回到默认页面，才能进一步操作
```

##多窗口切换

```python
在HTML页面中，当点击超链接或按钮时，有的会在新的窗口打开页面
```

方法：

```python
driver.current_window_handle      获取当前窗口句柄
driver.window_handles             获取所有窗口句柄
driver.switch_to.window(handle)   切换至指定句柄窗口
```

代码如下：

```PYTHO N
#获取当前窗口的句柄
print(driver.current_window_handle)
driver.find_element_by_id('ZCA').click()
#获取所有窗口的句柄
print(driver.window_handles)
#获取指定窗口的句柄
handle=driver.window_handles[1]
#切换至指定句柄的窗口
driver.switch_to.window(handle)
```

##窗口截图

```PYTHON
driver.get_screenshot_as_file('./img/img01.png')
```

##验证码

```python
验证码的处理方式：去掉验证码，设置万能验证码，验证码识别技术，记录cookies(通过记录cookies，进行跳过登录)
不同的网站实现自动登录的字段不同，如有需要可以和开发人员确认，在自动登录的时候需要一直保持登录状态，否者就需要重新登录
```

方法：

```PYTHON
driver.get_cookie(name)          获取指定cookie，name为cookie的名称
driver.get_cookies()             获取本网站所有本地cookie
driver.add_cookie(cookie_dict)   添加cookie，cookie_dict为一个字典对象，必须包含name和value

```

代码如下：

```PYTHON
driver.add_cookie({"name":"字段名","value":"值"})
sleep(2)
driver.refresh()
```

##获取当前系统的时间

```PYTHON
now_time=time.strftime('%Y%m%d_%H%M%S')
格式化的第一种方式
driver.get_screenshot_as_file('./img/img_%s.png' % now_time)

格式化的第二种方式
driver.get_screenshot_as_file('./img/img_{}.png' .format(now_time))
```

## UnitTest基本使用

###TestCase:测试用例

```PYTHON
TestCase:测试用例
1.导包   import unittest
2.定义测试类   新建测试类必须继承unittest.TestCase
3.定义测试方法   测试方法名称命名必须以test开头
4.执行测试用例
   Pycharm右键用UnitTest或unittest.main()运行

```

###TestSuite:测试套件

```PYTHON
多条测试用例集合在一起就是一个测试套件
使用：
1.实例化   suite=unittest.TestSuite()
2.添加用例方法1   
suite.addTest(ClassName(MethodName"))         classname:类名；methodname：方法名
 添加用例方法2 
suite.addTest(unittest.makeSuite(ClassName))   
  搜索指定ClassName内test开头的方法，并添加到测试套件中 
                        
注意：TestSuite需要配合TestRunner才能被执行
                        
```

### TextTestRunner:执行测试用例和测试套件的

```python
使用：
1.实例化
runner=unittest.TextTestRunner()
2.执行
runner.run(suite)       suite测试套件的名称
```

### Testloader：测试套件

```python
使用：
1.suite=unittest.TestLoader().discover(start_dir,pattern="test*.py")=unittest.defaultTestLoader.discover(start_dir,pattern="test*.py")
"""
自动搜索指定目录下，指定开头的.py文件，并将查找到的测试用例组装到测试套件
start_dir：指定的测试用例的目录；pattern：查找的.py文件的格式
"""

```

###TestSuite与Testloader区别

```PYTHON
1.TestSuite需要手动添加测试用例，可以添加某个测试类下面的某个测试方法
2.Testloader搜索指定目录下的.py文件，自动动添加某个测试类下的所有测试方法，不能单独添加某个测试方法
```

## Fixture

### 使用场景

```PYTHON
在一个测试类中定义多个测试方法，查看每个测试方法执行完成所花费的时长
```

### Fixture控制级别

```PYTHON
方法级别
使用：1.初始化:def setUp(self);
     2.销毁:def tearDown(self);
     3.运行于测试方法的始末，即运行一次测试方法，就会运行一次setUp，tearDown

类级别
使用：1.初始化
      @classmethod
      def setUpClass(cls);
     2.销毁
      @classmethod
      def tearDownClass(cls);
     3.运行于测试类的始末，即运行一次测试类，就会运行一次setUpClass，tearDownClass
模块级别
使用：1.初始化
      def setUpModule();
     2.销毁
      def tearDownModule();
     3.运行于整个模块的始末，即整个模块只会运行一次setUpModule，tearDownModule
```

代码如下：

```python
#导包
from selenium import webdriver
from time import sleep
import unittest
class TestLogin(unittest.TestCase):
    def setUp(self):
        # 初始化浏览器对象
        self.driver = webdriver.Chrome()
        # 打开学伴B端首页
        self.driver.get("http://xb-test.easylesson.cn/index.html#/login")
        # 设置隐士等待
        self.driver.implicitly_wait(2)
        #窗口最大化
        self.driver.minimize_window()

    def test_login(self):
        # 输入用户名密码，不输入验证码，直接点击登录
        username = self.driver.find_element_by_xpath('//*[@placeholder="帐号"]').send_keys('cxy')
        password =self.driver.find_element_by_xpath('//*[@placeholder="密码"]').send_keys('cxy')
        verifycode =self.driver.find_element_by_xpath(
            '/html/body/div/div/div/div[2]/form/div[3]/div/div/div[1]/div/input').send_keys('sdf')
        login = self.driver.find_element_by_css_selector('.login-btn-submit').click()

    def tearDown(self) -> None:
        sleep(3)
        # 退出浏览器驱动
        self.driver.quit()
```

## 断言

```PYTHON
概念：让程序代替认为去判断程序执行的结果是否符合预期结果的过程
```

### UnitTest常用的断言方法

```python
assertTrue(expr)      验证expr是True，如果为false则fail
assertFalse(expr)     验证expr是false，如果为true则fail
assertEqual(first,second)          验证first==second，如果不等则fail
assertIn(member,container)		   验证是否member in container
```

### 捕获异常的方法

```PYTHON
        try:
            self.assertTrue(expr)
        except AssertionError as e:
            raise e
```

##参数化

```python
使用前需要先安装：pip3 install parameterized
```

####一个测试方法写一条用例

```python
# 自定义一个函数，测试加法
#一个测试用例中只包含一种方法
#缺点：代码冗余
# 导包
import unittest

# 定义一个加法函数
def add(x,y):
    return x+y
# 自定义测试类
class TestAdd(unittest.TestCase):
    # 自定义测试方法
    def test_add01(self):
        num=add(0,0)
        self.assertEqual(num,0)
    def test_add02(self):
        num=add(0,1)
        is_ok=num==1
        self.assertTrue(is_ok)
    def test_add03(self):
        num=add(1,1)
        self.assertEqual(num,3)
```

#### 一个测试方法写多条用例

```PYTHON
"""
测试加法
一个测试方法中包含多个测试用例
缺点：结果只有一个
"""
# 导包
import unittest

# 定义一个加法函数
def add(x,y):
    return x+y
# 自定义测试类
class TestAdd(unittest.TestCase):
    def test_add(self):
        test_data=[(0,0,0),(0,1,1),(1,1,2)]
        for x,y,expect in test_data:
            print("x={} y={} expect={}".format(x, y, expect))
            result=add(x,y)
            self.assertEqual(result,expect)
```

#### 参数化

```PYTHON
"""
测试加法
一个测试方法中包含多个测试用例
"""
# 导包
import unittest

from parameterized import parameterized

# 定义一个加法函数
def add(x,y):
    return x+y

# 自定义测试类
方法一：
class TestAdd(unittest.TestCase):
    test_data = [(0, 0, 0), (0, 1, 1), (1, 1, 2)]
    @parameterized.expand(test_data)
    def test_add(self,x,y,expect):
            print("x={} y={} expect={}".format(x, y, expect))
            result=add(x,y)
            self.assertEqual(result,expect)

 # 定义一个构建数据的函数
方法二：
def build_data():
    return [(0, 0, 0), (0, 1, 1), (1, 1, 2)]
class TestAdd(unittest.TestCase):
    @parameterized.expand(build_data())
    def test_add(self,x,y,expect):
        print("x={} y={} expect={}".format(x, y, expect))
        result = add(x, y)
        self.assertEqual(result, expect)

```

### 跳过

```pyt
概念：对于一些未完成的或者不满足测试条件的测试函数或类，可跳过执行
```

代码见下：

```python
# 导包
import unittest
version=10
# 自定义测试类
@unittest.skip('跳过')
class TestSkip(unittest.TestCase): 
    # 自定义测试方法
    # 直接将测试函数标记成跳过
   # @unittest.skip('代码未完成')
    def test_skip01(self):
        print('测试方法1')
    # 根据测试条件判断测试函数是否跳过
   # @unittest.skipIf(version<=10,'版本号小于等于10才跳过')
    def test_skip02(self):
        print('测试方法2')
```

### 测试报告英文模板

文件名：HTMLTestRunner.py

```PYTHON
"""
A TestRunner for use with the Python unit testing framework. It
generates a HTML report to show the result at a glance.

The simplest way to use this is to invoke its main method. E.g.

    import unittest
    import HTMLTestRunner

    ... define your tests ...

    if __name__ == '__main__':
        HTMLTestRunner.main()


For more customization options, instantiates a HTMLTestRunner object.
HTMLTestRunner is a counterpart to unittest's TextTestRunner. E.g.

    # output to a file
    fp = file('my_report.html', 'wb')
    runner = HTMLTestRunner.HTMLTestRunner(
                stream=fp,
                title='My unit test',
                description='This demonstrates the report output by HTMLTestRunner.'
                )

    # Use an external stylesheet.
    # See the Template_mixin class for more customizable options
    runner.STYLESHEET_TMPL = '<link rel="stylesheet" href="my_stylesheet.css" type="text/css">'

    # run the test
    runner.run(my_test_suite)


------------------------------------------------------------------------
Copyright (c) 2004-2007, Wai Yip Tung
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

* Redistributions of source code must retain the above copyright notice,
  this list of conditions and the following disclaimer.
* Redistributions in binary form must reproduce the above copyright
  notice, this list of conditions and the following disclaimer in the
  documentation and/or other materials provided with the distribution.
* Neither the name Wai Yip Tung nor the names of its contributors may be
  used to endorse or promote products derived from this software without
  specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED
TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A
PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER
OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
"""

# URL: http://tungwaiyip.info/software/HTMLTestRunner.html

__author__ = "Wai Yip Tung"
__version__ = "0.8.2"


"""
Change History

Version 0.8.2
* Show output inline instead of popup window (Viorel Lupu).

Version in 0.8.1
* Validated XHTML (Wolfgang Borgert).
* Added description of test classes and test cases.

Version in 0.8.0
* Define Template_mixin class for customization.
* Workaround a IE 6 bug that it does not treat <script> block as CDATA.

Version in 0.7.1
* Back port to Python 2.3 (Frank Horowitz).
* Fix missing scroll bars in detail log (Podi).
"""

# TODO: color stderr
# TODO: simplify javascript using ,ore than 1 class in the class attribute?

import datetime
import io
import sys
import time
import unittest
from xml.sax import saxutils


# ------------------------------------------------------------------------
# The redirectors below are used to capture output during testing. Output
# sent to sys.stdout and sys.stderr are automatically captured. However
# in some cases sys.stdout is already cached before HTMLTestRunner is
# invoked (e.g. calling logging.basicConfig). In order to capture those
# output, use the redirectors for the cached stream.
#
# e.g.
#   >>> logging.basicConfig(stream=HTMLTestRunner.stdout_redirector)
#   >>>

class OutputRedirector(object):
    """ Wrapper to redirect stdout or stderr """
    def __init__(self, fp):
        self.fp = fp

    def write(self, s):
        self.fp.write(s)

    def writelines(self, lines):
        self.fp.writelines(lines)

    def flush(self):
        self.fp.flush()

stdout_redirector = OutputRedirector(sys.stdout)
stderr_redirector = OutputRedirector(sys.stderr)



# ----------------------------------------------------------------------
# Template

class Template_mixin(object):
    """
    Define a HTML template for report customerization and generation.

    Overall structure of an HTML report

    HTML
    +------------------------+
    |<html>                  |
    |  <head>                |
    |                        |
    |   STYLESHEET           |
    |   +----------------+   |
    |   |                |   |
    |   +----------------+   |
    |                        |
    |  </head>               |
    |                        |
    |  <body>                |
    |                        |
    |   HEADING              |
    |   +----------------+   |
    |   |                |   |
    |   +----------------+   |
    |                        |
    |   REPORT               |
    |   +----------------+   |
    |   |                |   |
    |   +----------------+   |
    |                        |
    |   ENDING               |
    |   +----------------+   |
    |   |                |   |
    |   +----------------+   |
    |                        |
    |  </body>               |
    |</html>                 |
    +------------------------+
    """

    STATUS = {
    0: 'pass',
    1: 'fail',
    2: 'error',
    }

    DEFAULT_TITLE = 'Unit Test Report'
    DEFAULT_DESCRIPTION = ''

    # ------------------------------------------------------------------------
    # HTML Template

    HTML_TMPL = r"""<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>%(title)s</title>
    <meta name="generator" content="%(generator)s"/>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
    %(stylesheet)s
</head>
<body>
<script language="javascript" type="text/javascript"><!--
output_list = Array();

/* level - 0:Summary; 1:Failed; 2:All */
function showCase(level) {
    trs = document.getElementsByTagName("tr");
    for (var i = 0; i < trs.length; i++) {
        tr = trs[i];
        id = tr.id;
        if (id.substr(0,2) == 'ft') {
            if (level < 1) {
                tr.className = 'hiddenRow';
            }
            else {
                tr.className = '';
            }
        }
        if (id.substr(0,2) == 'pt') {
            if (level > 1) {
                tr.className = '';
            }
            else {
                tr.className = 'hiddenRow';
            }
        }
    }
}


function showClassDetail(cid, count) {
    var id_list = Array(count);
    var toHide = 1;
    for (var i = 0; i < count; i++) {
        tid0 = 't' + cid.substr(1) + '.' + (i+1);
        tid = 'f' + tid0;
        tr = document.getElementById(tid);
        if (!tr) {
            tid = 'p' + tid0;
            tr = document.getElementById(tid);
        }
        id_list[i] = tid;
        if (tr.className) {
            toHide = 0;
        }
    }
    for (var i = 0; i < count; i++) {
        tid = id_list[i];
        if (toHide) {
            document.getElementById('div_'+tid).style.display = 'none'
            document.getElementById(tid).className = 'hiddenRow';
        }
        else {
            document.getElementById(tid).className = '';
        }
    }
}


function showTestDetail(div_id){
    var details_div = document.getElementById(div_id)
    var displayState = details_div.style.display
    // alert(displayState)
    if (displayState != 'block' ) {
        displayState = 'block'
        details_div.style.display = 'block'
    }
    else {
        details_div.style.display = 'none'
    }
}


function html_escape(s) {
    s = s.replace(/&/g,'&amp;');
    s = s.replace(/</g,'&lt;');
    s = s.replace(/>/g,'&gt;');
    return s;
}

/* obsoleted by detail in <div>
function showOutput(id, name) {
    var w = window.open("", //url
                    name,
                    "resizable,scrollbars,status,width=800,height=450");
    d = w.document;
    d.write("<pre>");
    d.write(html_escape(output_list[id]));
    d.write("\n");
    d.write("<a href='javascript:window.close()'>close</a>\n");
    d.write("</pre>\n");
    d.close();
}
*/
--></script>

%(heading)s
%(report)s
%(ending)s

</body>
</html>
"""
    # variables: (title, generator, stylesheet, heading, report, ending)


    # ------------------------------------------------------------------------
    # Stylesheet
    #
    # alternatively use a <link> for external style sheet, e.g.
    #   <link rel="stylesheet" href="$url" type="text/css">

    STYLESHEET_TMPL = """
<style type="text/css" media="screen">
body        { font-family: verdana, arial, helvetica, sans-serif; font-size: 80%; }
table       { font-size: 100%; }
pre         { }

/* -- heading ---------------------------------------------------------------------- */
h1 {
	font-size: 16pt;
	color: gray;
}
.heading {
    margin-top: 0ex;
    margin-bottom: 1ex;
}

.heading .attribute {
    margin-top: 1ex;
    margin-bottom: 0;
}

.heading .description {
    margin-top: 4ex;
    margin-bottom: 6ex;
}

/* -- css div popup ------------------------------------------------------------------------ */
a.popup_link {
}

a.popup_link:hover {
    color: red;
}

.popup_window {
    display: none;
    position: relative;
    left: 0px;
    top: 0px;
    /*border: solid #627173 1px; */
    padding: 10px;
    background-color: #E6E6D6;
    font-family: "Lucida Console", "Courier New", Courier, monospace;
    text-align: left;
    font-size: 8pt;
    width: 500px;
}

}
/* -- report ------------------------------------------------------------------------ */
#show_detail_line {
    margin-top: 3ex;
    margin-bottom: 1ex;
}
#result_table {
    width: 80%;
    border-collapse: collapse;
    border: 1px solid #777;
}
#header_row {
    font-weight: bold;
    color: white;
    background-color: #777;
}
#result_table td {
    border: 1px solid #777;
    padding: 2px;
}
#total_row  { font-weight: bold; }
.passClass  { background-color: #6c6; }
.failClass  { background-color: #c60; }
.errorClass { background-color: #c00; }
.passCase   { color: #6c6; }
.failCase   { color: #c60; font-weight: bold; }
.errorCase  { color: #c00; font-weight: bold; }
.hiddenRow  { display: none; }
.testcase   { margin-left: 2em; }


/* -- ending ---------------------------------------------------------------------- */
#ending {
}

</style>
"""



    # ------------------------------------------------------------------------
    # Heading
    #

    HEADING_TMPL = """<div class='heading'>
<h1>%(title)s</h1>
%(parameters)s
<p class='description'>%(description)s</p>
</div>

""" # variables: (title, parameters, description)

    HEADING_ATTRIBUTE_TMPL = """<p class='attribute'><strong>%(name)s:</strong> %(value)s</p>
""" # variables: (name, value)



    # ------------------------------------------------------------------------
    # Report
    #

    REPORT_TMPL = """
<p id='show_detail_line'>Show
<a href='javascript:showCase(0)'>Summary</a>
<a href='javascript:showCase(1)'>Failed</a>
<a href='javascript:showCase(2)'>All</a>
</p>
<table id='result_table'>
<colgroup>
<col align='left' />
<col align='right' />
<col align='right' />
<col align='right' />
<col align='right' />
<col align='right' />
</colgroup>
<tr id='header_row'>
    <td>Test Group/Test case</td>
    <td>Count</td>
    <td>Pass</td>
    <td>Fail</td>
    <td>Error</td>
    <td>View</td>
</tr>
%(test_list)s
<tr id='total_row'>
    <td>Total</td>
    <td>%(count)s</td>
    <td>%(Pass)s</td>
    <td>%(fail)s</td>
    <td>%(error)s</td>
    <td>&nbsp;</td>
</tr>
</table>
""" # variables: (test_list, count, Pass, fail, error)

    REPORT_CLASS_TMPL = r"""
<tr class='%(style)s'>
    <td>%(desc)s</td>
    <td>%(count)s</td>
    <td>%(Pass)s</td>
    <td>%(fail)s</td>
    <td>%(error)s</td>
    <td><a href="javascript:showClassDetail('%(cid)s',%(count)s)">Detail</a></td>
</tr>
""" # variables: (style, desc, count, Pass, fail, error, cid)


    REPORT_TEST_WITH_OUTPUT_TMPL = r"""
<tr id='%(tid)s' class='%(Class)s'>
    <td class='%(style)s'><div class='testcase'>%(desc)s</div></td>
    <td colspan='5' align='center'>

    <!--css div popup start-->
    <a class="popup_link" onfocus='this.blur();' href="javascript:showTestDetail('div_%(tid)s')" >
        %(status)s</a>

    <div id='div_%(tid)s' class="popup_window">
        <div style='text-align: right; color:red;cursor:pointer'>
        <a onfocus='this.blur();' onclick="document.getElementById('div_%(tid)s').style.display = 'none' " >
           [x]</a>
        </div>
        <pre>
        %(script)s
        </pre>
    </div>
    <!--css div popup end-->

    </td>
</tr>
""" # variables: (tid, Class, style, desc, status)


    REPORT_TEST_NO_OUTPUT_TMPL = r"""
<tr id='%(tid)s' class='%(Class)s'>
    <td class='%(style)s'><div class='testcase'>%(desc)s</div></td>
    <td colspan='5' align='center'>%(status)s</td>
</tr>
""" # variables: (tid, Class, style, desc, status)


    REPORT_TEST_OUTPUT_TMPL = r"""
%(id)s: %(output)s
""" # variables: (id, output)



    # ------------------------------------------------------------------------
    # ENDING
    #

    ENDING_TMPL = """<div id='ending'>&nbsp;</div>"""

# -------------------- The end of the Template class -------------------


TestResult = unittest.TestResult

class _TestResult(TestResult):
    # note: _TestResult is a pure representation of results.
    # It lacks the output and reporting ability compares to unittest._TextTestResult.

    def __init__(self, verbosity=1):
        TestResult.__init__(self)
        self.stdout0 = None
        self.stderr0 = None
        self.success_count = 0
        self.failure_count = 0
        self.error_count = 0
        self.verbosity = verbosity

        # result is a list of result in 4 tuple
        # (
        #   result code (0: success; 1: fail; 2: error),
        #   TestCase object,
        #   Test output (byte string),
        #   stack trace,
        # )
        self.result = []


    def startTest(self, test):
        TestResult.startTest(self, test)
        # just one buffer for both stdout and stderr
        self.outputBuffer = io.StringIO()
        stdout_redirector.fp = self.outputBuffer
        stderr_redirector.fp = self.outputBuffer
        self.stdout0 = sys.stdout
        self.stderr0 = sys.stderr
        sys.stdout = stdout_redirector
        sys.stderr = stderr_redirector


    def complete_output(self):
        """
        Disconnect output redirection and return buffer.
        Safe to call multiple times.
        """
        if self.stdout0:
            sys.stdout = self.stdout0
            sys.stderr = self.stderr0
            self.stdout0 = None
            self.stderr0 = None
        return self.outputBuffer.getvalue()


    def stopTest(self, test):
        # Usually one of addSuccess, addError or addFailure would have been called.
        # But there are some path in unittest that would bypass this.
        # We must disconnect stdout in stopTest(), which is guaranteed to be called.
        self.complete_output()


    def addSuccess(self, test):
        self.success_count += 1
        TestResult.addSuccess(self, test)
        output = self.complete_output()
        self.result.append((0, test, output, ''))
        if self.verbosity > 1:
            sys.stderr.write('ok ')
            sys.stderr.write(str(test))
            sys.stderr.write('\n')
        else:
            sys.stderr.write('.')

    def addError(self, test, err):
        self.error_count += 1
        TestResult.addError(self, test, err)
        _, _exc_str = self.errors[-1]
        output = self.complete_output()
        self.result.append((2, test, output, _exc_str))
        if self.verbosity > 1:
            sys.stderr.write('E  ')
            sys.stderr.write(str(test))
            sys.stderr.write('\n')
        else:
            sys.stderr.write('E')

    def addFailure(self, test, err):
        self.failure_count += 1
        TestResult.addFailure(self, test, err)
        _, _exc_str = self.failures[-1]
        output = self.complete_output()
        self.result.append((1, test, output, _exc_str))
        if self.verbosity > 1:
            sys.stderr.write('F  ')
            sys.stderr.write(str(test))
            sys.stderr.write('\n')
        else:
            sys.stderr.write('F')


class HTMLTestRunner(Template_mixin):
    """
    """
    def __init__(self, stream=sys.stdout, verbosity=1, title=None, description=None):
        self.stream = stream
        self.verbosity = verbosity
        if title is None:
            self.title = self.DEFAULT_TITLE
        else:
            self.title = title
        if description is None:
            self.description = self.DEFAULT_DESCRIPTION
        else:
            self.description = description

        self.startTime = datetime.datetime.now()


    def run(self, test):
        "Run the given test case or test suite."
        result = _TestResult(self.verbosity)
        test(result)
        self.stopTime = datetime.datetime.now()
        self.generateReport(test, result)
        print(sys.stderr, '\nTimeElapsed: %s' % (self.stopTime-self.startTime))
        return result


    def sortResult(self, result_list):
        # unittest does not seems to run in any particular order.
        # Here at least we want to group them together by class.
        rmap = {}
        classes = []
        for n,t,o,e in result_list:
            cls = t.__class__
            if not cls in rmap:
                rmap[cls] = []
                classes.append(cls)
            rmap[cls].append((n,t,o,e))
        r = [(cls, rmap[cls]) for cls in classes]
        return r


    def getReportAttributes(self, result):
        """
        Return report attributes as a list of (name, value).
        Override this to add custom attributes.
        """
        startTime = str(self.startTime)[:19]
        duration = str(self.stopTime - self.startTime)
        status = []
        if result.success_count: status.append('Pass %s'    % result.success_count)
        if result.failure_count: status.append('Failure %s' % result.failure_count)
        if result.error_count:   status.append('Error %s'   % result.error_count  )
        if status:
            status = ' '.join(status)
        else:
            status = 'none'
        return [
            ('Start Time', startTime),
            ('Duration', duration),
            ('Status', status),
        ]


    def generateReport(self, test, result):
        report_attrs = self.getReportAttributes(result)
        generator = 'HTMLTestRunner %s' % __version__
        stylesheet = self._generate_stylesheet()
        heading = self._generate_heading(report_attrs)
        report = self._generate_report(result)
        ending = self._generate_ending()
        output = self.HTML_TMPL % dict(
            title = saxutils.escape(self.title),
            generator = generator,
            stylesheet = stylesheet,
            heading = heading,
            report = report,
            ending = ending,
        )
        self.stream.write(output.encode('utf8'))


    def _generate_stylesheet(self):
        return self.STYLESHEET_TMPL


    def _generate_heading(self, report_attrs):
        a_lines = []
        for name, value in report_attrs:
            line = self.HEADING_ATTRIBUTE_TMPL % dict(
                    name = saxutils.escape(name),
                    value = saxutils.escape(value),
                )
            a_lines.append(line)
        heading = self.HEADING_TMPL % dict(
            title = saxutils.escape(self.title),
            parameters = ''.join(a_lines),
            description = saxutils.escape(self.description),
        )
        return heading


    def _generate_report(self, result):
        rows = []
        sortedResult = self.sortResult(result.result)
        for cid, (cls, cls_results) in enumerate(sortedResult):
            # subtotal for a class
            np = nf = ne = 0
            for n,t,o,e in cls_results:
                if n == 0: np += 1
                elif n == 1: nf += 1
                else: ne += 1

            # format class description
            if cls.__module__ == "__main__":
                name = cls.__name__
            else:
                name = "%s.%s" % (cls.__module__, cls.__name__)
            doc = cls.__doc__ and cls.__doc__.split("\n")[0] or ""
            desc = doc and '%s: %s' % (name, doc) or name

            row = self.REPORT_CLASS_TMPL % dict(
                style = ne > 0 and 'errorClass' or nf > 0 and 'failClass' or 'passClass',
                desc = desc,
                count = np+nf+ne,
                Pass = np,
                fail = nf,
                error = ne,
                cid = 'c%s' % (cid+1),
            )
            rows.append(row)

            for tid, (n,t,o,e) in enumerate(cls_results):
                self._generate_report_test(rows, cid, tid, n, t, o, e)

        report = self.REPORT_TMPL % dict(
            test_list = ''.join(rows),
            count = str(result.success_count+result.failure_count+result.error_count),
            Pass = str(result.success_count),
            fail = str(result.failure_count),
            error = str(result.error_count),
        )
        return report


    def _generate_report_test(self, rows, cid, tid, n, t, o, e):
        # e.g. 'pt1.1', 'ft1.1', etc
        has_output = bool(o or e)
        tid = (n == 0 and 'p' or 'f') + 't%s.%s' % (cid+1,tid+1)
        name = t.id().split('.')[-1]
        doc = t.shortDescription() or ""
        desc = doc and ('%s: %s' % (name, doc)) or name
        tmpl = has_output and self.REPORT_TEST_WITH_OUTPUT_TMPL or self.REPORT_TEST_NO_OUTPUT_TMPL

        # o and e should be byte string because they are collected from stdout and stderr?
        if isinstance(o,str):
            # TODO: some problem with 'string_escape': it escape \n and mess up formating
            # uo = unicode(o.encode('string_escape'))
            uo = e
        else:
            uo = o
        if isinstance(e,str):
            # TODO: some problem with 'string_escape': it escape \n and mess up formating
            # ue = unicode(e.encode('string_escape'))
            ue = e
        else:
            ue = e

        script = self.REPORT_TEST_OUTPUT_TMPL % dict(
            id = tid,
            output = saxutils.escape(uo+ue),
        )

        row = tmpl % dict(
            tid = tid,
            Class = (n == 0 and 'hiddenRow' or 'none'),
            style = n == 2 and 'errorCase' or (n == 1 and 'failCase' or 'none'),
            desc = desc,
            script = script,
            status = self.STATUS[n],
        )
        rows.append(row)
        if not has_output:
            return

    def _generate_ending(self):
        return self.ENDING_TMPL


##############################################################################
# Facilities for running tests from the command line
##############################################################################

# Note: Reuse unittest.TestProgram to launch test. In the future we may
# build our own launcher to support more specific command line
# parameters like test title, CSS, etc.
class TestProgram(unittest.TestProgram):
    """
    A variation of the unittest.TestProgram. Please refer to the base
    class for command line parameters.
    """
    def runTests(self):
        # Pick HTMLTestRunner as the default test runner.
        # base class's testRunner parameter is not useful because it means
        # we have to instantiate HTMLTestRunner before we know self.verbosity.
        if self.testRunner is None:
            self.testRunner = HTMLTestRunner(verbosity=self.verbosity)
        unittest.TestProgram.runTests(self)

main = TestProgram

##############################################################################
# Executing this module from the command line
##############################################################################

if __name__ == "__main__":
    main(module=None)

```

### 测试报告中文模板

文件名：HTMLTestReportCN.py

```PYTHON
#coding=utf-8
"""
A TestRunner for use with the Python unit testing framework. It
generates a HTML report to show the result at a glance.

The simplest way to use this is to invoke its main method. E.g.

    import unittest
    import HTMLTestRunner

    ... define your tests ...

    if __name__ == '__main__':
        HTMLTestRunner.main()


For more customization options, instantiates a HTMLTestRunner object.
HTMLTestRunner is a counterpart to unittest's TextTestRunner. E.g.

    # output to a file
    fp = file('my_report.html', 'wb')
    runner = HTMLTestRunner.HTMLTestRunner(
                stream=fp,
                title='My unit test',
                description='This demonstrates the report output by HTMLTestRunner.'
                )

    # Use an external stylesheet.
    # See the Template_mixin class for more customizable options
    runner.STYLESHEET_TMPL = '<link rel="stylesheet" href="my_stylesheet.css" type="text/css">'

    # run the test
    runner.run(my_test_suite)


------------------------------------------------------------------------
Copyright (c) 2004-2007, Wai Yip Tung
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

* Redistributions of source code must retain the above copyright notice,
  this list of conditions and the following disclaimer.
* Redistributions in binary form must reproduce the above copyright
  notice, this list of conditions and the following disclaimer in the
  documentation and/or other materials provided with the distribution.
* Neither the name Wai Yip Tung nor the names of its contributors may be
  used to endorse or promote products derived from this software without
  specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED
TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A
PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER
OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
"""

# URL: http://tungwaiyip.info/software/HTMLTestRunner.html

__author__ = "Wai Yip Tung,  Findyou"
__version__ = "0.8.2.2"


"""
Change History
Version 0.8.2.1 -Findyou
* 改为支持python3

Version 0.8.2.1 -Findyou
* 支持中文，汉化
* 调整样式，美化（需要连入网络，使用的百度的Bootstrap.js）
* 增加 通过分类显示、测试人员、通过率的展示
* 优化“详细”与“收起”状态的变换
* 增加返回顶部的锚点

Version 0.8.2
* Show output inline instead of popup window (Viorel Lupu).

Version in 0.8.1
* Validated XHTML (Wolfgang Borgert).
* Added description of test classes and test cases.

Version in 0.8.0
* Define Template_mixin class for customization.
* Workaround a IE 6 bug that it does not treat <script> block as CDATA.

Version in 0.7.1
* Back port to Python 2.3 (Frank Horowitz).
* Fix missing scroll bars in detail log (Podi).
"""

# TODO: color stderr
# TODO: simplify javascript using ,ore than 1 class in the class attribute?

import datetime
import io
import sys
import time
import unittest
from xml.sax import saxutils
import sys

# ------------------------------------------------------------------------
# The redirectors below are used to capture output during testing. Output
# sent to sys.stdout and sys.stderr are automatically captured. However
# in some cases sys.stdout is already cached before HTMLTestRunner is
# invoked (e.g. calling logging.basicConfig). In order to capture those
# output, use the redirectors for the cached stream.
#
# e.g.
#   >>> logging.basicConfig(stream=HTMLTestRunner.stdout_redirector)
#   >>>

class OutputRedirector(object):
    """ Wrapper to redirect stdout or stderr """
    def __init__(self, fp):
        self.fp = fp

    def write(self, s):
        self.fp.write(s)

    def writelines(self, lines):
        self.fp.writelines(lines)

    def flush(self):
        self.fp.flush()

stdout_redirector = OutputRedirector(sys.stdout)
stderr_redirector = OutputRedirector(sys.stderr)

# ----------------------------------------------------------------------
# Template

class Template_mixin(object):
    """
    Define a HTML template for report customerization and generation.

    Overall structure of an HTML report

    HTML
    +------------------------+
    |<html>                  |
    |  <head>                |
    |                        |
    |   STYLESHEET           |
    |   +----------------+   |
    |   |                |   |
    |   +----------------+   |
    |                        |
    |  </head>               |
    |                        |
    |  <body>                |
    |                        |
    |   HEADING              |
    |   +----------------+   |
    |   |                |   |
    |   +----------------+   |
    |                        |
    |   REPORT               |
    |   +----------------+   |
    |   |                |   |
    |   +----------------+   |
    |                        |
    |   ENDING               |
    |   +----------------+   |
    |   |                |   |
    |   +----------------+   |
    |                        |
    |  </body>               |
    |</html>                 |
    +------------------------+
    """

    STATUS = {
    0: '通过',
    1: '失败',
    2: '错误',
    }

    DEFAULT_TITLE = '单元测试报告'
    DEFAULT_DESCRIPTION = ''
    DEFAULT_TESTER='最棒QA'

    # ------------------------------------------------------------------------
    # HTML Template

    HTML_TMPL = r"""<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>%(title)s</title>
    <meta name="generator" content="%(generator)s"/>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
    <link href="http://libs.baidu.com/bootstrap/3.0.3/css/bootstrap.min.css" rel="stylesheet">
    <script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
    <script src="http://libs.baidu.com/bootstrap/3.0.3/js/bootstrap.min.js"></script>
    %(stylesheet)s
</head>
<body >
<script language="javascript" type="text/javascript">
output_list = Array();

/*level 调整增加只显示通过用例的分类 --Findyou
0:Summary //all hiddenRow
1:Failed  //pt hiddenRow, ft none
2:Pass    //pt none, ft hiddenRow
3:All     //pt none, ft none
*/
function showCase(level) {
    trs = document.getElementsByTagName("tr");
    for (var i = 0; i < trs.length; i++) {
        tr = trs[i];
        id = tr.id;
        if (id.substr(0,2) == 'ft') {
            if (level == 2 || level == 0 ) {
                tr.className = 'hiddenRow';
            }
            else {
                tr.className = '';
            }
        }
        if (id.substr(0,2) == 'pt') {
            if (level < 2) {
                tr.className = 'hiddenRow';
            }
            else {
                tr.className = '';
            }
        }
    }

    //加入【详细】切换文字变化 --Findyou
    detail_class=document.getElementsByClassName('detail');
	//console.log(detail_class.length)
	if (level == 3) {
		for (var i = 0; i < detail_class.length; i++){
			detail_class[i].innerHTML="收起"
		}
	}
	else{
			for (var i = 0; i < detail_class.length; i++){
			detail_class[i].innerHTML="详细"
		}
	}
}

function showClassDetail(cid, count) {
    var id_list = Array(count);
    var toHide = 1;
    for (var i = 0; i < count; i++) {
        //ID修改 点 为 下划线 -Findyou
        tid0 = 't' + cid.substr(1) + '_' + (i+1);
        tid = 'f' + tid0;
        tr = document.getElementById(tid);
        if (!tr) {
            tid = 'p' + tid0;
            tr = document.getElementById(tid);
        }
        id_list[i] = tid;
        if (tr.className) {
            toHide = 0;
        }
    }
    for (var i = 0; i < count; i++) {
        tid = id_list[i];
        //修改点击无法收起的BUG，加入【详细】切换文字变化 --Findyou
        if (toHide) {
            document.getElementById(tid).className = 'hiddenRow';
            document.getElementById(cid).innerText = "详细"
        }
        else {
            document.getElementById(tid).className = '';
            document.getElementById(cid).innerText = "收起"
        }
    }
}

function html_escape(s) {
    s = s.replace(/&/g,'&amp;');
    s = s.replace(/</g,'&lt;');
    s = s.replace(/>/g,'&gt;');
    return s;
}
</script>
%(heading)s
%(report)s
%(ending)s

</body>
</html>
"""
    # variables: (title, generator, stylesheet, heading, report, ending)


    # ------------------------------------------------------------------------
    # Stylesheet
    #
    # alternatively use a <link> for external style sheet, e.g.
    #   <link rel="stylesheet" href="$url" type="text/css">

    STYLESHEET_TMPL = """
<style type="text/css" media="screen">
body        { font-family: Microsoft YaHei,Tahoma,arial,helvetica,sans-serif;padding: 20px; font-size: 80%; }
table       { font-size: 100%; }

/* -- heading ---------------------------------------------------------------------- */
.heading {
    margin-top: 0ex;
    margin-bottom: 1ex;
}

.heading .description {
    margin-top: 4ex;
    margin-bottom: 6ex;
}

/* -- report ------------------------------------------------------------------------ */
#total_row  { font-weight: bold; }
.passCase   { color: #5cb85c; }
.failCase   { color: #d9534f; font-weight: bold; }
.errorCase  { color: #f0ad4e; font-weight: bold; }
.hiddenRow  { display: none; }
.testcase   { margin-left: 2em; }
</style>
"""

    # ------------------------------------------------------------------------
    # Heading
    #

    HEADING_TMPL = """<div class='heading'>
<h1 style="font-family: Microsoft YaHei">%(title)s</h1>
%(parameters)s
<p class='description'>%(description)s</p>
</div>

""" # variables: (title, parameters, description)

    HEADING_ATTRIBUTE_TMPL = """<p class='attribute'><strong>%(name)s : </strong> %(value)s</p>
""" # variables: (name, value)



    # ------------------------------------------------------------------------
    # Report
    #
    # 汉化,加美化效果 --Findyou
    REPORT_TMPL = """
<p id='show_detail_line'>
<a class="btn btn-primary" href='javascript:showCase(0)'>概要{ %(passrate)s }</a>
<a class="btn btn-danger" href='javascript:showCase(1)'>失败{ %(fail)s }</a>
<a class="btn btn-success" href='javascript:showCase(2)'>通过{ %(Pass)s }</a>
<a class="btn btn-info" href='javascript:showCase(3)'>所有{ %(count)s }</a>
</p>
<table id='result_table' class="table table-condensed table-bordered table-hover">
<colgroup>
<col align='left' />
<col align='right' />
<col align='right' />
<col align='right' />
<col align='right' />
<col align='right' />
</colgroup>
<tr id='header_row' class="text-center success" style="font-weight: bold;font-size: 14px;">
    <td>用例集/测试用例</td>
    <td>总计</td>
    <td>通过</td>
    <td>失败</td>
    <td>错误</td>
    <td>详细</td>
</tr>
%(test_list)s
<tr id='total_row' class="text-center active">
    <td>总计</td>
    <td>%(count)s</td>
    <td>%(Pass)s</td>
    <td>%(fail)s</td>
    <td>%(error)s</td>
    <td>通过率：%(passrate)s</td>
</tr>
</table>
""" # variables: (test_list, count, Pass, fail, error ,passrate)

    REPORT_CLASS_TMPL = r"""
<tr class='%(style)s warning'>
    <td>%(desc)s</td>
    <td class="text-center">%(count)s</td>
    <td class="text-center">%(Pass)s</td>
    <td class="text-center">%(fail)s</td>
    <td class="text-center">%(error)s</td>
    <td class="text-center"><a href="javascript:showClassDetail('%(cid)s',%(count)s)" class="detail" id='%(cid)s'>详细</a></td>
</tr>
""" # variables: (style, desc, count, Pass, fail, error, cid)

    #失败 的样式，去掉原来JS效果，美化展示效果  -Findyou
    REPORT_TEST_WITH_OUTPUT_TMPL = r"""
<tr id='%(tid)s' class='%(Class)s'>
    <td class='%(style)s'><div class='testcase'>%(desc)s</div></td>
    <td colspan='5' align='center'>
    <!--默认收起错误信息 -Findyou
    <button id='btn_%(tid)s' type="button"  class="btn btn-danger btn-xs collapsed" data-toggle="collapse" data-target='#div_%(tid)s'>%(status)s</button>
    <div id='div_%(tid)s' class="collapse">  -->

    <!-- 默认展开错误信息 -Findyou -->
    <button id='btn_%(tid)s' type="button"  class="btn btn-danger btn-xs" data-toggle="collapse" data-target='#div_%(tid)s'>%(status)s</button>
    <div id='div_%(tid)s' class="collapse in">
    <pre>
    %(script)s
    </pre>
    </div>
    </td>
</tr>
""" # variables: (tid, Class, style, desc, status)

    # 通过 的样式，加标签效果  -Findyou
    REPORT_TEST_NO_OUTPUT_TMPL = r"""
<tr id='%(tid)s' class='%(Class)s'>
    <td class='%(style)s'><div class='testcase'>%(desc)s</div></td>
    <td colspan='5' align='center'><span class="label label-success success">%(status)s</span></td>
</tr>
""" # variables: (tid, Class, style, desc, status)

    REPORT_TEST_OUTPUT_TMPL = r"""
%(id)s: %(output)s
""" # variables: (id, output)

    # ------------------------------------------------------------------------
    # ENDING
    #
    # 增加返回顶部按钮  --Findyou
    ENDING_TMPL = """<div id='ending'>&nbsp;</div>
    <div style=" position:fixed;right:50px; bottom:30px; width:20px; height:20px;cursor:pointer">
    <a href="#"><span class="glyphicon glyphicon-eject" style = "font-size:30px;" aria-hidden="true">
    </span></a></div>
    """

# -------------------- The end of the Template class -------------------


TestResult = unittest.TestResult

class _TestResult(TestResult):
    # note: _TestResult is a pure representation of results.
    # It lacks the output and reporting ability compares to unittest._TextTestResult.

    def __init__(self, verbosity=1):
        TestResult.__init__(self)
        self.stdout0 = None
        self.stderr0 = None
        self.success_count = 0
        self.failure_count = 0
        self.error_count = 0
        self.verbosity = verbosity

        # result is a list of result in 4 tuple
        # (
        #   result code (0: success; 1: fail; 2: error),
        #   TestCase object,
        #   Test output (byte string),
        #   stack trace,
        # )
        self.result = []
        #增加一个测试通过率 --Findyou
        self.passrate=float(0)


    def startTest(self, test):
        TestResult.startTest(self, test)
        # just one buffer for both stdout and stderr
        self.outputBuffer = io.StringIO()
        stdout_redirector.fp = self.outputBuffer
        stderr_redirector.fp = self.outputBuffer
        self.stdout0 = sys.stdout
        self.stderr0 = sys.stderr
        sys.stdout = stdout_redirector
        sys.stderr = stderr_redirector


    def complete_output(self):
        """
        Disconnect output redirection and return buffer.
        Safe to call multiple times.
        """
        if self.stdout0:
            sys.stdout = self.stdout0
            sys.stderr = self.stderr0
            self.stdout0 = None
            self.stderr0 = None
        return self.outputBuffer.getvalue()


    def stopTest(self, test):
        # Usually one of addSuccess, addError or addFailure would have been called.
        # But there are some path in unittest that would bypass this.
        # We must disconnect stdout in stopTest(), which is guaranteed to be called.
        self.complete_output()


    def addSuccess(self, test):
        self.success_count += 1
        TestResult.addSuccess(self, test)
        output = self.complete_output()
        self.result.append((0, test, output, ''))
        if self.verbosity > 1:
            sys.stderr.write('ok ')
            sys.stderr.write(str(test))
            sys.stderr.write('\n')
        else:
            sys.stderr.write('.')

    def addError(self, test, err):
        self.error_count += 1
        TestResult.addError(self, test, err)
        _, _exc_str = self.errors[-1]
        output = self.complete_output()
        self.result.append((2, test, output, _exc_str))
        if self.verbosity > 1:
            sys.stderr.write('E  ')
            sys.stderr.write(str(test))
            sys.stderr.write('\n')
        else:
            sys.stderr.write('E')

    def addFailure(self, test, err):
        self.failure_count += 1
        TestResult.addFailure(self, test, err)
        _, _exc_str = self.failures[-1]
        output = self.complete_output()
        self.result.append((1, test, output, _exc_str))
        if self.verbosity > 1:
            sys.stderr.write('F  ')
            sys.stderr.write(str(test))
            sys.stderr.write('\n')
        else:
            sys.stderr.write('F')


class HTMLTestRunner(Template_mixin):
    """
    """
    def __init__(self, stream=sys.stdout, verbosity=1,title=None,description=None,tester=None):
        self.stream = stream
        self.verbosity = verbosity
        if title is None:
            self.title = self.DEFAULT_TITLE
        else:
            self.title = title
        if description is None:
            self.description = self.DEFAULT_DESCRIPTION
        else:
            self.description = description
        if tester is None:
            self.tester = self.DEFAULT_TESTER
        else:
            self.tester = tester

        self.startTime = datetime.datetime.now()


    def run(self, test):
        "Run the given test case or test suite."
        result = _TestResult(self.verbosity)
        test(result)
        self.stopTime = datetime.datetime.now()
        self.generateReport(test, result)
        print('\nTime Elapsed: %s' % (self.stopTime-self.startTime), file=sys.stderr)
        return result


    def sortResult(self, result_list):
        # unittest does not seems to run in any particular order.
        # Here at least we want to group them together by class.
        rmap = {}
        classes = []
        for n,t,o,e in result_list:
            cls = t.__class__
            if cls not in rmap:
                rmap[cls] = []
                classes.append(cls)
            rmap[cls].append((n,t,o,e))
        r = [(cls, rmap[cls]) for cls in classes]
        return r

    #替换测试结果status为通过率 --Findyou
    def getReportAttributes(self, result):
        """
        Return report attributes as a list of (name, value).
        Override this to add custom attributes.
        """
        startTime = str(self.startTime)[:19]
        duration = str(self.stopTime - self.startTime)
        status = []
        status.append('共 %s' % (result.success_count + result.failure_count + result.error_count))
        if result.success_count: status.append('通过 %s'    % result.success_count)
        if result.failure_count: status.append('失败 %s' % result.failure_count)
        if result.error_count:   status.append('错误 %s'   % result.error_count  )
        if status:
            status = '，'.join(status)
            self.passrate = str("%.2f%%" % (float(result.success_count) / float(result.success_count + result.failure_count + result.error_count) * 100))
        else:
            status = 'none'
        return [
            ('测试人员', self.tester),
            ('开始时间',startTime),
            ('合计耗时',duration),
            ('测试结果',status + "，通过率= "+self.passrate),
        ]


    def generateReport(self, test, result):
        report_attrs = self.getReportAttributes(result)
        generator = 'HTMLTestRunner %s' % __version__
        stylesheet = self._generate_stylesheet()
        heading = self._generate_heading(report_attrs)
        report = self._generate_report(result)
        ending = self._generate_ending()
        output = self.HTML_TMPL % dict(
            title = saxutils.escape(self.title),
            generator = generator,
            stylesheet = stylesheet,
            heading = heading,
            report = report,
            ending = ending,
        )
        self.stream.write(output.encode('utf8'))


    def _generate_stylesheet(self):
        return self.STYLESHEET_TMPL

    #增加Tester显示 -Findyou
    def _generate_heading(self, report_attrs):
        a_lines = []
        for name, value in report_attrs:
            line = self.HEADING_ATTRIBUTE_TMPL % dict(
                    name = saxutils.escape(name),
                    value = saxutils.escape(value),
                )
            a_lines.append(line)
        heading = self.HEADING_TMPL % dict(
            title = saxutils.escape(self.title),
            parameters = ''.join(a_lines),
            description = saxutils.escape(self.description),
            tester= saxutils.escape(self.tester),
        )
        return heading

    #生成报告  --Findyou添加注释
    def _generate_report(self, result):
        rows = []
        sortedResult = self.sortResult(result.result)
        for cid, (cls, cls_results) in enumerate(sortedResult):
            # subtotal for a class
            np = nf = ne = 0
            for n,t,o,e in cls_results:
                if n == 0: np += 1
                elif n == 1: nf += 1
                else: ne += 1

            # format class description
            if cls.__module__ == "__main__":
                name = cls.__name__
            else:
                name = "%s.%s" % (cls.__module__, cls.__name__)
            doc = cls.__doc__ and cls.__doc__.split("\n")[0] or ""
            desc = doc and '%s: %s' % (name, doc) or name

            row = self.REPORT_CLASS_TMPL % dict(
                style = ne > 0 and 'errorClass' or nf > 0 and 'failClass' or 'passClass',
                desc = desc,
                count = np+nf+ne,
                Pass = np,
                fail = nf,
                error = ne,
                cid = 'c%s' % (cid+1),
            )
            rows.append(row)

            for tid, (n,t,o,e) in enumerate(cls_results):
                self._generate_report_test(rows, cid, tid, n, t, o, e)

        report = self.REPORT_TMPL % dict(
            test_list = ''.join(rows),
            count = str(result.success_count+result.failure_count+result.error_count),
            Pass = str(result.success_count),
            fail = str(result.failure_count),
            error = str(result.error_count),
            passrate =self.passrate,
        )
        return report


    def _generate_report_test(self, rows, cid, tid, n, t, o, e):
        # e.g. 'pt1.1', 'ft1.1', etc
        has_output = bool(o or e)
        # ID修改点为下划线,支持Bootstrap折叠展开特效 - Findyou
        tid = (n == 0 and 'p' or 'f') + 't%s_%s' % (cid+1,tid+1)
        name = t.id().split('.')[-1]
        doc = t.shortDescription() or ""
        desc = doc and ('%s: %s' % (name, doc)) or name
        tmpl = has_output and self.REPORT_TEST_WITH_OUTPUT_TMPL or self.REPORT_TEST_NO_OUTPUT_TMPL

        # utf-8 支持中文 - Findyou
         # o and e should be byte string because they are collected from stdout and stderr?
        if isinstance(o, str):
            # TODO: some problem with 'string_escape': it escape \n and mess up formating
            # uo = unicode(o.encode('string_escape'))
            # uo = o.decode('latin-1')
            uo = o
        else:
            uo = o
        if isinstance(e, str):
            # TODO: some problem with 'string_escape': it escape \n and mess up formating
            # ue = unicode(e.encode('string_escape'))
            # ue = e.decode('latin-1')
            ue = e
        else:
            ue = e

        script = self.REPORT_TEST_OUTPUT_TMPL % dict(
            id = tid,
            output = saxutils.escape(uo+ue),
        )

        row = tmpl % dict(
            tid = tid,
            Class = (n == 0 and 'hiddenRow' or 'none'),
            style = n == 2 and 'errorCase' or (n == 1 and 'failCase' or 'passCase'),
            desc = desc,
            script = script,
            status = self.STATUS[n],
        )
        rows.append(row)
        if not has_output:
            return

    def _generate_ending(self):
        return self.ENDING_TMPL


##############################################################################
# Facilities for running tests from the command line
##############################################################################

# Note: Reuse unittest.TestProgram to launch test. In the future we may
# build our own launcher to support more specific command line
# parameters like test title, CSS, etc.
class TestProgram(unittest.TestProgram):
    """
    A variation of the unittest.TestProgram. Please refer to the base
    class for command line parameters.
    """
    def runTests(self):
        # Pick HTMLTestRunner as the default test runner.
        # base class's testRunner parameter is not useful because it means
        # we have to instantiate HTMLTestRunner before we know self.verbosity.
        if self.testRunner is None:
            self.testRunner = HTMLTestRunner(verbosity=self.verbosity)
        unittest.TestProgram.runTests(self)

main = TestProgram

##############################################################################
# Executing this module from the command line
##############################################################################

if __name__ == "__main__":
    main(module=None)

```



### 生成HTML测试报告

```python
方法1:pycharm中运行代码之后，左下角有一个导出测试报告功能
方法2：HTML TestRunner报告
# 复制HTML TestRunner.py文件到项目文件夹
# 导包
import unittest
import time
from test_add02 import TestAdd
from HTMLTestRunner import HTMLTestRunner

# 组装测试用例（生成测试套件）
suite = unittest.TestSuite()
suite.addTest(unittest.makeSuite(TestAdd))
# 准备报告写入路径和文件名
now_time=time.strftime('%H%m%d_%H%M%S')
file_path = './report_{}.html' .format(now_time)
# 打开报告，写入文件流
with open(file_path, 'wb')as f:
    # 执行测试，生成测试报告
    # 初始化执行对象
    runner = HTMLTestRunner(stream=f,title='自动化测试',description='chrome浏览器')
    # 调用RUN方法
    runner.run(suite)

```

### V1

```PYTHON
"""
v1,一个用例一个文件
登录，用户名正确，密码错误
"""
# 导包
from selenium import webdriver
from time import sleep

# 初始化浏览器对象，窗口最大化，设置隐士等待，打开三角洲后台系统
driver = webdriver.Chrome()
driver.maximize_window()
driver.implicitly_wait(10)
driver.get('要访问的网址')
driver.find_element_by_xpath('/html/body/div[2]/div/div[3]/button/span').click()
driver.find_element_by_xpath('/html/body/div[2]/div/div[3]/button/span').click()
#element1=driver.find_element_by_css_selector('.el-button--primary')
#element2=driver.find_element_by_css_selector('span')
#element1>element2.click()
# 输入正确的用户名，错误的密码，点击登录按钮
driver.find_element_by_css_selector('[placeholder="请输入用户名"]').send_keys('正确的用户名')
driver.find_element_by_xpath('//*[@placeholder="请输入密码"]').send_keys('错误的密码')
driver.find_element_by_xpath('//*[@id="app"]/div/div/div/form/div[3]/div/button/span') .click()
#driver.find_element_by_xpath('//*[@type="button"]/span').click()
# driver.find_element_by_css_selector('[type="button"]>span').click()
sleep(2)
# 获取错误信息
msg=driver.find_element_by_xpath('/html/body/div[2]/div/div[2]/div[2]/p').text
# msg=driver.find_element_by_css_selector('."el-message-box__message">p').text
print('msg=',msg)
# 退出浏览器
sleep(1)
driver.quit()

```

### 占位符

pass和...

### V2

```python
在使用unittest框架时，文件的命名必须符合规范：项目名+模块名
```

代码如下：

```PYTHON
"""
引入unittest
"""
# 导包
import unittest


# 自定义测试类
from time import sleep

from selenium import webdriver


class TestDeltaLogin(unittest.TestCase):
    """测试登录模块"""
    @classmethod
    def setUpClass(cls) -> None:
        # 初始化浏览器对象，窗口最大化，设置隐士等待，打开三角洲后台系统
        cls.driver = webdriver.Chrome()
        cls.driver.maximize_window()
        cls.driver.implicitly_wait(10)
        cls.driver.get('网页的网址')
        cls.driver.find_element_by_xpath('/html/body/div[2]/div/div[3]/button/span').click()
        cls.driver.find_element_by_xpath('/html/body/div[2]/div/div[3]/button/span').click()
    @classmethod
    def tearDownClass(cls) -> None:
        # 退出浏览器
        sleep(1)
        cls.driver.quit()
    def setUp(self) -> None:
        sleep(2)
    def tearDown(self) -> None:
        # 点击确定按钮
        self.driver.find_element_by_xpath('/html/body/div[2]/div/div[3]/button/span').click()

    # 自定义测试方法
    def test_username_error01(self):
        """用户不存在"""
        # 输入正确的用户名，错误的密码，点击登录按钮
        username=self.driver.find_element_by_css_selector('[placeholder="请输入用户名"]')
        username.clear()
        username.send_keys('用户名')

        self.driver.find_element_by_xpath('//*[@placeholder="请输入密码"]').send_keys('密码')
        sleep(2)
        self.driver.find_element_by_xpath('//*[@id="app"]/div/div/div/form/div[3]/div/button/span').click()
        sleep(2)
        # 获取错误信息
        msg = self.driver.find_element_by_xpath('/html/body/div[2]/div/div[2]/div[2]/p').text
        print('msg=', msg)

    def test_password_wrong02(self):
        """密码错误"""
        # 输入正确的用户名，错误的密码，点击登录按钮
        self.driver.find_element_by_css_selector('[placeholder="请输入用户名"]').send_keys('用户名')
        self.driver.find_element_by_xpath('//*[@placeholder="请输入密码"]').send_keys('密码')
        sleep(2)
        self.driver.find_element_by_xpath('//*[@id="app"]/div/div/div/form/div[3]/div/button/span').click()
        sleep(2)
        # 获取错误信息
        msg = self.driver.find_element_by_xpath('/html/body/div[2]/div/div[2]/div[2]/p').text
        print('msg=', msg)

```

### V3

Utils.py

```python
# 公共工具类,所有的文件都可以调用，因此放在最外面
# 导包
from selenium import webdriver
"""定义弹窗消息的方法"""
def get_tip_message():
    # 获取错误信息
    #msg = self.driver.find_element_by_xpath('/html/body/div[2]/div/div[2]/div[2]/p').text
    msg=DriverUtil.get_driver().find_element_by_xpath('/html/body/div[2]/div/div[2]/div[2]/p').text
    #print('msg=', msg)
    return msg
class DriverUtil(object):
    """浏览器驱动工具类"""
    driver=None
    """第一次调用的时候给浏览器赋值为空"""
    @classmethod
    def get_driver(cls):
        """
        获取浏览器驱动对象并完成初始化设置
        返回浏览器对象
        """
        """判断是否存在浏览器驱动对象"""
        if cls.driver is None:
            cls.driver=webdriver.Chrome()
            cls.driver.get("网页网址")
            cls.driver.maximize_window()
            cls.driver.implicitly_wait(10)
        return cls.driver
    @classmethod
    def quit_driver(cls):
        """关闭浏览器驱动对象"""
        # 判断浏览器存在
        if cls.driver is not None:
            """从代码逻辑上退出浏览器驱动对象"""
            cls.driver.quit()
            """为了防止关闭浏览器但电脑内存没有释放，将浏览器置为空"""
            cls.driver=None

# DriverUtil().get_driver()
"""类中的方法在调用的时候不能直接调用，需要先实例化一个类对象，再调用方法，但类级别的方法可以直接用类名和方法名调用"""
```



V3的完整代码+utils

```python
"""
v3方法封装：将一些有共性的，或多次被使用的代封装到一个方法中，供其他地方调用
定义获取驱动对象的工具类
封装获取弹出框的提示消息
"""

# 导包
import unittest

from time import sleep

from selenium import webdriver

# 自定义测试类
from utils import DriverUtil, get_tip_message


class TestDeltaLogin(unittest.TestCase):
    """测试登录模块"""
    @classmethod
    def setUpClass(cls) -> None:
        # 初始化浏览器对象，窗口最大化，设置隐士等待，打开三角洲后台系统
        # cls.driver = webdriver.Chrome()
        # cls.driver.maximize_window()
        # cls.driver.implicitly_wait(10)
        # cls.driver.get('网页网址')
        cls.driver=DriverUtil.get_driver()
        cls.driver.find_element_by_xpath('/html/body/div[2]/div/div[3]/button/span').click()
        cls.driver.find_element_by_xpath('/html/body/div[2]/div/div[3]/button/span').click()
    @classmethod
    def tearDownClass(cls) -> None:
        # 退出浏览器
        sleep(1)
        #cls.driver.quit()
        DriverUtil.quit_driver()
    def setUp(self) -> None:
        sleep(2)
    def tearDown(self) -> None:
        # 点击确定按钮
        self.driver.find_element_by_xpath('/html/body/div[2]/div/div[3]/button/span').click()

    # 自定义测试方法
    def test_username_error01(self):
        """用户不存在"""
        # 输入正确的用户名，错误的密码，点击登录按钮
        username=self.driver.find_element_by_css_selector('[placeholder="请输入用户名"]')
        username.clear()
        username.send_keys('用户名')

        self.driver.find_element_by_xpath('//*[@placeholder="请输入密码"]').send_keys('密码')
        sleep(2)
        self.driver.find_element_by_xpath('//*[@id="app"]/div/div/div/form/div[3]/div/button/span').click()
        sleep(2)
        # 获取错误信息
        # msg = self.driver.find_element_by_xpath('/html/body/div[2]/div/div[2]/div[2]/p').text
        # print('msg=', msg)
        msg=get_tip_message()

    def test_password_wrong02(self):
        """密码错误"""
        # 输入正确的用户名，错误的密码，点击登录按钮
        self.driver.find_element_by_css_selector('[placeholder="请输入用户名"]').send_keys('用户名')
        self.driver.find_element_by_xpath('//*[@placeholder="请输入密码"]').send_keys('密码')
        sleep(2)
        self.driver.find_element_by_xpath('//*[@id="app"]/div/div/div/form/div[3]/div/button/span').click()
        sleep(2)
        # 获取错误信息
        # msg = self.driver.find_element_by_xpath('/html/body/div[2]/div/div[2]/div[2]/p').text
        # print('msg=', msg)
        msg = get_tip_message()
```

### PO模式简介

```PYTHON
PO是Page Object的缩写，PO模式是自动化测试项目开发实践的最好的模式之一
PO模式把一个页面分为三层：对象库层，操作层，业务层
对象库层：封装定位元素的方法；
操作层：封装对元素的操作；
业务层：一个或多个操作组合起来完成一个业务功能，比如登录，账号，秘密，点击登录按钮三个操作
```

```python
login_page.py
from utils import DriverUtil


class LoginPage(object):
    """登录-对象库层"""
    def __init__(self):
        self.driver=DriverUtil.get_driver()
    def find_username(self):
        """定位用户名输入框的方法"""
        return self.driver.find_element_by_css_selector('[placeholder="请输入用户名"]')
    def find_password(self):
        """定位密码输入框的方法"""
        return self.driver.find_element_by_xpath('//*[@placeholder="请输入密码"]')
    def find_login_btn(self):
        """定位登录按钮的方法"""
        return self.driver.find_element_by_xpath('//*[@id="app"]/div/div/div/form/div[3]/div/button/span')

    ...
class LoginHandle(object):
    """登录—操作层"""
    def __init__(self):
        self.login_page=LoginPage()
    def imput_username(self,username):
        """输入用户名方法"""
        self.login_page.find_username().send_keys(username)
    def input_password(self,pwd):
        """输入密码的方法"""
        self.login_page.find_password().send_keys(pwd)
    def click_login_btn(self):
        """点击登录按钮的方法"""
        self.login_page.find_login_btn().click()



class LoginProxy(object):
    """登录-业务层"""
    def __init__(self):
        self.login_handle=LoginHandle()
    def login(self,username,pwd):
        """
        登录方法
        """
        self.login_handle.imput_username(username)
        self.login_handle.input_password(pwd)
        self.login_handle.click_login_btn()

```

```python
v4.py
"""
v4:引入了PO，将页面分为三个层次
"""

# 导包
import unittest

from time import sleep

# 自定义测试类
from V4.login_page import LoginProxy
from utils import DriverUtil, get_tip_message


class TestDeltaLogin(unittest.TestCase):
    """测试登录模块"""
    @classmethod
    def setUpClass(cls) -> None:
        # 初始化浏览器对象，窗口最大化，设置隐士等待，打开三角洲后台系统
        cls.driver=DriverUtil.get_driver()
        cls.driver.find_element_by_xpath('/html/body/div[2]/div/div[3]/button/span').click()
        cls.driver.find_element_by_xpath('/html/body/div[2]/div/div[3]/button/span').click()
        cls.login_proxy=LoginProxy()
    @classmethod
    def tearDownClass(cls) -> None:
        # 退出浏览器
        sleep(1)
        DriverUtil.quit_driver()
    def setUp(self) -> None:
        sleep(2)
    def tearDown(self) -> None:
        # 点击确定按钮
        self.driver.find_element_by_xpath('/html/body/div[2]/div/div[3]/button/span').click()

    # 自定义测试方法
    def test_username_error01(self):
        """用户不存在"""
        # 输入错误的的用户名，正确的密码，点击登录按钮
        self.login_proxy.login('chenxiaoyan','12345')
        # 获取错误信息
        msg=get_tip_message()
        self.assertIn("用户不存在或密码错误",msg)

    def test_password_wrong02(self):
        """密码错误"""
        # 输入正确的用户名，错误的密码，点击登录按钮
        self.login_proxy.login('chenxioayan','12345')
        # 获取错误信息
        msg = get_tip_message()
        self.assertIn("用户不存在或密码错误", msg)
```

### V5

```python
login_page.py
from selenium.webdriver.common.by import By

from utils import DriverUtil


class LoginPage(object):
    """登录-对象库层"""
    def __init__(self):
        self.driver=DriverUtil.get_driver()
        self.username=(By.CSS_SELECTOR,'[placeholder="请输入用户名"]')
        self.pwd=(By.XPATH,'//*[@placeholder="请输入密码"]')
        self.click_btn=(By.XPATH,'//*[@id="app"]/div/div/div/form/div[3]/div/button/span')
    def find_username(self):
        """定位用户名输入框的方法"""
        return self.driver.find_element(self.username[0],self.username[1])
    def find_password(self):
        """定位密码输入框的方法"""
        return self.driver.find_element(self.pwd[0],self.pwd[1])
    def find_login_btn(self):
        """定位登录按钮的方法"""
        return self.driver.find_element(self.click_btn[0],self.click_btn[1])

    ...
class LoginHandle(object):
    """登录—操作层"""
    def __init__(self):
        self.login_page=LoginPage()
    def imput_username(self,username):
        """输入用户名方法"""
        self.login_page.find_username().clear()
        self.login_page.find_username().send_keys(username)
    def input_password(self,pwd):
        """输入密码的方法"""
        self.login_page.find_password().clear()
        self.login_page.find_password().send_keys(pwd)
    def click_login_btn(self):
        """点击登录按钮的方法"""
        self.login_page.find_login_btn().click()



class LoginProxy(object):
    """登录-业务层"""
    def __init__(self):
        self.login_handle=LoginHandle()
    def login(self,username,pwd):
        """
        登录方法
        """
        self.login_handle.imput_username(username)
        self.login_handle.input_password(pwd)
        self.login_handle.click_login_btn()

```

### V6

```PYTHON
base_page.py
from utils import DriverUtil


class PageBase(object):
    """Page 基类（父类）"""
    def __init__(self):
        self.driver=DriverUtil.get_driver()
    def find_element_func(self,location):
        """查找元素的方法"""
        return self.driver.find_element(location[0],location[1])
class PageHandle(object):
    """Handle 基类（父类）"""
    def input_text(self,element,text):
        """输入内容的方法"""
        element.clear()
        element.send_keys(text)
```

```python
login_page.py
from selenium.webdriver.common.by import By

from V6.base_page import PageBase, PageHandle
from utils import DriverUtil


class LoginPage(PageBase):
    """登录-对象库层"""
    def __init__(self):
        super().__init__()#子类继承父类的方法，子类跟父类中有相同的，不需要重写，只需要扩展，就用此方法
        self.username=(By.CSS_SELECTOR,'[placeholder="请输入用户名"]')
        self.pwd=(By.XPATH,'//*[@placeholder="请输入密码"]')
        self.click_btn=(By.XPATH,'//*[@id="app"]/div/div/div/form/div[3]/div/button/span')
    def find_username(self):
        """定位用户名输入框的方法"""
        #return self.driver.find_element(self.username[0],self.username[1])
        return self.find_element_func(self.username)
    def find_password(self):
        """定位密码输入框的方法"""
        #return self.driver.find_element(self.pwd[0],self.pwd[1])
        return self.find_element_func(self.pwd)
    def find_login_btn(self):
        """定位登录按钮的方法"""
        #return self.driver.find_element(self.click_btn[0],self.click_btn[1])
        return self.find_element_func(self.click_btn)

    ...
class LoginHandle(PageHandle):
    """登录—操作层"""
    def __init__(self):
        self.login_page=LoginPage()
    def imput_username(self,username):
        """输入用户名方法"""
        self.input_text(self.login_page.find_username(),username)
    def input_password(self,pwd):
        """输入密码的方法"""
        #self.login_page.find_password().clear()
        #self.login_page.find_password().send_keys(pwd)
        self.input_text(self.login_page.find_password(), pwd)
    def click_login_btn(self):
        """点击登录按钮的方法"""
        self.login_page.find_login_btn().click()



class LoginProxy(object):
    """登录-业务层"""
    def __init__(self):
        self.login_handle=LoginHandle()
    def login(self,username,pwd):
        """
        登录方法
        """
        self.login_handle.imput_username(username)
        self.login_handle.input_password(pwd)
        self.login_handle.click_login_btn()

```

### 数据驱动

```PYTHON
数据驱动结果,可以理解为一种设计模式也可以理解为一种测试思想，将数据和测试代码分离，依赖于参数化
```

### JSON简介

```PYTHON
JSON 的全称是Java Script Object Notation 是Java Script对象表示方法；

特点：纯文本；具有良好的自我描述性，便于阅读和编写；具有清晰地层级结构；有效的提升网络传输效率；

语法规则：{}保存对象；[]保存列表；对象数组可以相互嵌套；数据采用键值对形式；多个数据由逗号分割；JSON文件的最外层可以是{}也可以是[]；里面的内容必须以键值对的形式存在；所有的键必须是字符串类型；只能用双引号；所有的逗号只能用英文

JSON值可以是：数字(整数或浮点数)，字符串(双引号中)，逻辑值(true或false)，列表([])，对象（{}），null
```

json文件的代码如下：

文件名以.json结尾的文件

```PYTHON
{
  "name": "小明",
  "age":18,
  "height": 180.4,
  "school": null,
  "link": [{"name": "http://www.baidu.com"}]

}
```

### Python字典与JSON之间的转换

Python字典转换成JSON字符串代码如下：

```PYTHON
import json
data={'id':1,
      'name':'小明',
      'address':'北京市昌平区',
      'school':None
      }
json_str=json.dumps(data)
print(json_str)
```

JSON字符串转换成Python字典代码如下：

```PYTHON
import json
json_str = '{"id":1, "name":"小明","address":"北京市昌平区","school":null}'
dict_data=json.loads(json_str)
print(dict_data)
```

### JSON文件读写

读取json文件的代码如下：

```PYTHON
import json
with open('文件的存放路径和文件名',encoding='UTF-8')as f:
    data=json.load(f)# 读取的文件为字典或数组
    print(data)
```

将字典写入json文件的代码如下：

```python
import json
param={"name":"小兰","age":12}
with open('文件的存放路径和文件名','w',encoding='UTF-8')as f:
    json.dump(param,f)
```



### 在线计算器加法的项目实战（po）

```python
utils.py
# 公共工具类,所有的文件都可以调用，因此放在最外面
# 导包
from selenium import webdriver
class DriverUtil(object):
    """浏览器驱动工具类"""
    driver=None
    """第一次调用的时候给浏览器赋值为空"""
    @classmethod
    def get_driver(cls):
        """
        获取浏览器驱动对象并完成初始化设置
        返回浏览器对象
        """
        """判断是否存在浏览器驱动对象"""
        if cls.driver is None:
            cls.driver=webdriver.Chrome()
            cls.driver.get("http://cal.apple886.com/")
            cls.driver.maximize_window()
            cls.driver.implicitly_wait(10)
        return cls.driver
    @classmethod
    def quit_driver(cls):
        """关闭浏览器驱动对象"""
        # 判断浏览器存在
        if cls.driver is not None:
            """从代码逻辑上退出浏览器驱动对象"""
            cls.driver.quit()
            """为了防止关闭浏览器但电脑内存没有释放，将浏览器置为空"""
            cls.driver=None
if __name__ == '__main__':
    DriverUtil.get_driver()
    DriverUtil.quit_driver()

```

```python
calc_page.py
from selenium.webdriver.common.by import By

from utils import DriverUtil


class CalcPage(object):
    """计算器的对象库层"""
    def __init__(self):
        self.driver=DriverUtil.get_driver()
        self.num_btn=(By.ID,'simple{}')# 数字键
        self.add_btn=(By.ID,'simpleAdd') # 加号键
        self.equal_btn=(By.ID,'simpleEqual')# 等号键
        self.result=(By.ID,'resultIpt')# 结果
    def find_num_btn(self,num):
        """定位数字按钮的方法"""
        #location=(self.num_btn[0],self.num_btn[1].format(num))
        #return self.driver.find_element(location[0],location[1])
        return self.driver.find_element(self.num_btn[0],self.num_btn[1].format(num))
    def find_add_btn(self):
        """定义查找加号的方法"""
        return self.driver.find_element(self.add_btn[0],self.add_btn[1])
    def find_equal_btn(self):
        """定义查找等号的按钮"""
        return self.driver.find_element(self.equal_btn[0],self.equal_btn[1])
    def find_result(self):
        """定义查找结果的方法"""
        return self.driver.find_element(self.result[0],self.result[1])
    ...
class CalcHandle(object):
    """计算器的操作层"""
    def __init__(self):
        self.calc_page=CalcPage()
    def click_num_btn(self,num):
        """点击数字按钮"""
        self.calc_page.find_num_btn(num).click()
    def click_add_btn(self):
        """点击加号按钮"""
        self.calc_page.find_add_btn().click()
    def click_equal_btn(self):
        """点击等号按钮"""
        self.calc_page.find_equal_btn().click()
    def get_result(self):
        """获取结果"""
        # 由于该元素没有直接体现文本信息，因此获取对用的TEXT可能没有结果
        # 可以通过获取value属性的属性值来获取结果
        return self.calc_page.find_result().get_attribute('value')
    def input_number(self,number):
        """定义一个输入数字的方法"""
        for i in str(number):
            self.click_num_btn(i)
class CalcProxy(object):
    """计算器的业务层"""
    def __init__(self):
        self.calc_handle=CalcHandle()
    def add_func(self,num1,num2):
        """测试计算器加法"""
        # 利用循环将输入的数拆分成一个一个的数
        # 整数不能被遍历，因此强转为字符串
        #for i in str(num1):
           # self.calc_handle.click_num_btn(i)
        self.calc_handle.input_number(num1)
        self.calc_handle.click_add_btn()
       # for j in str(num2):
            #self.calc_handle.click_num_btn(j)
        self.calc_handle.input_number(num2)
        self.calc_handle.click_equal_btn()

    def get_result_func(self):
        """获取结果的方法"""
        return self.calc_handle.get_result()

```

```python
test_calc.py
import json
import unittest

from parameterized import parameterized

from calc_page import CalcProxy
from utils import DriverUtil

def buid_calc_data():
    """构建数据"""
    with open('./calc_data.json', encoding='utf-8')as f:
        data = json.load(f)
        print(data)
        return data
class TestCalc(unittest.TestCase):
    """自定义测试类"""
    @classmethod
    def setUpClass(cls) -> None:
        cls.driver=DriverUtil.get_driver()
        cls.calc_proxy=CalcProxy()
    @classmethod
    def tearDownClass(cls) -> None:
        DriverUtil.quit_driver()
    @parameterized.expand(buid_calc_data())
    def test_calc_add(self,x,y,expect):
        """执行加法操作"""
        self.calc_proxy.add_func(x,y)
        result=self.calc_proxy.get_result_func()
        # 由于断言的结果是字符串因此将预期结果改成字符串的形式
        self.assertEqual(str(expect),result)

```

```python
calc_data.json
[
  [0,0,0],
  [1,0,1],
  [1,1,2],
  [12,23,35]

]
```

### Web自动化测试用例的书写规范

```PYTHON
1.ID
2.模块：PO页面对象的命名需要依据模块名来命名；
3.优先级：测试数据放在前面还是后面；
4.测试标题：自定义测试方法名；
5.预置条件：用例执行完之后，要恢复的状态；
6.步骤描述：业务逻辑；
7.测试数据：数据驱动，数据源文件的准备依据；
8.预期结果：数据驱动，数据源文件的准备依据，断言的设置依据；
9.测试结果
```

测试用例的覆盖不可能达到100%，一般公司会用web自动化测试做正向用例的测试，如果公司人员充足或有专门的自动化测试人员覆盖率最高能达到80%

### 日志

####概念

```PYTHON
日志就是用于记录系统运行时的信息，对一个事件的记录，也称为log
```

####作用

```PYTHON
1.调试程序
2.了解系统程序运行的情况，是否正常；
3.系统程序运行故障分析与问题定位；
4.用来做用户行为分析和数据统计；
```

#### 常见的日志级别

```PYTHON
DEBUG:调试级别，通常用于对代码的调试；
INFO:信息级别，突出强调信息的运行过程；
WARNING:警告级别，表明会出现潜在错误的情行，一般不影响软件的正常使用；
ERROR:错误级别，该级别的错误可能会导致系统的一些功能无法正常使用；
CRITICAL:严重错误级别，表明系统可能无法正常运行；

当指定日志级别后，系统会记录大于和等于指定日志级别的信息
```

#### 日志的基本用法

基本用法，代码如下：

```PYTHON
import logging
logging.debug("这是一条调试信息")
logging.info("这是一条普通信息")
logging.warning("这是一条警告信息")
logging.error("这是一条错误信息")
logging.critical("这是一条严重错误信息")
```

```PYTHON
LOGGING中默认的日志级别是warning，大于和等于该级别的信息才会被输出
```

#####设置日志级别，代码如下：

```PYTHON
import logging
logging.basicConfig(level=logging.DEBUG)
```

一般开发和测试环境中使用DEBUG或INFO,生产环境使用WARINING或ERROR,方便定位和排查问题

##### 设置日志格式，代码如下：

```python
默认的日志格式：
日志级别：Logger名称：日志内容
```

```python
format参数中常用的格式化信息
%(levelname)s:文本形式的日志级别
%(filename)s:调用日志输出函数的模块的文件名
%(lineno)s:调用日志输出级别的函数所在的代码行数
%(asctime)s:字符串形式的当前时间
%(message)s:用户输出的信息
```

```PYTHON
自定义日志格式：
import logging
fmt="%(levelname)s:%(filename)s:%(lineno)s:%(asctime)s:%(message)s"
logging.basicConfig(level=logging.INFO,format=fmt)
logging.debug("这是一条调试信息")
logging.info("这是一条普通信息")
logging.warning("这是一条警告信息")
logging.error("这是一条错误信息")
logging.critical("这是一条严重错误信息")
```

##### 将日志信息输出到文件中

```PYTHON
logging默认将日志输出到控制台，如果想将日志输出到文件代码如下：
import logging
fmt="%(levelname)s:%(filename)s:%(lineno)s:%(asctime)s:%(message)s"
logging.basicConfig(filename="a.log",level=logging.INFO,format=fmt)
logging.debug("这是一条调试信息")
logging.info("这是一条普通信息")
logging.warning("这是一条警告信息")
logging.error("这是一条错误信息")
logging.critical("这是一条严重错误信息")
```

#### 日志的高级用法

```PYTHON
logging模块四大日志组件
Logger:日志器：提供了程序使用日志的入口
Handle：处理器：将日志器创建的日志记录发送到合适的目的输出
Formatter：格式器：决定日志记录的最终输出格式
Filter：过滤器：提供了更细粒度的控制工具来决定输出哪条日志记录，丢弃哪条记录

关系：日志器可以设置多个处理器，每个处理器可以设置自己的格式器和过滤器
```

##### 如何创建Logger对象及其常用方法

```PYTHON
import logging
# 创建logger对象
logger=logging.getLogger()
# 常用方法,打印日志
logger.debug("调试")
logger.info("信息")
logger.warning("警告")
logger.error("错误")
logger.critical("严重")
# 设置日志器将会处理的日志消息的最低严重级别
logger.setLevel()
# 为该logger对象添加一个处理器对象
logger.addHandler()
# 为为该logger对象添加一个过滤器对象
logger.addFilter()
```

#####如何创建Handler对象及其常用方法

```PYTHON
Handler是一个基类，创建对象时如果导logging类导不出，可以导logging.handlers类
创建handler对象的常用方法：
方法1
import logging
handle=logging.StreamHandler() # 将日志消息发送到输出到stream
handle=logging.FileHandler(filename) # 将日志消息发送到磁盘文件，默认情况下文件大小会无限增加
方法2
import logging.handlers
handle=logging.handlers.TimedRotatingFileHandler # 将日志消息发送到磁盘文件，并支持文件按照时间进行切割
handle常用方法：
handle.setLevel()# 设置handle将会处理的日志消息的最低严重级别
handle.setFormatter() # 为handle设置一个格式器对象
handle.addFilter() # 为handle添加一个过滤器对象
```

##### 如何创建Formatter对象

```python
import logging
formatter=logging.Formatter(fmt=None, datefmt=None, style='%')
```

#### 日志使用实例

#####1.将日志信息同时输出到控制台和文件中

```PYTHON
# 导包
import logging
import logging.handlers
# 1.创建日志器对象
logger = logging.getLogger()
# 2.创建控制台处理器对象
handler1 = logging.StreamHandler()
# 3.创建文件处理器对象
handler2 = logging.FileHandler("b.log")
# 4.创建格式化器对象 
fmt = "%(levelname)s:%(filename)s:%(lineno)s:%(asctime)s:%(message)s"
formatter = logging.Formatter(fmt)
# 5.把格式化器添加到处理器
handler1.setFormatter(formatter)
handler2.setFormatter(formatter)
# 6.把处理器添加到日志器
logger.addHandler(handler2)
logger.addHandler(handler1)
```

##### 2.每日生成一个日志文件

```PYTHON

# 导包
import logging
import logging.handlers

# 1.创建日志器对象
logger = logging.getLogger()
# 设置日志器级别
logger.setLevel(logging.DEBUG)
# 2.创建控制台处理器对象
handler=logging.handlers.TimedRotatingFileHandler("c.log", when='midnight', interval=1, backupCount=3)
handler.setLevel(logging.INFO)
# 3.创建格式化器对象
fmt = "%(levelname)s:%(filename)s:%(lineno)s:%(asctime)s:%(message)s"
formatter = logging.Formatter(fmt)
# 5.把格式化器添加到处理器
handler.setFormatter(formatter)

# 6.把处理器添加到日志器
logger.addHandler(handler)

```

#### 自动化测试流程

```PYTHON
1.需求分析
根据需求文档
2.挑选适合做自动化测试的功能
3.设计自动化测试用例
原则：一般只实现核心业务流程或重复执行率较高的功能；一半一半正向验证的逻辑为主；尽量减少多个用例脚本之间的依赖；自动化测试用例执行完毕之后一般需要回归到原点；
4.搭建自动化测试环境[可选]
初始化项目
	1.新建项目
    项目名称：webAutoTestTPshop
    2.创建目录名称
    base
    data
    log
    page
    report
    screenshot
    script
    tools
	创建文件
    config.py
    run_suite.py
    utils.py
    3.安装依赖包
    安装selenium包
    安装parameterized包
    添加HTML TestRunner
初始化代码
	封装驱动工具类
    封装PO基类 定义BasePage 和BaseHandle
5.设计自动化测试项目的架构[可选]
6.编写代码
抽取PO
根据用例分析待测功能，提取页面对象
	1.定义页面对象文件
    一个页面一个文件，命名方式分别为功能名_page.py：
    首页：index_page.py
    登录页:longin_page.py
    2.分别编写对象库层，操作层，业务层的代码
编写测试脚本
	1.定义测试脚本文件
    登录模块：test_login.py
    购物车模块:test_cart.py
    订单模块:test_order.py
    2.使用unittest管理测试脚本
 执行测试脚本
	1.使用unittest执行测试脚本
    2.调试代码
完善代码
  数据驱动
    1.定义数据文件
    	定义测试文件存在在data目录中
        分模块定义测试文件
        	登录模块：login.json
        	购物车模块:cart.json
        	订单模块:order.json
        根据业务编写用例数据
    2.测试数据参数化
    	修改测试脚本，使用parameterized参数化
 日志收集
 使用logging模块实现日志的收集
     
7.执行测试用例
8.生成测试报告并分析结果
使用HTML TestRunner生成报告
```

### 拆包

```PYTHON
def add(a,*args):
    print(a)
    #print(args)
    print(*args)
add(1,2,3,4,5)
```

#### 守护属性

```PYTHON
_+变量名，改属性只能自己内部使用，外部无法调用
```

#### Pycharm创建工程时注意事项

```PYTHON
创建工程时有一个是真实环境和虚拟环境，两者之间的区别是：
1.一般如果写测试脚本用虚拟环境，因为别人可能需要拷贝你的脚本去运行，虚拟环境中自带第三方包，拷贝过去只要本地有解释器就能用，缺点是没次创建虚拟工程都需要重新安装第三方包
2.正式环境只要你安装了，之后再创建工程就不需要安装了，但拷贝之后别人用不了
```





