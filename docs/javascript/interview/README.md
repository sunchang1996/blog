# JavaScript 概念题目

## 什么是作用域 ？
- <font color="#f28500">浏览器给代码的执行环境，可以理解为是一个作用域</font>

## 什么是私有作用域
- 一个函数执行，会产生一个私有的作用域，用来提供JS代码执行的环境

## 什么是作用域链
- <font color="#f28500">在私有的作用域中，当执行遇到变量时，首先会在私有作用域中查找，如果没有，会往上级作用域查找，一直找到 window为止，这种查找方式就叫做”作用域链“</font>

## 什么是闭包？
- <font color="#f28500"> 简单理解为，一个函数就是一个闭包。</font>函数形成私有作用域保护了里面的变量不受外面干扰，外面不能修改，这种机制就叫”闭包“

## js 执行 this 的几种情况
1. 给元素绑定事件 tag.onclick = fucntion(){} this 是 tag
2. 自执行函数的 this  是 window
3. 函数执行前的主体如 fn() -> this 是 window， obj.fn() -> this 是 obj
4. 当构造函数运行的时候，this 就是当前构造函数创建的示例。

## 介绍下观察者模式和订阅-发布模式的区别，各适应于什么场景
### 观察者模式
> 观察者模式在软件中是一个对象，维护一个依赖列表，但任何状态发送改变自动通知他们。
- 假如你正在找工作，对某个大厂 A 感兴趣。你联系了 A 的 HR 给了他你的联系方式，有合适的工作时，会通知你。 这里可能还有其他几位候选人也感兴趣，所以职位空缺大家都知道，如果你回应了他们的通知，HR 就会联系你去面试。
- 上面观察者模式的关系， A 公司就是 subject ，用来维护 Observer （和你一样的候选人），为某些 event（职位的空缺） 来 通知（notify）观察者。

### 发布-订阅设计模式
- 在观察者模式中 Subject 就像一个发布者，观察者 Observer 完全和订阅者 Subscriber 关联。subject 通知观察者就像一个发布者通知他的订阅者。这也就是发布-订阅 概念来解释观察者设计模式。但是这里还有另外一个流行的模式叫做发布-订阅设计模式。它的概念和观察者模式非常类似。
- 发布-订阅模式，消息的发送发，叫发布者（publishers），消息不会直接发送给特定的接受者，叫做订阅者。
- 意思是发布者和订阅者不知道对方的存在。需要一个第三方组件，叫做”信息中介“，它将订阅和发布者串联起来，它过滤的分配所有输入的消息。发布-订阅模式用来处理不同系统组件的信息交流，即使这些组件不知道对方的存在。

### 总结
- <font color="#f28500"> 在观察者模式中，观察者是知道 Subject的，Subject 一直保持对观察者进行记录。然而 发布订阅模式中，”发布者和订阅者不知道对象的存在“，它们只有通过消息代理进行通信。</font>
- 在发布订阅模式中，<font color="#f28500">组件是松散耦合的，正好和观察者模式相反。</font>
- <font color="red">> 观察者模式大多数时候是同步的，</font>例如：当事件触发，Subject 就会去调用观察者的方法。<font color="#f28500">而 ”发布-订阅“模式大多数的时候是异步的（使用消息队列）</font>
- <font color="#f28500">观察者 模式需要在单个应用程序地址空间中实现，</font><font color="red">而发布-订阅更像交叉应用模式。</font>

## 浏览器和Node事件循环的区别
- 微任务和宏任务在Node的执行顺序
  - Node 10以前：
  > 执行完一个阶段的所有任务，执行完nextTick队列里面的内容，然后执行完微任务队列的内容
  - Node 11以后：
  > <font color="red"> 和浏览器的行为统一了，都是每执行一个宏任务就执行完微任务队列。</font>

## var let const 的区别
> let 不存在变量提升，不能重复定义，会产生块级作用域
> const 声明就得赋值，变量的值不能改动 称为 ”暂时性死区“

## CommonJs 中的 require/exports  和  ES6 中的 import/export 区别？
- CommonJS 模块的重要特性是加载时执行，即脚本代码在 require 的时候，就会全部执行，一旦出现某个模块被”循环加载“，就只输出已经执行的部分，还未执行部分不会输出
- ES6 模块是动态引用，如果使用 import 从一个模块加载变量，那些变量不会被缓存，而是成为一个指向被加载模块的引用，需要开发者自己保证，真正取值的时候能够取到值。
- import/export 最终都是编译为 require/exports 来执行
- CommonJS 规范规定，每个模块内部，module 变量带边当前模块。这个变量是一个对象，它的 exports 属性（module.exports）是对外的接口。加载某个模块，其实是加载该模块的 module.exports 属性
- export 命令对应的是对外的接口，必须与模块内部的变量建立 -- 对应关系

