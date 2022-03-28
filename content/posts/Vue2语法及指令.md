---
title: Vue2语法及指令
toc: true
date: 2020-04-08 22:52:01
tags: ['Vue2']
---

# Mustache 语法

通过上几期文章，我们了解到想要将定义在 data 属性中的变量显示到网页中，通常需要用到 Mustache 语法，语法结构如下，

> &#123;&#123; 变量 / 表达式 &#125;&#125;

如果 Vue 读取到这种格式，会将括号内的语句当作命令执行，在括号内的变量也是可以进行计算的，比如加减乘除，但是需要注意的是使用加号，若两边有一方是字符串，将会和 JS 语法差不多，进行字符串拼接，这是需要注意的，其实除了使用 Mustache 语法可以将变量输出到页面中，还可以使用 Vue 指令，但是有时不如 Mustache 语法好用

# Vue 指令

> Vue 封装了一些功能，这些功能可以简化我们对 Dom 的操作

### v-once

这个指令会导致所在的 Dom 元素内的数据只会渲染一次，等加载完成后，再去修改数据，所对应的网页内容不会发生改变 ，也就是，所在的 Dom 元素内的数据不再是响应式，用法如下

```html
<p v-once>{{content}}</p>
```

### v-html

若我们从服务器请求下来的数据本身是一个 html 代码的话，我们希望，直接让他展示到页面当中，此时， v-html 指令就能够满足我们的需求，如下

```html
<div v-html="url"></div>
```

```javascript
const temp = new Vue({
  el: "div",
  data: {
    url: "<a href='www.suyuan5.top'>SuYuan5</a>",
  },
});
```

使用 v-html 指令，它便会将变量 url 中的内容当做 html 代码渲染到 div 中，需要注意的是，这个指令会覆盖 div 中已有的内容

### v-text

该指令的用途和 Mustache 语法相似，就是将变量的内容渲染到页面当中，渲染的过程中，只是将该变量的值当作一个普通字符串处理，不过该指令会和 v-html 指令一样，会将元素内已有的内容覆盖，如下

```html
<p v-text="content"></p>
```

```javascript
const temp = new Vue({
  el: "p",
  data: {
    content: "<h1>Hello World</h1>",
  },
});
```

### v-pre

若我们想要在页面中显示 &#123;&#123; 内容 &#125;&#125; 这样的内容，而不想让它被当做 Mustache 语法去解析的话，就可以用到 v-pre 指令，元素内的内容会原样渲染到页面当中

```html
<p v-pre>{{content}}</p>
```

### v-cloak

有时会因为网络加载过慢，导致有些 Mustache 语法，还没有被解析，就展示到了页面当中，为了防止这种现象，可以使用 v-cloak，如下

```css
[v-cloak] {
  display: none;
}
```

```html
<p v-cloak>{{content}}</p>
```

```javascript
setTimeout(() => {
  const temp = new Vue({
    el: "p",
    data: {
      content: "Hello Vue",
    },
  });
}, 2000);
```

上面的代码依次为 CSS，HTML，JS 代码，同时我们使用了 setTimeout 模拟了一下网络加载慢的情况，然后宁愿该元素在网络加载慢时，不展示到页面当中，也不要将未解析完成的 mustache 语法，直接展示到页面当中，影响用户体验

### v-for

这个指令一般用来遍历数组，也可以遍历对象，下面以数组为例，如下

```html
<ul>
  <li v-for="(item, index) in arr">{{item + ' ' + index}}</li>
</ul>
```

```javascript
const temp = new Vue({
  el: "ul",
  data: {
    arr: ["content1", "content2", "content3", "content4"],
  },
});
```

> 其中 item 是数组内的"元素"，而 index 是数组元素对应的"索引"，可以将它们当做变量在所在的作用域内使用

如果频繁操作数组元素，删除替换等操作时，可以为元素绑定一个 key，绑定完成后，在进行操作数组时，会由于 diff 算法的原因，优化了程序的性能，每个 key 的值都应该是独一无二的，同时绑定了 key 也表示该元素不再进行复用，例如切换两个表单元素时，在上个表单文本框内输入的值，就不会保留到切换后的表单文本框内，一般可以为 key 属性绑定遍历元素或者其索引，这里用到了 v-bind 指令，如下

