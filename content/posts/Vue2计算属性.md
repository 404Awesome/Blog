---
title: Vue2计算属性
toc: true
date: 2020-04-09 8:35:26
tags: ['Vue2']
---

# computed 简介

计算属性 (computed) 也是 options 对象中的一个属性

我们虽然可以直接在模板中使用插值语法来显示一些 data 中的数据，但是在某些情况下，我们需要对数据进行一些转化或计算过后再显示，我们可以通过 计算属性 (computed) 的例子，来看看

```html
<p>{{money}}</p>
```

```javascript
const temp = new Vue({
  el: "p",
  data: {
    USD: 100,
  },
  computed: {
    money() {
      return this.USD + "$";
    },
  },
});
```

上面代码来看，我们不难发现 Mustache 语法中的 money 没有使用 ( ) 括号进行调用，这是因为 money 是一个属性，并非是一个方法，上面的形式是简写形式，完整的计算属性拥有 get 和 set 方法，具体代码如下

```javascript
const temp = new Vue({
  el: "p",
  data: {
    USD: 100,
  },
  computed: {
    money: {
      set() {
        // function content
      },
      get() {
        return this.USD + "$";
      },
    },
  },
});
```

其中 set 方法很少使用，可以被省略，然后代码就会被简写成最上面的形式，所以 money 并非是一个方法，而是一个属性，后面的函数体，是 get 方法，set 方法如何使用，set 方法只有当该属性名内的值发生改变时，就会触发 set 方法，或者可以利用 set 方法改变值

# computed 和 methods 的区别

他们虽然最后的结果相差不大，但是性能却各不相同，每次使用由 methods 定义的方法求值时，就会调用一次该方法，而 computed 则不会，它会将值加入到缓存当中，以便于下次使用，若下次使用时，值没有发生改变，就不会去调用方法，直接取缓存中的值，如下

### methods

```html
<ul>
  <li>{{show()}}</li>
  <li>{{show()}}</li>
  <li>{{show()}}</li>
</ul>
```

```javascript
const temp = new Vue({
  el: "ul",
  methods: {
    show() {
      console.log("methods");
      return "Hello methods";
    },
  },
});
```

> 这时你会发现，控制台输出了三次 methods，也就是调用了 三次 show 方法

### computed

```html
<ul>
  <li>{{show}}</li>
  <li>{{show}}</li>
  <li>{{show}}</li>
</ul>
```

```javascript
const temp = new Vue({
    el: 'ul',
    computed: {
        console.log('computed');
    	return 'computed';
    }
});
```

> 这时控制台就会只输出一次
>
> 所以在某些场合下使用 computed 会更好
>
> 注意：不要将 methods 和 computed 混用，毕竟分工不同
