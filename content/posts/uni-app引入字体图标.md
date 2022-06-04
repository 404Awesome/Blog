---
title: "UniApp引入字体图标"
date: 2022-04-10T23:03:42+08:00
toc: true
tags: ['UniApp']
---

#  前言

> UniApp 支持 base64 格式字体图标
>
> 所以想使用字体图标, 需要使用转换工具进行转换



# 下载字体图标文件

> 这里以 <a href="https://remixicon.com/" target="_blank">remixicon</a> 为例
>
> 通过 npm下载到本地, 字体图标目录结构如下, 这里只用到 ttf 文件

<img src="/img/post/uni_app/remixicon_ structure.png">



# 使用工具进行转换

> 这里用到的转换工具是在线网站
>
> 点击 <a href="https://transfonter.org/" target="_blank">transfonter</a> 进行访问

<img src="/img/post/uni_app/transfonter.png">

1. 第一步：点击 add fonts, 将下载好的字体文件中的 ttf 文件选中并上传
2. 第二步：如上图所示, 将 Base64 encode 选项打开, 下方只勾选 TTF 选项
3. 第三步：点击 Convert 按钮，进行转换
4. 第四步：转换后，点击下载

> 下载并解压后会得到以下三个文件

1. demo.html
2. xxx.ttf
3. stylesheet.css  重要



# 替换 @font-face

> 将 stylesheet.css 文件中 @font-face 进行复制, 找到我们之前下载好的字体图标文件
>
> 我这里用了 npm, 所以文件是 node_modules/remixicon/fonts/remixicon.css
>
> 将样式文件中 @font-face 进行替换	
>
> 到这里就可以的正常引用, 并使用了该字体图标了



# 结束语

> 因为 node_modules 被 .gitignore 文件忽略, 所以不会上传
>
> 别人下载了该源码, 并不知晓此处做了改动
