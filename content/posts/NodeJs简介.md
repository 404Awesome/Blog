---
title: NodeJs简介
toc: true
date: 2020-05-23 22:10:21
tags: ['Node']
---

# Node.Js 是什么?

Node.js 是一个基于<a href="https://v8.dev/" target="_blank">Chrome V8 引擎</a>的 JavaScript 运行时

点击此处访问<a href="https://nodejs.org/zh-cn/" target="_blank">Node官网</a>

Node 的创始人为：Ryan Dahl

> 这里需要注意的是目前 Ryan Dahl 认为 Node 违背了它的初衷, 否定了 Node, 然后开发了 deno, deno 支持 TypeScript 运行时，设计更加安全，有兴趣的可以了解下


1. Node.js 不是一门语言
2. Node.js 不是库，更不是框架
3. Node.js 是一个 JavaScript 运行时环境
4. 因为 Node.js 是基于 V8 引擎的，所以可以解析并执行 JS 代码





# Node.js 中的 JS

没有 Bom 和 Dom

在 Node.js 这个 JS 执行环境中为 JS 提供了一些服务器级别的 API

1. 列如文件读写
2. 网络服务的构建
3. 网络通信
4. http 服务器
5. 等处理...





# Node.js 特性

> Node.js uses an event-driven, non-blocking I/0 model, that makes it lightweight and efficient 

1. event-driven 事件驱动
2. non-blocking I/0 model 非阻塞 IO 模型（异步）
3. lightweight and efficient 轻量和高效

> Node.js package ecosyste, npm is the largest ecosystem of open source libraries in the world

1. npm 是世界上最大的开源库生态系统
2. 绝大多数 JS 包都存放至 npm 上，方便开发人员下载及使用
3. npm 通过命令式，下载及管理 JS 包

