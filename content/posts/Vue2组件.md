---
title: Vue2组件
toc: true
date: 2020-04-13 15:20:45
tags: ['Vue2']
---

# 什么是组件化

### 复杂问题的处理方式

1. 任何一个人处理信息的逻辑能力都是有限的
2. 所以，当面对一个非常复杂的问题时，我们不太可能一次性搞定一大堆的内容
3. 如果将一个复杂的问题，拆分成多个可以处理的小问题，再将其放在整体当中，你会发现大的问题也会迎刃而解

### 组件化思想

1. 如果我们将一个页面中所有的处理逻辑全部放在一起， 处理起来就会变得非常复杂，而且不利于后续的管理一级扩展
2. 但如果，我们将一个页面拆分成一个个小的功能块，每个功能块完成属于自己的这部分独立的功能，那么之后整个页面的管理和维护就变的非常容易

# Vue 组件化思想

### 介绍

1. 它提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用
2. 组件化是 Vue.js 中的重要思想
3. 任何的应用都会被抽象成一颗组件树，如下

<img src="/img/post/vue2/组件树.png">

### 组件化思想的应用

1. 有了组件化的思想，我们在之后的开发中就要充分的利用它
2. 尽可能的将页面拆分成一个个小的，可复用的组件
3. 这样让我们的代码更加方便组织和管理，并且扩展性也更强

# 注册组件基本步骤

组件的使用分成以下三个步骤

1. 创建组件构造器

   > 通过 Vue.extend( ) 创建组件构造器

2. 注册组件

   > 通过 Vue.component( ) 注册组件

3. 使用组件

   > 根据注册的标签名进行使用

例子如下

```html
<main>
  <cpn></cpn>
</main>
```

```javascript
const myCpn = Vue.extend({
  template: `
		<div>
			<h1>Hello Vue</h1>
			<p>Lorem ipsum dolor sit</p>
		</div>
	`,
});
Vue.component("cpn", myCpn);
const temp = new Vue({
  el: "main",
});
```

经过上述操作便可以在页面中看到 Hello Vue 等字样，其中 Vue.extend 是创建组件，Vue.component 是用来注册组件的，还有就是组件构造器中 template 属性可以配合模板字面量，这些 HTML 代码需要在一个根节点下面，否则解析失败，上述代码中 div 就是一个根节点，此外 Vue.component( ) 方法内有两个参数，第一个是注册的标签名，第二个是组件构造器的引用，除了上面代码的那种写法之外，还有语法糖格式的，可以将组件构造器的创建与注册进行简写，如下

```javascript
Vue.component("cpn", {
  template: `
		<div>
			<h1>Hello Vue</h1>
		</div>
	`,
});
```

其中注册组件还分为

1. 全局注册

   > 如上所示代码的 Vue.component 注册组件的方式，是全局注册，进过全局注册的组件可以在所有组件中直接使用

2. 局部注册

   > 通过局部注册的组件，只能在当前组件下使用，使用属性 components 进行注册，注意是复数，如下

   ```javascript
   const myCpn = Vue.extend({
     template: `
   		<div>
   			<h1>Hello Vue</h1>
   			<p>Lorem ipsum dolor sit</p>
   		</div>
   	`,
   });
   
   const temp = new Vue({
     el: "main",
     data: {
       content: "Hello World",
     },
     components: {
       cpn: myCpn,
     },
   });
   ```

> 需要注意的是注册组件所使用的标签名称应该全部为小写形式，可以使用连字符，不能使用驼峰写法，因为 HTML 无法解析

### 注册组件语法糖

#### 注册全局组件

可以简写为以下代码

```javascript
Vue.component("cpn", {
  template: `
    	<div>
    		<h1>Hello World</h1>
    	</div>`,
});
```

虽然看起来是没有用到 Vue.extend( )，但是底层还是调用的 Vue.extend( ) 方法实现的

#### 注册局部组件

可以简写为以下代码