```html
<ul>
  <li v-for="(item, index) in arr" v-bind:key="index + item">{{item}}</li>
</ul>
```

> Key 的作用主要是为了高效的更新虚拟 DOM


> 注意的是，如果遍历的是数组，则可以按照顺序取到数组元素及索引，但是遍历对象，则可以按照顺序取到对象的属性值，属性名，索引

### v-bind

v-bind 用于绑定一个或者多个属性值，或者向另一个组件传递 props 值( 组件 )， 这个指令可以绑定 Dom 元素的属性，如果我们不只是想让 Dom 元素的内容动态改变，也想让其属性也能动态改变，这个 v-bind 指令就可以做到，如下

```html
<main>
  <img v-bind:src="img" />
  <a v-bind:href="a"> {{content}} </a>
</main>
```

```javascript
const temp = new Vue({
  el: "main",
  data: {
    content: "Hello World",
    img: "www.suyuan5.top/xxx.jpg",
    a: "www.suyuan5.top/xxx.html",
  },
});
```

通过 v-bind 指令，我们为 img 标签的 src 属性和 a 标签的 href 属性绑定一个变量，这样一来，变量内的值就会当作绑定时属性的属性值，一般来说，该变量内存放的值，大多都是从服务器请求下来的，这样就可以动态的改变某张图片，或则某个链接的指向，Vue 还提供了 v-bind 的语法糖，可以在属性前面加上 : ，等同于在属性前面加上了 v-bind，往后的代码中，我们直接使用语法糖的形式来操作

#### 当 v-bind 遇上 class

可以使用 v-bind 动态的加载 class 类，分为对象形式和数组形式，常用对象形式，如下

> 对象形式

```html
<p :class="{'class1': isClass1, 'class2': isClass2}">{{content}}</p>
```

```javascript
const temp = new Vue({
  el: "p",
  data: {
    content: "Hello World",
    isClass1: true,
    isClass2: false,
  },
});
```

对象形式的结构为：&#123; 类名：布尔值 &#125; 的形式，根据布尔值，来决定前面的类名是否添加到 class 类当中，true 为添加，false 为不添加，如果 class 属性中的对象内的值比较多，还可以在 methods 或者 computed 中定义，然后将结果返回 return，这两个属性的区别在于，computed 不用加上 ( ) 括号调用，而 methods 则需要，如下

```html
<p :class="classes / getClass()">{{content}}</p>
```

```javascript
const temp = new Vue({
  el: "p",
  data: {
    content: "Hello World",
    isClass1: true,
    isClass2: false,
  },
  methods: {
    getClass() {
      return { class1: this.isClass1, class2: this.isClass2 };
    },
  },
  computed: {
    classes() {
      return { class1: this.isClass1, class2: this.isClass2 };
    },
  },
});
```

> 数组形式

一般来说并不如对象形式常用，如下

```html
<p :class="[value1, value2]">{{content}}</p>
```

```javascript
const temp = new Vue({
  el: "p",
  data: {
    content: "Hello World",
    value1: "class1",
    value2: "class2",
  },
});
```

显然使用数组形式起来不如对象灵活，当然，如果 class 属性中的数组内的值比较多，也可以使用 methods 属性或者 computed 属性返回

使用 v-bind 绑定的 class 属性在对象和数组形式下都可以和普通的 class 共存，如下

```html
<p class="class" :class="{'class1': isClass1}">{{content}}</p>
```

```html
<p class="class" :class="[class1]">{{content}}</p>
```

> 需要注意的是，一般来说，类名后面的布尔值是不会写死的，可以使用条件表达式返回一个布尔值，动态加载 class 类

#### 当 v-bind 遇上 style

v-bind 不仅可以动态绑定 class ，还可以动态绑定 style 样式，也分为对象形式和数组形式

> 对象形式

```html
<p :style="{color: getColor, fontSize: getFS + 'px'}">{{content}}</p>
```

