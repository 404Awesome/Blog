---
title: Vue2入门
toc: true
date: 2020-04-06 21:21:16
tags: ['Vue2']
---

# 声明

> 教学视频链接为:  <a class="alert-link" href="https://www.bilibili.com/video/BV15741177Eh/" target="_blank">Vue 教学视频</a> 点击观看
目前 Vue 分类中部分文章内容参考至 B 站一个 Vue 教学视频

其中部分内容直接出至教学视频中老师 PPT 中的内容

因为本人是第一次学习 Vue，难免文章中会出现纰漏，还望指正

下面为本篇文章正文

# Vue 实例

下面书写一段 Vue 代码体验一下，Hello Word 大法

```html
<p id="text">{{content}}</p>
```

```javascript
const temp = new Vue({
  el: "#text",
  data: {
    content: "Hello World",
  },
});
```

打开网页，查看效果

> 说明：Vue 是一个构造函数，首先创建一个 Vue 实例，传入的参数是一个对象 (options)，对象内有许多定义好的属性，通过操作对应的属性值，就可以管理 Dom 元素

## 实例属性

我们知道一个 Vue 实例，会传入一个对象类型的参数，即 options，而这个对象内的属性已经是 Vue 定义好的，我们通过知道该属性的作用及用法，便可以操作挂载好的 Dom 元素了，属性如下

### el 属性

> 类型：String | HTMLElement
>
> 作用：挂载 Dom 对象到 Vue 实例中，然后进行管理

el 属性用来绑定某个 Dom 元素，或者称其为挂载，然后对其进行管理，属性值可以像 jquery 一样进行选择元素，如上代码所示，还可以使用原生 Js 进行选择，如下：

> el: document.getElementById( 'text' );

### data 属性

> 类型：Object | Function
>
> 作用：Vue 实例对应的数据对象

data 属性用来定义一些变量，存放着需要用到的数据，如上述代码中，data 属性中定义了一个 content ，值是一个字符串的 'Hello World'，然后在页面中需要显示这段话，可以如 HTML 代码中一样，使用 &#123;&#123;content&#125;&#125; 将变量内的值显示到页面中，&#123;&#123;变量名&#125;&#125; 这种语法称之为 mustache 语法，后面还会有介绍

### methods 属性

> 类型：&#123; [key: string]: Function &#125;
>
> 作用：定义属于 Vue 的一些方法，可以在其他地方调用也可以在指令中使用

这个属性虽然没有在上面的例子中体现出来，不过大概来说，就是在这个属性中定义些方法，定义好的方法，可以在指令或者在 mustache 语法中被调用，然后执行方法内的命令，这个属性是方法的集合，下面通过一个例子体验一下

#### 例子

HTML 代码如下

```html
<main>
  <h1>{{num}}</h1>
  <button v-on:click="add()">+</button>
  <button v-on:click="less()">-</button>
</main>
```

Js 代码如下

```javascript
const temp = new Vue({
  el: "main",
  data: {
    num: 0,
  },
  methods: {
    add: function () {
      this.num++;
    },
    less: function () {
      this.num--;
    },
  },
});
```

通过 v-on 指令加上点击事件调用了方法，实现了计数器的功能，其中 v-on 等指令相关的内容稍后再去了解，我们还可以使用如下代码，实现和上面一样的功能，前提是 num 变量已经在 data 中定义好，如下

```html
<main>
  <h1>{{num}}</h1>
  <button v-on:click="num++">+</button>
  <button v-on:click="num--">-</button>
</main>
```

这样一来就用不到 methods 属性来定义方法实现了，这里需要注意的是，定义在 methods 属性内的方法，若想在方法内访问变量，需要在前面加上 this 关键字，这样一来，我们就完成了 Vue 的一些基本操作，通过上面的几个例子来看，通过 Vue 来管理 Dom 元素，较为灵活，并且该元素用到的数据和方法，分别通过 data 和 methods 属性来定义，这种归类方式简直不要太爽

<br>

> 注意：<br>在 options 对象中的属性 data 和 methods 中定义的变量或者方法，只能在 el 绑定的 Dom 元素内使用，还有就是，实例中的属性并不只有以上四种，后续会对其他属性进行介绍