```javascript
const temp = new Vue({
  el: "main",
  data: {
    content: "Hello Vue",
  },
  components: {
    cpn: {
      template: `
				<div>
					<h1>Hello Vue</h1>
				</div>	`,
    },
  },
});
```

以上两种方式注册的组件内 template 模板属性后面的 HTML 代码看起来有些臃肿，有两种方式可以组件模板与 Js 代码相分离，如下

### 模板分离

#### script

使用 script 标签创建组件模板，如下

```html
<script type="text/x-template" id="myCpn">
  <div>
     	<h1>Hello Vue</h1>
     </div>
</script>
```

```javascript
const temp = new Vue({
  el: "main",
  data: {
    content: "Hello World",
  },
  components: {
    cpn: {
      template: "#myCpn",
    },
  },
});
```

以上是使用注册局部组件的方式演示的，全局组件如上形式，在 template 属性后面跟上组件模板的 id 名

#### template

使用 template 标签创建组件模板和使用 script 一样，只不过换了个标签，如下

```html
<template id="myCpn">
  <div>
    <h1>Hello Vue</h1>
  </div>
</template>
```

Js 代码同使用 script 标签模板的一样，在 template 属性后面跟上 id 名

# 步骤解析

### 1. Vue.extend( )

> 调用 Vue.extend( ) 创建的是一个组件构造器
>
> 通常在创建组件构造器时，传入 template 代表我们自定义的组件模板
>
> 该模板就是在使用组件的地方，要显示的 HTML 代码
>
> 事实上，这种写法在 Vue2.x 的文档中几乎已经看不到了，他会直接使用语法糖格式，但是还是会有很多资料提到这种方式，而且这种方式是学习后面方式的基础

### 2. Vue.component( )

> 调用 Vue.component( ) 是将刚才的组件构造器注册为一个组件，并且给它起一个组件的标签名称
>
> 所以需要传递的两个参数：1. 注册组件的标签名 2. 组件构造器 {全局注册}，局部注册则不需要

### 3. 使用

> 如果是全局组件，可以在所有使用 Vue 实例管理的 Dom 元素下使用，如果为局部组件，就必须在注册 Vue 实例对应的 Dom 下使用

# 组件数据的存放

目前来看我们创建的组件，内部使用的数据都是写死的，如果我们想要通过变量来获取数据，该如何操作，其实组件内不止有 template 属性，还可以有 data methods 等，但是需要注意的是 data 并非是一个对象类型的，而是一个工厂函数，通过这个函数返回一个带有数据的对象，以全局组件为例，如下

```javascript
Vue.component("cpn", {
  template: `
		<div>
			<h1> {{content}} </h1>
		</div>
	`,
  data() {
    return {
      content: "Hello Vue",
    };
  },
});
```

为什么需要这样做，先看如下代码

```html
<main>
  <cpn></cpn>
  <cpn></cpn>
  <cpn></cpn>
</main>
```

当使用多个同样组件时，若 data 是对象类型，则这些组件使用的是数据是指向一个内存地址的，也就是操作的都是一个对象，这样一来，就无法保证它们之间的数据互相独立，但是使用函数的话，每使用一次组件，都会由函数返回一个内存地址不同的对象，这样一来，不管使用几次组件，都不会相互影响了

# 父组件和子组件

#### 在前面我们看到了组件树

1. 组件与组件之间存在着层级关系
2. 而其中一种非常常见的关系就是父子组件关系

我们还可以创建多个组件，让他们有顺序的嵌套在一起，然后注册父级组件，然后展示到页面，注册在组件内的组件，为所在组件的子组件，而所在的组件为父组件，可以嵌套多层 ，例子如下

```javascript
const child = Vue.extend({
  template: `
		<div>
			<h2>Hello Son</h2>
		</div>
	`,
});

const parent = Vue.extend({
  template: `
		<div>
			<h1>Hello Father</h1>
			<son></son>
		</div>
	`,
  components: {
    son: child,
  },
});

const temp = new Vue({
  el: "main",
  data: {},
  components: {
    cpn: parent,
  },
});
```