```javascript
const temp = new Vue({
  el: "p",
  data: {
    content: "Hello World",
    getColor: "orangered",
    getFS: 100,
  },
});
```

HTML 代码中对象的形式为 &#123;属性名：属性值 &#125; 的形式，其中后面的 fontSize 是 css 样式中 font-size 的驼峰写法，虽然在对象中直接书写 font-size 为属性名，也可以识别，但是还是推荐使用驼峰写法，当对象内的值过多的时候，也可以使用 methods 或者 computed 返回值，如下

```html
<p :Style="getStyle() / styles">{{content}}</p>
```

```javascript
const temp = new Vue({
  el: "p",
  data: {
    content: "Hello World",
    getColor: "orangered",
    getFontS: 100,
  },
  methods: {
    getStyle() {
      return { color: this.getColor, fontSize: this.getFontS + "px" };
    },
  },
  computed: {
    styles() {
      return { color: this.getColor, fontSize: this.getFontS + "px" };
    },
  },
});
```

> 数组形式

使用数组形式的情况也不是特别多，但是还是要看一下，如下

```html
<p :style="[value1, value2]">{{content}}</p>
```

```javascript
const temp = new Vue({
  el: "p",
  data: {
    content: "Hello World",
    value1: { color: "orange" },
    value2: { fontSize: "100px" },
  },
});
```

当数组内的值多时，也可以使用 methods 属性和 computed 属性等返回

### v-on

#### 基本使用

如果我们需要监听一些事件，这时候就可以用到 v-on 指令了，当然这个指令也是有语法糖形式的，便于开发，如下

```html
<button v-on:click="function / JsCode">OK</button>
```

除了 click 点击事件还有 keyup 等事件，后面引号中即可以是方法又可以是 Js 代码，调用方法是有区别的，如下

1. 如果方法不传入参数的话，可以省略方法后面的括号，直接使用方法名
2. Vue 默认会将事件对象传入第一个形参当中
3. 若想传入参数，并且还需要事件对象的话，可以使用 $event 指定事件对象，如下

```html
<button v-on:click="show('Vue', $event)">OK</button>
```

```javascript
3const temp = new Vue({
    el: 'button',
    methods: {
        show (value, event){
            console.log(value, event);
            // pintf  -->  Vue eventObject
        }
    }
});
```

然后 Vue 还提供了语法糖的形式，如下

> 语法糖：简写形式
>
> v-on:click == @click

```html
<button @blur="show()">blur</button> <button @click="show()">click</button>
```

除了以上几种事件之外，还有许多，这里就不多说了

#### v-on 事件修饰符

在某些情况下，我们会拿到事件对象，然后做一些事件处理，比如取消默认事件等，所以 Vue 帮我们定义了一些常用的方法，就是 v-on 的修饰符，如下

1. .stop
   > 调用 event.stopPropagation( )
   >
   > 阻止冒泡事件
2. .prevent
   > 调用 event.preventDefault( )
   >
   > 取消默认事件
3. .capture

   > 添加事件侦听器时使用 capture 模式

4. .self

   > 只当事件是从侦听器绑定的元素本身触发时才触发回调

5. .{keyCode | keyAlias}
   > 只当事件是从特定键触发时才触发回调
   >
   > 键别名 .enter
6. .native

   > 监听组件根元素的原生事件
   >
   > 默认直接对组件添加事件是无效的，需要加上该修饰符，才可以

7. .once

   > 只触发一次回调

8. .left

   > (2.2.0) 只当点击鼠标左键时触发

9. .right

   > (2.2.0) 只当点击鼠标右键时触发

10. .middle

    > (2.2.0) 只当点击鼠标中键时触发

11. .passive

    > (2.3.0) 以 { passive: true } 模式添加侦听器

用法如下

```html
<button v-on:click.stop="show()">OK</button>
```

```html
<button @click.prevent="show()">OK</button>
```

在绑定事件后面添加上需要的修饰符，就能够帮我们完成一些事件处理，提升效率