## SetTimout 、Promise、Async / Await 的区别
- 三种方式在事件循环中的区别，事件循环中分别为宏任务队列和微任务队列。

### SetTimeout
- 回调函数放到宏任务队列中，等到执行栈清空以后执行

### promise 
- promise.then 里的回调函数会放到宏任务的微任务队列里，等宏任务执行完里面的同步代码在执行。

### async await
- async 函数表示函数里面可能有异步方法，await 后面跟一个表达式，async 方法执行时，遇到 await 会立即执行表达式，然后把表达式后面的代码放到微任务队列里，让出执行栈让同步代码先执行（也就是执行微任务）。


## 介绍下重绘和回流（Repaint & Reflow），以及如何进行优化
### 浏览器渲染机制
1. 浏览器采用流式布局模型（flow based loyout）
2. 浏览器会把 HMTL 解析成 DOM，把 CSS 解析成 CSSOM，DOM 和 CSSOM 合并就产生了渲染树（Render Tree）
3. 有了 Render Tree ，就知道了所有的节点样式，然后计算他们在页面上大小的位置，最后把节点绘制到页面上。
4. 由于浏览器使用流式布局，对 Render Tree 的计算通常只需要遍历一次就可以完成，但 Table 及其内部元素除外，他们可能需要多次计算，通常要化3倍于同等元素的计算，这也就是为什么要避免使用 table 布局原因之一。

### 重绘
- 由于节点的几何属性发生改变或者由于 样式发生改变，但不会影响布局。称为重绘， 例如outline，visibility，color，background-color 等，重绘的代价是高昂的，因为浏览器必须验证 DOM 数上其它节点元素的可见性。

### 回流
- 回流是布局或者几何属性需要改变就称为回流。回流是影响浏览器性能的关键因素，因为其变化涉及到部分页面（或是整个网页）的布局更新。一个元素的回流可能导致了其所有子元素以及 DOM 中紧跟其后的节点，祖先节点元素的随后回流。
> 回流必定发生重绘，重绘不一定会引发回流。

### 浏览器优化
- 现代浏览器大多都是通过队列机制来批量更新布局，浏览器会把修改操作放在队列中，至少一个浏览器刷新（即16.6ms）才会清空队列，但当你获取布局信息的时候，队列中可能有会影响这些属性或方法返回值的操作，即使没有，浏览器也会强制清空队列，触发回流与重绘来确保返回正确的值。
主要包括以下属性或方法：
```js
offsetTop、offsetLeft、offsetWidth、offsetHeight
scrollTop、scrollLeft、scrollWidth、scrollHeight
clientTop、clientLeft、clientWidth、clientHeight
width、height
getComputedStyle()
getBoundingClientRect()
```
- 所以应该避免频繁的使用上面的属性，它们都会强制渲染刷新队列。

### 减少重绘与回流
#### css
- 使用 transform 代替 top
- 使用 visibility 替换 display: none ，因为前者只会引起重绘，后者会引发回流（改变了布局
- 避免使用table布局，可能很小的一个小改动会造成整个 table 的重新布局。
- 尽可能在DOM树的最末端改变class，回流是不可避免的，但可以减少其影响。尽可能在DOM树的最末端改变class，可以限制了回流的范围，使其影响尽可能少的节点。
- 避免设置多层内联样式，CSS 选择符从右往左匹配查找，避免节点层级过多。
```html
<div>
  <a> <span></span> </a>
</div>
<style>
  span {
    color: red;
  }
  div > a > span {
    color: red;
  }
</style>
```
- 对于第一种设置样式来说，浏览器只需要找到页面中所有的 span 设置颜色，而第二种，浏览器首先找到 span ，然后找到 a 标签，最后找到 div 标签，然后对符合要求的设置颜色，这样递归过程复杂。使用时应当避免写过去具体的 css 选择器，然后减少 HTML无意义的标签，保证层级扁平。

- 将动画效果应用到 position 属性为 ansolute 或 fixed 元素上，避免影响其他元素的布局，这样知识一个重绘，而不是回流，同时控制动画速度可以选择 requestAnimationFrame
- 避免使用CSS表达式，可能会引发回流。
- 将频繁重绘或者回流的节点设置为图层，图层能够阻止该节点的渲染行为影响别的节点，例如will-change、video、iframe等标签，浏览器会自动将该节点变为图层。

- CSS3 硬件加速（GPU加速），使用css3硬件加速，可以让transform、opacity、filters这些动画不会引起回流重绘 。但是对于动画的其它属性，比如background-color这些，还是会引起回流重绘的，不过它还是可以提升这些动画的性能。

