---
title: "JavaScript由来"
date: 2020-03-26T23:17:41+08:00 
toc: true
tags: ["JavaScript"]
---

# JavaScript历史

## 诞生

JavaScript 诞生于1995年，简称 JS，由网景公司 Netscape 开发，当时的网景公司正凭借其 Navigator 浏览器成为Web时代开启时最著名的第一代互联网公司，由于网景公司希望能在静态HTML页面上添加一些动态效果，据说由 Brendan Eich 在两周内就设计出了 JavaScript，JS是一种网页脚本语言，当时是为了能让网页拥有更好的交互体验而开发的

## 更名

起初该编程语言并非叫做 JavaScript，而是叫做 LiveScript，后来因为 Sun 公司所开发的 Java 在当时的人气很高，加上自身在市场上的反馈不是很理想，然将 LiveScript 改名为 JavaScript，想要通过名称来混淆视野，以此提升自己的人气，但是 Java 和 JavaScript 终究是两回事，并没有太多关系

## 标准化

其实可以将 ECMAScript 简称 ES 理解为 JavaScript，本质上是差不多的，因为当时 JavaScript 的出现，改变了网页的格局，随着 JavaScript 的大火，一年后微软模仿 JavaScript 开发了 JScript，为了让 JavaScript 成为全球标准，因此由 几个公司联合 ECMA（European Computer Manufacturers Association 欧洲计算机制造商协会）组织共同定制了 JavaScript 语言的标准，被称为 ECMAScript 标准，因此才能够让 JavaScript 标准化，否则，你懂的，头发 -1，1997年06月 ECMA-262 的第一个版本于被欧洲计算机制造商协会采纳，并将 ECMA-262 标准取名为 ECMAScript，其中 ES3 被浏览器厂商所普及，也是最通行的一个版本，ES6 改动较大，同时也增加了许多新特性，学习完基础后，便可以尝试学习 ES6 语法了, ES7, ES8 等...

<p class="alert alert-primary">可以学习阮一峰的 <a target="_blank" class="alert-link" href="https://es6.ruanyifeng.com/">ES6 入门教程</a></p>

### ES 版本情况

1. ES 1

   > 发布时间: 1997-06
   >
   > 描述:   ECMA 发布 262 号标准文件 (ECMA-262)，规定了浏览器脚本语言的标准

2. ES 2

   > 发布时间: 1998-06
   >
   > 描述:   未增加新特性，对内容做了调整

3. ES 3

   >  发布时间: 1999-12
   >
   >  描述:   有较好的完善修改，成为了通用标准，目前绝大多数浏览器都支持这个版本

4. ES 4

   >  发布时间: 2008-07
   >
   >  描述:   因为提议的改动太大，未通过

5. ES 5

   >  发布时间: 2009-12
   >
   >  描述:   新功能主要包括：JSON对象 (含parse/stringify等方法)，Array和Object增加一些方法，严格模式 (use strict)，函数的bind方法等

6. ES 6

   >  发布时间: 2015-06
   >
   >  描述:   也称之为 ECMAScript 2015，该版本改动较大，同时也增加了许多特性，比如，let/const、变量的解构赋值、Promise 等

7. ES 7

   >  发布时间: 2016
   >
   >  描述:   也称之为 ECMAScript 2016，Array.prototype.includes()，求幂运算符等

8. ES 8

   >  发布时间: 2017
   >
   >  描述:   也称之为 ECMAScript 2017，异步函数，共享内存等

9. ES 9

   >  发布时间: 2018
   >
   >  描述:     也称之为 ECMAScript 2018，异步迭代等



### ES 语法提案

1. Stage 0

   > 定义：Strawman（展示阶段）
   >
   > 内容：任何尚未提交为正式提案的讨论，想法，改变或对已有规范的补充建议都被认为是一个稻草人草案（“strawman” proposal），但只有TC39成员可以提出此阶段的草案。

2. Stage 1

   > 定义：Proposal（征求意见阶段）
   >
   > 内容：此阶段，稻草人草案升级为正式化的提案，并将逐步解决多部门关切的问题，如与其他提案的相互之间会有什么影响，这一草案具体该如何实施等问题。人们需要对这些问题提供具体的解决方案。stage1的提案通常还需要包括API描述，拥有说明性使用示例，并对语义和算法进行讨论，一般来说草案在这一阶段会经历巨大的变化。

3. Stage 2

   > 定义：Draft（草案阶段）
   >
   > 内容：此阶段，草案就有了初始的规范。通过 polyfill，开发者可以开始使用这一阶段的草案了，一些浏览器引擎也会逐步对这一阶段的规范的提供原生支持，此外通过使用构建工具也可以编译源代码为现有引擎可以执行的代码，这些方法都使得这一阶段的草案可以开始被使用了。

4. Stage 3

   > 定义：Candidate（候选人阶段）
   >
   > 内容：此阶段的规范就属于候选推荐规范了，这一阶段之后变化就不会那么大了，要达到这一阶段需要满足以下条件：
   >
   > - 规范的编辑和指定的审阅者必须在最终规范上签字；
   > - 用户也应该对该提议感兴趣；
   > - 提案必须至少被一个浏览器原生支持；
   > - 拥有高效的 ployfill，或者被Babel支持；

5. Stage 4  

   > 定义：Finished（定案阶段）
   >
   > 内容：此阶段的提案必须有两个独立的通过验收测试的实现，进入第4阶段的提案将包含在 ECMAScript 的下一个修订版中。

<p class="alert alert-primary"> ES 语法提案内容出之 segmentfault 社区的 zhangwang
<br>想要了解关于此内容更详细的信息请 <a target="_blank" href="https://segmentfault.com/a/1190000010074709" class="alert-link">点击此链接</a> 进行阅读</p>


### 实现

ECMAScript 是一个标准，而这个标准需要各个浏览器厂商去实现，不同浏览器厂商都会对该标准有着不同的实现方式，不同的浏览器有着不同的 JS 引擎，用来解析并执行 JS 代码，但是浏览器之间的引擎是不一样，所导致的实现效果也是有些区别，具体如下：

1. Mozilla 公司

   > 浏览器：FireFox
   >
   > JS 引擎：SpiderMonkey / TraceMonkey / JaegerMonkey
   >
   > 渲染引擎：Gecko

2. Microsoft 公司

   > 浏览器：IE6-8 / IE9-11
   >
   > JS 引擎：JScript / Chakra
   >
   > 渲染引擎：Trident

3. Microsoft 公司

   > 浏览器：Edge
   >
   > JS 引擎：Chakra
   >
   > 渲染引擎：Edge

4. Apple 公司

   > 浏览器：Safari
   >
   > JS 引擎：SquirrelFish Extreme
   >
   > 渲染引擎：Webkit

5. Google 公司

   > 浏览器：Chrome
   >
   > JS 引擎：V8
   >
   > 渲染引擎：Webkit / Blink

6. Opera 公司

   > 浏览器：Opera
   >
   > JS 引擎：Linear A/B / Futhark / Carakan
   >
   > 渲染引擎：Presto / Blink

