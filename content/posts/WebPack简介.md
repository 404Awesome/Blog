---
title: WebPack简介
toc: true
date: 2020-06-17 23:24:08
tags: ['WebPack']
---

# WebPack 简介

> 官网:  <a href="https://www.webpackjs.com/" target="_blank">点击访问</a><br />关于 WebPack 笔记，是根据尚硅谷的教学视频及老师笔记

<img src="/img/post/webpack/webpack-info.png" />

# 作用

1. webpack 是一种前端资源构建工具，一个静态模块打包器 (module bundler)
2. 在 webpack 看来, 前端的所有资源文件 (js/json/css/img/less/...) 都会作为模块处理
3. 它将根据模块的依赖关系进行静态分析，打包生成对应的静态资源 (bundle)



# 核心概念

1. Entry

   入口，指示 webpack 以哪个文件为入口起点开始打包，分析构建内部依赖图

2. Output

   输出，指示 webpack 打包后的资源 bundles 输出到那里去，以及如何命名

3. loader

   Loader 让 webpack 能够去处理那些非 JavaScript 文件 (webpack自身只能处理 JS)

4. Plugins

   插件，可以用于执行范围更广的任务，插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量等

5. Mode

   模式，指示 webpack 使用相应模式的配置，如下

   | 选项        | 特点                       |
   | :---------- | :------------------------- |
   | development | 能让代码本地调试运行的环境 |
   | production  | 能让代码优化上线运行的环境 |

   

# 技能点

<img src="/img/post/webpack/WebPack-skill.png" />



# 环境

环境参数

1. Nodejs 10 版本以上
2. webpack 4.26 版本以上

预备技能

1. 基本 Nodejs 知识和 Npm 指令
2. 熟悉 ES6 语法

