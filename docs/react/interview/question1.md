# 类组件和函数组件的区别
问这个问题，面试官主要想了解：
- 对组件的两种编写模式是否了解
- 是否具备在合适的场景下选用合适的技术栈的能力。

#### 共同点
他们的实际用途都是一样的，无论是高阶组件还是异步加载，都可以用它们作用基础组件展示 UI。也就是作用组件本身的所有基础功能都是一致的。（类组件可以改为函数组件，函数也可以改为类组件）

#### 不同点
- 类组件是基于 OOP（面向对象编程），所以它有继承、有属性、有内部状态的管理。
- 函数组件的根基是 FP，也就是函数式编程。它属于”结构化编程“的一种，与数学函数思想类似。也就是假定输入与输出存在某种特定的映射关系，那么输入一定的情况下，输出必然是确定的。
想较于类组件，函数组件更纯粹、简单、易测试、这是他们本质上的最大不同。

类组件和函数组件有个最经典的问题，就是 this 的问题，类组件中 this 存在一定的模糊性，容易引起错误。函数组件在同一个闭包中，不会有这样的问题。

#### 独有能力
类组件可以通过生命周期包装业务逻辑，这是类组件所”特有的“

#### 性能优化
- 类组件的优化主要依靠 shouldComponentUpdate 函数去阻断渲染。
- 而函数组件很一般靠 React.memo 来优化。

#### 未来的趋势
”类组件“的模式并不能很好的适应未来的趋势
  - this 的模糊性
  - 业务逻辑散落在生命周期中
  - React 的组件代码缺乏标准的拆分方式。
而使用 Hooks 的函数组件可以提供比原先更细粒度的逻辑组织复用，且能更好地适应时间切片与并发模式。

### 总结
1. 作用组件而言，类组件与函数组件在使用与呈现上并没有任何不同，性能上在现代浏览器中也不会有明显差异。
2. 它们在开发时的心智模型上却存在巨大的差异。类组件是基于面向对象编程的，它主打的是继承、生命周期等核心概念；而函数组件内核是函数式编程，主打的是 immutable、没有副作用、引用透明等特点。

3. 之前在使用场景上，如果存在需要使用生命周期的组件，那么主推类组件；设计模式上，如果需要使用继承，那么主推类组件。现在由于 React Hooks 的推出，生命周期的概念的淡出，函数组件可以完全取代类组件。其次继承并不是组件最佳的设计模式，官方更推崇”组由于继承“的设计概念，所以类组件在这方面的优势也在淡出。

4. 性能优化上，类组件主要依靠 shouldComponentUpdate 阻断渲染来提升性能，而函数组件依靠 React.memo 缓存渲染结果来提升性能。

5. 从上手程度而言，类组件更容易上手，从未来趋势上看，由于React Hooks 的推出，函数组件成了社区未来主推的方案。

6. 类组件在未来时间切片与并发模式中，由于生命周期带来的复杂度，并不易于优化。而函数组件本身轻量简单，且在 Hooks 的基础上提供了比原先更细粒度的逻辑组织与复用，更能适应 React 的未来发展。