从上代码看的出来，parent 中定义了 components 属性，然后通过 components 属性将 child 子组件注册成局部组件，然后又将 parent 注册到根组件上，也就是 Vue 实例，我们可以把 Vue 实例当做根组件

# 父子组件通信

一般情况下，子组件是无法访问父组件的 data 数据的

但是，在开发中，往往一些数据是需要从上层传递到下层的

1. 比如在一个页面，我们从服务器请求到了很多数据
2. 其中一部分数据，并非是我们整个页面的大组件来展示的，而是需要下面的子组件进行展示
3. 这个时候，并不会让子组件再次发送一个网络请求，而是直接让大组件( 父组件)将数据传递给小组件(子组件)

如何进行父子组件之间的通信，如下

1. 通过 props 向子组件传递数据
2. 通过事件向父组件发送信息

<img src="/img/post/vue2/父子通信.png">

### 父传子

可以使用 props 属性，这个属性有两种方式，一种是数组，一种是对象，为了方便我们在一个 Vue 实例中注册局部组件

```html
<main>
  <cpn v-bind:mytext="content"></cpn>
</main>

<template id="myCpn">
  <div>
    <h1>{{mytext}}</h1>
  </div>
</template>
```

```javascript
const temp = new Vue({
  el: "main",
  data: {
    content: "Hello World",
  },
  components: {
    cpn: {
      template: "#myCpn",
      props: ["mytext"],
    },
  },
});
```

上面在组件实例中使用 props 属性，值是一个数组类型，但是数组类型的并不常用，常用的是对象类型，这里我们将定义好的属性 mytext，在自己组件上使用，还是使用了 v-bind 指令，将父元素上的变量 content 的值，传了过来，这里若只想传过来一个普通字符串，就不必使用 v-bind 指令了

对象类型还分为两种，如下

```javascript
const temp = new Vue({
  el: "main",
  data: {
    content: "Hello World",
  },
  components: {
    cpn: {
      template: "#myCpn",
      props: {
        mytext: String,
      },
    },
  },
});
```

对象内属性 mytext 对象的值是对 props 做数据验证，关于这个后面在做讲解，这个 mytext 变量还可以是一个对象形式的，如果是对象形式的话，还能设置默认值等， 如下

```javascript
const temp = new Vue({
  el: "main",
  data: {
    content: "Hello World",
  },
  components: {
    cpn: {
      template: "#myCpn",
      props: {
        mytext: {
          type: String,
          default: "Hello Vue",
          required: true,
        },
      },
    },
  },
});
```

其中 type 属性是对 props 做数据验证，default 是设置默认值，若没有传值过来，就使用默认值，required 属性是表示是否必需为该变量传值，属性值是布尔值，true 是必传，false 则不是，默认是 false

如果 type 属性是 Array / Object 时，默认值需要通过函数返回，如下

```javascript
myarr: {
    type: String,
    default (){
        return ['value1', 'value2'];
    }
}
```

如果设置了该变量必需传值，这时候默认值就无需设置了，需要注意是 props 对象中的属性名可以使用驼峰写法，但是在使用 v-bind 传值时，使用了驼峰写法的变量应该使用 - 代替，单词全部为小写，如下

```html
"myCpn" --> "my-cpn"
```

### props 数据验证

在前面我们的 props 选项使用过数组写法，除了数组之外，还可以使用对象，当需要对 props 进行类型等验证时，就需要对象写法了

验证都支持如下几种数据类型

1. String
2. Number
3. Boolean
4. Array
5. Object
6. Date
7. Function
8. Symbol

使用数据验证可以对传入的值进行判断

### 子传父

子传父使用 $emit 来传输数据，还需要一个事件来决定何时向父组件发送数据，下面使用表单来演示

```html
<main>
  <cpn v-on:message="receive"></cpn>
</main>
<template id="mycpn">
  <div>
    <input type="text" v-on:input="send" />
  </div>
</template>
```

