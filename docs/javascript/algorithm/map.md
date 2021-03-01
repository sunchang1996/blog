## 字典是什么
与集合类似，字典也是一种存储唯一值的数据结构，但它是以 “键值对” 的形式来存储。

ES6 中有字典， Map

常用操作： 键值对的增删改查

```js
const m = new Map()

// 增
m.set('a', 'aa')

// 删
m.delete('a')
// 删除所有
m.clear()

// 改
m.set('a', 'bb')
```