有时我们还需要监听键盘事件 (keyup，keydown，keypress)，根据按下的键，来处理某些事情，Vue 也帮我们定义了一些常用的按键修饰符，如下

1. .enter
2. .tab
3. .delete 捕获 "删除" 和" 退格" 键
4. .esc
5. .space
6. .up
7. .down
8. .left
9. .right

### v-if / v-else / v-else-if

这三个和 Js 中的条件语句 if，else，else if 类似，根据表达式的值决定该 DOM 元素是否进行渲染或者进行销毁，需要注意的是这个指令会对 DOM 元素进行渲染和销毁操作，所以频繁调用会损耗性能

#### v-if

原理是 v-if 后面的条件为 false 时，对应的 DOM 元素以及子元素不会被渲染，而为 true 时，则进行渲染显示，如下

```html
<main v-if="false">
  <h1>Hello World</h1>
</main>
```

上面的案例就不会被渲染到页面当中，只有后面的条件表达式为 true 时，才会进行渲染，上面为了方便没有使用条件 ，直接使用的布尔值，与 v-if 对应的就是 v-else，如下

#### v-else

如果 v-if 为 false 时，v-if 所在的 DOM 元素不会渲染到页面当中，但是 v-else 所在的 DOM 元素则会进行渲染到页面，也就是如果 v-if 为 true，渲染 v-if 所在的 DOM 元素，不会渲染 v-else 所在的 DOM 元素，如果为 false，则反之，如下

```html
<main>
  <div v-if="false">
    <h1>Hello v-if</h1>
  </div>
  <div v-else>
    <h1>Hello v-else</h1>
  </div>
</main>
```

#### v-else-if

进行多个条件匹配，为 true 的显示，其余的不显示，后面跟表达式，返回的应该是一个布尔值，如下

```html
<div>
  <p v-if="score>=90">Very Good</p>
  <p v-else-if="score>=80">Good</p>
  <p v-else-if="score>=60">Pass</p>
  <p v-else>failed</p>
</div>
```

### v-show

v-show 的用法和 v-if 非常类似，也用于决定一个元素是否会被加载到页面当中，v-show 后面值是一个表达式，会返回一个布尔值，如果为 true 就显示，为 false 就不显示，如下

```html
<main v-show="true">
  <h1>Hello World</h1>
</main>
```

但是 v-show 和 v-if 是有区别的

1. v-if 当条件为 false 时，压根不会有对应的元素在 DOM 中
2. v-show 当条件为 false 时，仅仅是将元素的 display 属性设置为 none 而已

开发中如何选择

1. 当需要在显示与隐藏之间切换很频繁时，使用 v-show
2. 当只切换一次时，使用 v-if

### v-model

表单控件在实际开发中是非常常见的，特别是对于用户信息的提交，需要大量的表单，Vue 中使用 v-model 指令来实现表单元素和数据的双向绑定，例子如下

```html
<div class="model">
  <input type="text" v-model="message" />
  <h1>{{message}}</h1>
</div>
```

```javascript
const temp = new Vue({
  el: ".model",
  data: {
    message: " ",
  },
});
```

1. 当我们在表单文本框内输入文本时
2. 因为该表单中使用了 v-model 指令绑定了 message 变量，所以输入的内容会实时的传递给 message，因此 message 会发生变化
3. 当 message 内容发生改变时，绑定的表单元素内的值（value），也会发生改变，所以叫做双向绑定

当然也可以将 v-model 指令用于 textarea 文本域

#### v-model 原理

v-model 其实就是一个语法糖，它的背后实质上是包含两个操作

1. v-bind 绑定一个 value 值
2. v-on 指令给当前元素绑定 input 事件

#### v-model 遇上 radio

如果想要实现单选的话，无需添加 name 属性，直接使用 v-model 指令，值是一个变量，这个变量将存储着单选的结果

```html
<main>
  <label for="male">
    <input type="radio" id="male" value="male" v-model="sex" />男
  </label>
  <label for="female">
    <input type="radio" id="female" value="female" v-model="sex" />女
  </label>
  <h1>{{sex}}</h1>
</main>
```

