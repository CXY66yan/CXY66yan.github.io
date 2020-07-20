---
title: blogs
date: 2019-08-27 17:45:18
tags:  [blogs,hexo]
categories: hexo
toc: true
---
[TOC]
#如何在hexo新建文件并上传至博客
1.首先打开终端，切换到_posts文件所在路径，hexo new 文件名（新建一个.md文件）

2.以Typora的形式打开进行编辑，完成之后在终端中输入：hexo generate，回车，生成静态页面

3.再输入：hexo server，回车，到localhost:4000预览博客效果

4.最后输入：hexo deploy，回车，同步到github上去就行了

## 解决hexo博客中可以上传图片

```PYTHON
1.配置文件_config.yml中 post_asset_folder:true

2.安装插件：在hexo的目录下执行(博客文件夹下执行)
npm install https://github.com/CodeFalling/hexo-asset-image --save 
 安装的过程中可能会出现：终端一直处于fetchMetadata: sill resolveWithNewModule hexo-asset-imag状态
**解决方法**：
#将npm的源换成淘宝镜像(在该目录下)
1.使用下面命令更换源：npm config set registry https://registry.npm.taobao.org
2.源更换完成之后，使用下面命令检查
npm config get registry#或者npm info express
3.输入命令执行后，输出内容如下，即代表更换成功。
https://registry.npm.taobao.org/
4.此时再输入安装插件的网址
完成安装后用hexo新建文章的时候会发现_posts目录下面会多出一个和文章名字一样的文件夹。图片就可以放在文件夹下面
#打开/node_modules/hexo-asset-image/index.js，将内容更换为下面的代码
​```python
'use strict';
var cheerio = require('cheerio');

// http://stackoverflow.com/questions/14480345/how-to-get-the-nth-occurrence-in-a-string
function getPosition(str, m, i) {
  return str.split(m, i).join(m).length;
}

var version = String(hexo.version).split('.');
hexo.extend.filter.register('after_post_render', function(data){
  var config = hexo.config;
  if(config.post_asset_folder){
    	var link = data.permalink;
	if(version.length > 0 && Number(version[0]) == 3)
	   var beginPos = getPosition(link, '/', 1) + 1;
	else
	   var beginPos = getPosition(link, '/', 3) + 1;
	// In hexo 3.1.1, the permalink of "about" page is like ".../about/index.html".
	var endPos = link.lastIndexOf('/') + 1;
    link = link.substring(beginPos, endPos);

    var toprocess = ['excerpt', 'more', 'content'];
    for(var i = 0; i < toprocess.length; i++){
      var key = toprocess[i];
 
      var $ = cheerio.load(data[key], {
        ignoreWhitespace: false,
        xmlMode: false,
        lowerCaseTags: false,
        decodeEntities: false
      });

      $('img').each(function(){
		if ($(this).attr('src')){
			// For windows style path, we replace '\' to '/'.
			var src = $(this).attr('src').replace('\\', '/');
			if(!/http[s]*.*|\/\/.*/.test(src) &&
			   !/^\s*\//.test(src)) {
			  // For "about" page, the first part of "src" can't be removed.
			  // In addition, to support multi-level local directory.
			  var linkArray = link.split('/').filter(function(elem){
				return elem != '';
			  });
			  var srcArray = src.split('/').filter(function(elem){
				return elem != '' && elem != '.';
			  });
			  if(srcArray.length > 1)
				srcArray.shift();
			  src = srcArray.join('/');
			  $(this).attr('src', config.root + link + src);
			  console.info&&console.info("update link as:-->"+config.root + link + src);
			}
		}else{
			console.info&&console.info("no src attr, skipped...");
			console.info&&console.info($(this));
		}
      });
      data[key] = $.html();
    }
  }
});
​```python

3.文章中插入图片方式：

方式一：{% asset_img test.jpg This is an test image %}
其中test.jpg就是你要引用的图片，我这里就是test.jpg，后面的This is an test image是图片描述，可以自己修改。

方式二： ![picturedescription](picturepath logo.jpg) 就可引用到图片 logo.jpg
picturedescription:图片的描述；picturepath：图片在同名文件夹中的路径；
```

