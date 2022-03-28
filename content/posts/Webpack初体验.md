---
title: Webpack初体验
toc: true
date: 2020-06-20 17:06:23
tags: ['WebPack']
---

# 基本使用

### 一. 初始化配置

1. 使用命令 npm init -y 初始化 package.json

2. 输入 npm i webpack webpack-cli -D 指令安装 webpack

   
### 二. 编译打包应用

1. 创建文件
2. 运行指令
   1. 开发环境指令： webpack src/js/index.js -o build/js/built.js --mode=development<br />                功能：webpack 能够编译打包 js 和 json 文件，并且能将 es6 的模块化语法转换成浏览器能识别的语法。
   2. 生产环境指令：webpack src/js/index.js -o build/js/built.js --mode=production<br />
      功能：在开发配置功能上多一个功能，压缩代码。

		> webpack 入口文件 -o 输出文件 --mode=模式<br />其中 mode 前方是两个横杠

3. 结论

   webpack 能够编译打包 js 和 json 文件
   能将 es6 的模块化语法转换成浏览器能识别的语法，能压缩代码

4. 问题

   不能编译打包 css、img 等文件
   不能将 js 的 es6 基本语法转化为 es5 以下语法



### 三. 目录结构

<img src='/img/post/webpack/dir.png' />

> 使用 Nodejs 的语法输出打包后的 js 文件，输出结果如上图



# 开发环境的基本配置

### 一. 创建配置文件

1. 在项目根目录下创建一个文件名为:  webpack.config.js

2. 配置文件内容如下

   ```javascript
   const { resolve } = require('path')
   
   module.exports = {
       entry: './src/index.js',
       output: {
           filename: 'built.js',
           path: resolve(__dirname, 'dist')
       },
       mode: 'development'
   }
   ```

3. 运行指令：webpack

4. 结果和上方的打包方式一样

### 二. 目录结构

如上方图片所示



### 三. 配置文件

1. webpack.config.js 配置文件中使用 Commonjs 规范，module.exports 导出一个对象，所有的配置信息在这个对象中定义
2. 其中 entry 是入口文件
3. output 输出文件是对象形式，output.filename 是输出文件的名称，output.path 是输出路径，这个路径不能是相对路径，应该是一个绝对路径，所以使用 node 中的变量 path 中的 resolve 方式
4. mode 是模式，有两种值 development 开发模式和 production 生产模式
