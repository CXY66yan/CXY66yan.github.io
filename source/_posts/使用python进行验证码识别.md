---
title: 使用python进行验证码识别
date: 2020-01-14 10:56:50
tags:  [ocr,python]
categories: 识别验证码
toc: true
---

###百度**OCR**使用教程

```PYTHON
1.打开百度云网址：https://cloud.baidu.com/

2.点击进入管理控制台：https://console.bce.baidu.com

3.左侧导航栏–>选择人工智能–>选择文字识别；

4.点击创建应用–>获取API KEY和SECRET KEY；

5. 安装baidu-aip模块；（pip3 install Baidu-api）

6.调用aip模块中的AipOcr，输入参数ID，KEY 和SECRET

(from api import ApiOcr

APP_ID=‘’

APi_KEY=‘’
SECRET_KEY=‘’

)

7.定义get_file_content方法获取图片二进制内容，参数为图片路径

8.创建image对象，填写图片实际路径（用client下的basicGeneral获取识别信息words）

```

### python自动识别web项目登录的验证码

```python
from PIL import Image
from selenium import webdriver
import time
from aip import AipOcr
import requests
import os

app_id = '17990316'
access_id = '0ef07eb536e0440c88281d627364430b'
access_secret = '28ad15a4ae584d19aef3052a1bb940ec'
client = AipOcr(app_id, access_id, access_secret)
requests.packages.urllib3.disable_warnings()

browser = webdriver.Chrome()
browser.get('http://xb-test.easylesson.cn/index.html#/login')
time.sleep(1)

options = {}
options["language_type"] = "ENG"
options["detect_direction"] = "true"
options["detect_language"] = "true"
options["probability"] = "true"

# 读取图片
def get_file_content(filePath):
    with open(filePath, 'rb') as fp:
        return fp.read()

def ocr(img_path):
    image = get_file_content(img_path)

    """ 带参数调用通用文字识别, 图片参数为本地图片 """
    try:
        #         return client.basicGeneral(image, options)['words_result'][0]['words']
        return client.basicAccurate(image, options)['words_result'][0]['words']

    except:
        return '----'


# code_base_url表示验证码图片要放置的地址
def login(code_base_url, username, password):
    while True:
        time.sleep(1)
        #     print(browser.current_url)
        if browser.current_url[-5:] == 'login':
            browser.find_element_by_xpath('/html/body/div/div/div/div[2]/form/div[1]/div/div/input').clear()
            browser.find_element_by_xpath('/html/body/div/div/div/div[2]/form/div[2]/div/div/input').clear()
            browser.find_element_by_xpath(
                '/html/body/div[1]/div/div/div[2]/form/div[3]/div/div/div[1]/div/input').clear()

            browser.save_screenshot(f'{code_base_url}/all.png')
            photo = browser.find_element_by_xpath('/html/body/div/div/div/div[2]/form/div[3]/div/div/div[2]/img')
            # x = photo.location['x']
            # y = photo.location['y']
            x = 2012
            y = 639
            # width = photo.size['width']
            # height = photo.size['height']
            width = 275
            height = 65
            # 打开图片  截图
            im = Image.open(f'{code_base_url}/all.png')
            im = im.crop((x, y, x + width, y + height))
            im.save(f'{code_base_url}/code.png')
            code = ocr(f'{code_base_url}/code.png')
            code = code.replace(' ', '')

            browser.find_element_by_xpath('/html/body/div/div/div/div[2]/form/div[1]/div/div/input').send_keys(username)
            browser.find_element_by_xpath('/html/body/div/div/div/div[2]/form/div[2]/div/div/input').send_keys(password)
            browser.find_element_by_xpath(
                '/html/body/div[1]/div/div/div[2]/form/div[3]/div/div/div[1]/div/input').send_keys(code)
            browser.find_element_by_xpath('/html/body/div[1]/div/div/div[2]/form/div[4]/div/button').click()
            continue
        break


if __name__ == '__main__':
    desktop_url = os.path.join(os.path.expanduser('~'), "Desktop")
    login(desktop_url, 'yukang', 'yukang')
    print('hello world')



```





