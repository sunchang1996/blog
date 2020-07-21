# JavaScript 概念题目

## 什么是作用域 ？
- 浏览器给代码的执行环境，可以理解为是一个作用域

## 什么是私有作用域
- 一个函数执行，会产生一个私有的作用域，用来提供JS代码执行的环境

## 什么是作用域链
- 在私有的作用域中，当执行遇到变量时，首先会在私有作用域中查找，如果没有，会往上级作用域查找，一直找到 window为止，这种查找方式就叫做”作用域链“

## 什么是闭包？
- 简单理解为，一个函数就是一个闭包。函数形成私有作用域保护了里面的变量不受外面干扰，外面不能修改，这种机制就叫”闭包“

## js 执行 this 的几种情况
1. 给元素绑定事件 tag.onclick = fucntion(){} this 是 tag
2. 自执行函数的 this  是 window
3. 函数执行前的主体如 fn() -> this 是 window， obj.fn() -> this 是 obj
4. 当构造函数运行的时候，this 就是当前构造函数创建的示例。