```javascript
const temp = new Vue({
  el: "main",
  data: {
    content: "",
  },
  methods: {
    receive(value) {
      this.content = value;
    },
  },
  components: {
    cpn: {
      template: "#mycpn",
      methods: {
        send(event) {
          this.$emit("message", event.target.value);
        },
      },
    },
  },
});
```

在上方代码中子组件通过 input 事件调用定义好的 send 方法，在 $emit 中有两个参数，第一个是事件名称，第二个是传入的数据，定义好事件名称后，在 Vue 实例管理的 Dom 元素中，我们看到使用了 cpn 这个组件，在这个组件中我们使用定义好的事件 message ，然后值是一个方法 receive，这个方法定义在父组件中，也就是目前的 Vue 实例，这个方法有一个参数，是系统将之前 $emit 中的第二参数传了过来，这个使用一个形参变量来接收，然后为 Vue 实例中的变量 content 赋值

> 总的来说，父组件向子组件传递数据使用 props 属性，而子组件向父组件传递数据使用 $emit
>
> 在真实开发中，Vue 实例和子组件的通信和父组件和子组件的通信过程是一样的

# 父子组件的访问方式

有时候我们需要父组件直接访问子组件，子组件直接访问父组件，或则是子组件直接访问根组件，如下

1. 父组件访问子组件：使用 $children 或者 $refs
2. 子组件访问父组件：使用 $parent
3. 子组件访问根组件：使用 $root

### $children

```html
<main>
  <cpn></cpn>
  <button v-on:click="show">OK</button>
</main>
```

```javascript
const temp = new Vue({
  el: "main",
  methods: {
    show() {
      console.log(this.$children[0].content);
    },
  },
  components: {
    cpn: {
      template: "#mycpn",
      data() {
        return {
          content: "Hello $children",
        };
      },
    },
  },
});
```

使用 $children 会返回一个含有子组件的数组，通过下标进行选择，然后访问组件内的数据 data，及调用方法，打开控制台即可看到输出的信息，如果所有的子组件都需要遍历，使用 $children 是挺好的，但是只需要对其中一个确定的子组件进行操作时，使用下标进行选取，就有了不确定性，比如中间增加了一个子组件，这时数组的长度和下标就发生的改变，所以推荐使用 $refs，如下

### $refs

默认情况下访问 $refs 的话，是一个空数组，通过对子组件添加一个属性 ref ，后面跟上一个名称，这时，我们再访问 $refs ，就不再是一个空数组了，与 $children 不同的是，$children 是通过下标访问的，而 $refs 是通过 ref 后面定义的名称访问的，这样即使数组发生改变，也不会影响到对某个子组件的访问了，如下

```html
<main>
  <cpn ref="child"></cpn>
  <button v-on:click="show">OK</button>
</main>
```

```javascript
const temp = new Vue({
  el: "main",
  methods: {
    show() {
      console.log(this.$refs.child.content);
    },
  },
  components: {
    cpn: {
      template: "#mycpn",
      data() {
        return {
          content: "Hello $refs",
        };
      },
    },
  },
});
```

### $parent

通过在子组件里定义了一个按钮，调用一个 show 方法，方法内使用 $parent 打印父组件的变量 content 和调用父组件的 show 方法，如下

```html
<main>
  <cpn></cpn>
</main>
<template id="mycpn">
  <div>
    <button v-on:click="show">OK</button>
  </div>
</template>
```

```javascript
const temp = new Vue({
  el: "main",
  data: {
    content: "Hello Father",
  },
  components: {
    cpn: {
      template: "#mycpn",
      methods: {
        show() {
          console.log(this.$parent.content);
        },
      },
    },
  },
});
```

### $root

如果父子组件之间嵌套的过多，想要在多层子组件里面直接访问根组件内的数据，可以将以上代码中 $parent 换为 $root，即可，用法如上

> 后面我们会使用 Vue 脚手架，来组件化开发