```javascript
const temp = new Vue({
  el: "male",
  data: {
    sex: " ",
  },
});
```

此时选择其中一个单选按钮，那么该按钮的值就会被输出到 h1 标签中，想要有默认值的话，可以为 sex 变量赋上一个默认值

#### v-model 遇上 checkbox

想使用复选框，也无需定义 name 属性，我们定义了一个变量 ball 数组类型的，用来存储选中的选项，然后将选的结果输出到 h1 标签中

```html
<main>
  <input type="checkbox" value="football" v-model="ball" />football
  <input type="checkbox" value="basketball" v-model="ball" />basketball
  <input type="checkbox" value="volleyball" v-model="ball" />volleyball
  <input type="checkbox" value="badminton" v-model="ball" />badminton
  <h1>{{arr}}</h1>
</main>
```

```javascript
const temp = new Vue({
  el: "main",
  data: {
    ball: [],
  },
});
```

上面是一个多个复选框的例子，下面还有一个单个复选框的应用

```html
<main>
  <label for="agree">
    <input type="checkbox" id="agree" v-model="bool" />
    <span>agree or not</span>
  </label>
  <input type="button" value="next" :disabled="!bool" />
  <h1>{{bool}}</h1>
</main>
```

```javascript
const temp = new Vue({
  el: "main",
  data: {
    bool: false,
  },
});
```

#### 当 v-model 遇上 select

和 checkbox 一样，select 也分为单选和多选

单选：只能选定一个值

1. v-model 绑定的是一个值
2. 当我们选中 option 中的一个选项时，会将它对应的 value 赋值到 v-model 绑定的变量当中

多选：可以选中多个值

1. v-model 绑定的是一个数组
2. 当选着多个值时，就会将选中的 option 对应的 value 添加 v-model 绑定的数组变量中

不管是单选还是多选，v-model 指令绑定的是 select 标签，而不是 option 标签，如下

```html
<select name="fruit" v-model="fruit">
  <option value="apple">apple</option>
  <option value="banana">banana</option>
  <option value="pear">pear</option>
  <option value="orange">orange</option>
</select>
```

```javascript
const temp = new Vue({
  el: "select",
  data: {
    fruit: "apple", // default value
  },
});
```

上面就是 select 单选，v-model 会将选中选项的值赋给 fruit 变量 ，也可以根据变量 fruit 的值，为 select 下拉列表赋一个默认值，而多选，只是为变量 fruit 赋了一个数组字面量，然后给 select 标签添加了一个 multiple 属性，无属性值，注意多选时，需要按住 ctrl 进行多选

#### v-model 修饰符

修饰符有如下几种，作用和 v-on 指令的修饰符差不多，将一些常用功能利用简洁的写法实现，如下

1. lazy 修饰符
   > 默认情况下，v-model 默认是在 input 事件中同步输入框的数据的
   >
   > 频繁的同步会浪费性能，若我们不想让他实时的刷新数据，可以在 v-model 后面加上 .lazy，就可以实现懒加载，等表单元素失去焦点或者按下回车，才会去同步数据
2. number 修饰符

   > 表单元素的类型为 Number 时，只能输入数字，虽然是输入数字，但是最后得到的仍是字符串格式的数字，使用 .number 修饰符，可以得到 number 类型的数据

3. trim 修饰符

   > 这个修饰符可以去除输入内容两侧的空白，使用方法同上

### 值绑定

上述使用的表单元素，无论是单选按钮，还是复选框，其中的值都是写死的，而值绑定的概念就是动态的去绑定值，我们会用到 v-for 指令和 v-bind 指令，例子如下

```html
<main>
  <label v-for="item in fruit" for="item">
    <input type="checkbox" v-bind:value="item" :id="item" />
    <span> {{item}} </span>
  </label>
</main>
```

```javascript
const temp = new Vue({
  el: "main",
  data: {
    fruit: ["apple", "banana", "pear", "orange"],
  },
});
```

> 经过上述操作，我们就完成了值绑定，根据数组内元素的个数，动态的生成对应的表单