#### JavaScript
- 避免频繁操作样式，最好一次性重写style属性，或者将样式列表定义为class并一次性更改class属性。
- 避免频繁操作DOM，创建一个documentFragment，在它上面应用所有DOM操作，最后再把它添加到文档中。
- 避免频繁读取会引发回流/重绘的属性，如果确实需要多次使用，就用一个变量缓存起来。
- 对具有复杂动画的元素使用绝对定位，使它脱离文档流，否则会引起父元素及后续元素频繁回流

## 有下面3个判断数组的方法，请分别介绍它们之间的区别和优劣 Object.prototype.toString.call() 、 instanceof 以及 Array.isArray()
### Object.prototype.toString.call()
- 每一个继承 Object 的对象都有 toString()方法，如果 toString() 方法没有重写的话，会返回 [Object type], 其中 type 是对象的类型。但当除了 Object 类型的对象外，其他类型直接使用 toString 方法时，会直接返回都是内容的字符串，所以我们需要使用call或者apply方法来改变toString方法的执行上下文。
```js
const an = ['Hello','An'];
an.toString(); // "Hello,An"
Object.prototype.toString.call(an); // "[object Array]"
```
- 这个方法对于所有基本数据类型都可以进行判断，即使 null 和 undefined
```js
Object.prototype.toString.call('An') // "[object String]"
Object.prototype.toString.call(1) // "[object Number]"
Object.prototype.toString.call(Symbol(1)) // "[object Symbol]"
Object.prototype.toString.call(null) // "[object Null]"
Object.prototype.toString.call(undefined) // "[object Undefined]"
Object.prototype.toString.call(function(){}) // "[object Function]"
Object.prototype.toString.call({name: 'An'}) // "[object Object]"
```
- Object.prototype.toString.call() 常用于判断浏览器内置对象时。

### instanceof 
- instanceof  的内部机制是通过判断对象的原型链中是不是能找到类型的 prototype。
- 使用 instanceof判断一个对象是否为数组，instanceof 会判断这个对象的原型链上是否会找到对应的 Array 的原型，找到返回 true，否则返回 false。
```js
[]  instanceof Array; // true
```
但 instanceof 只能用来判断对象类型，原始类型不可以。并且所有对象类型 instanceof Object 都是 true。
```js
[]  instanceof Object; // true
```

### Array.isArray()
- 用来判断对象是否为数组
- instanceof 与 isArray 比较
    - 当检测 Array实例时，Array.isArray 由于 instanceof,因为 Array.isArray 可以检测出 iframes
    ```js
    var iframe = document.createElement('iframe');
    document.body.appendChild(iframe);
    xArray = window.frames[window.frames.length-1].Array;
    var arr = new xArray(1,2,3); // [1,2,3]

    // Correctly checking for Array
    Array.isArray(arr);  // true
    Object.prototype.toString.call(arr); // true
    // Considered harmful, because doesn't work though iframes
    arr instanceof Array; // false

    ```
- Array.isArray() 与 Object.prototype.toString.call()
    - Array.isArray()是ES5新增的方法，当不存在 Array.isArray() ，可以用 Object.prototype.toString.call() 实现。
    ```js
    if (!Array.isArray) {
        Array.isArray = function(arg) {
            return Object.prototype.toString.call(arg) === '[object Array]';
        };
    }

    ```
### 性能上
- Array.isArray 的性能最好， instanceof 比 toString.call 稍微好一点

## call 和 apply 的区别是什么？ 哪个性能更好一些
- Function.prototype.apply 和 Function.prototype.call 的作用是一样的，区别在于传入参数的不同；
#### 相同点
- 第一个参数都是，指定函数体内 this 的指向。

#### 不同点
- 第二个参数开始不同
  - apply 传入带下标的集合，即可以是数组（array）也可以是类数组，apply 把它传给函数作为参数。
  - call 第二个参数的参数固定，都会传递给函数作为参数

> call比apply的性能要好，平常可以多用call, 特别是es6的reset解构的支持，call基本可以代替apply.

## 为什么通常在发送数据埋点请求的时候使用的是 1x1 像素的透明 gif 图片？
1. 能够完成整个 HTTP 请求+响应（尽管不需要响应内容）
2. 触发 GET 请求之后不需要获取和处理数据、服务器也不需要发送数据
3. 跨域友好
4. 执行过程无阻塞
5. 相比 XMLHttpRequest 对象发送 GET 请求，性能上更好
GIF的最低合法体积最小（最小的BMP文件需要74个字节，PNG需要67个字节，而合法的GIF，只需要43个字节）

## 箭头函数和普通函数的区别
1. 不绑定 arguments 对象，也就是说在箭头函数内访问 arguments 对象会报错；
2. 不能用作构造器，也就是说不能通过关键字 new 来创建实例；
3. 默认不会创建 prototype 原型属性；
4. 不能用作 Generator() 函数，不能使用 yeild 关键字。
