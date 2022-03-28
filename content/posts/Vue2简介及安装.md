---
title: Vue2简介及安装
toc: true
date: 2020-04-06 15:04:53
tags: ['Vue2']
---

# 官网及作者

> <a href="https://cn.vuejs.org/" target="_blank">Vue官网</a> 点击访问
>
> 作者尤雨溪出生在中国.无锡
> 之前担任于 Google 的工程师



# Vue 简介

Vue 是开源的

Vue 音似 view，Vue 是一个渐进式框架，渐进式的特点如下

1. 渐进式意为着你可以将 Vue 作为你应用的一部分嵌入其中，带来更丰富的交互体验
2. 或者如果你希望将更多的业务逻辑使用 Vue 实现，那么 Vue 的核心库以及生态系统
3. 比如 Core + Vue + router + Vuex，也可以满足你各种各样的需求

# Vue 特点及功能

1. 解耦视图和数据
2. 可复用的组件
3. 前端路由技术
4. 状态管理
5. 虚拟 DOM

# Vue 的安装

Vue 的安装方式有很多种，以下列举几种常用的

### 方式一 CDN

这种方式比较简单方便，无需下载资源到本地，就可以使用 Vue 了，但是需要本机联网，提供 CDN 服务的平台有很多，下面列举其中一个

> 登录 [BootCDN](https://www.bootcdn.cn/) 平台，搜索或选择 Vue ,主要分为以下两个版本
>
> 开发使用 vue.js，此版本未经压缩，保留了一些警告信息，便于开发
>
> 上线使用 vue.min.js，此版本经过压缩，和去除了一些不必要的信息

选择适合的版本，然后复制链接或直接复制 &lt;script&gt; 标签，在文件中引入即可，如下

> 开发版： &lt;script src="cdn.bootcss.com/vue/x.x.x/vue.js"&gt;&lt;/script&gt;
>
> 压缩版： &lt;script src="cdn.bootcss.com/vue/x.x.x/vue.min.js"&gt;&lt;/script&gt;

### 方式二 NPM

还可以使用 NPM 包管理工具，进行下载安装，在下载安装之前，确保电脑已安装 Node，使用如下命令，即可进行下载，下载完成后，也会有两个版本，选择所需的版本文件引入即可

> npm install vue

上面的命令默认安装最新的版本，若需要安装其他版本，可以使用如下命令

> npm install vue@版本号

### 方式三 Github

因为 Vue 是开源的，所以在 Github 中找到该项目，下载 zip 或者将文件克隆下载都可以，然后将对应文件引入即可，下面提供项目的 Github 地址

> <a href="https://github.com/vuejs/vue" target="_blank">Github地址</a>
>
> 别忘了点个 star 😉
>
> 以上需要注意的是，如果创建小型应用或 demo 的话，使用方式一或者三都可以，但是想要创建大型应用或项目，后面会使用 Vue Cli (脚手架) 配合 NPM 和 Webpack 来快速搭建应用，并且还可以使用 router 和 vuex 等
