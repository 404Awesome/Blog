---
title: Vue2生命周期及MVVM
toc: true
date: 2020-04-08 13:51:38
tags: ['Vue2']
---

# 生命周期

<img src='/img/post/vue2/Vue生命周期.png'>

上方的图片是官方网站给出的图片，其中说明了一个 Vue 实例从初始化到该实例销毁所经历的过程，其中红色内容是回调函数，当程序在生命周期图中经历到对应的部分时，就会触发对应的回调函数，默认回调函数是无返回值的，需要定义其方法才能使用，其中常用的回调函数有

1. created
2. mounted
3. destroyed

如何定义，如下

```javascript
const temp = new Vue({
  el: "div",
  data: {
    content: "Hello World",
  },
  craeted: function () {
    // function content
  },
  mounted: function () {
    // function content
  },
});
```

> 通常使用这几个回调函数，用来初始化页面，或者请求数据，在后面的组件化中也会用到生命周期函数，也可以叫做钩子函数 (hook)

# MVVM 框架

### 简介

MVVM 的主要目的是分离视图 View 和模型 Model，ViewModel 层封装了界面展示和操作的属性和接口，通过数据绑定，我们可以将 View 和 ViewModel 关联在一起，当 ViewModel 中数据发生变化时，View 也会同步进行更新，如下所示

<img src='/img/post/vue2/MVVM.png'>

在模式中，每一个视图都有对应的一个 ViewModel，同时 ViewModel 与模型建立联系，当接收到用户请求后，ViewModel 获取模型响应数据，并通过数据绑定将相应的视图页面重新渲染，模型层的数据只需要传入 ViewModel 即可实现视图的同步更新

Vue.js 就是一套轻量级的 MVVM 框架，与其他重量级框架不同的是，Vue 的核心库只关注视图层，并且提供尽可能简单的 API 以实现数据绑定，组件复用等机制

### Vue 与 MVVM

1. View 层

   视图层

   在我们的前端开发中，通常就是 DOM 层

   主要的作用是给用户展示各种信息

2. Model 层

   数据层

   数据可能是我们固定的数据，更多的是来自与服务器请求来的数据

3. ViewModel / VueModel 层

   视图模型层

   视图模型层是 View 和 Model 沟通的桥梁

   一方面它实现了 Date Binding，也就是数据绑定，将 Model 的改变实时的反应到 View 中

   另一方面它实现了 DOM Listener，也就是 DOM 监听，当 DOM 发生一些事件 (点击，滚动等) 时，可以监听到，并在需要的情况下改变对应的 Data
