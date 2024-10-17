# JavaScript 标准内置对象

## Proxy

Proxy 对象用于创建一个对象的代理，从而实现基本操作的拦截和自定义（如属性查找、赋值、枚举、函数调用等）。

### 语法

```js
const p = new Proxy(targe, handler)
```

参数：

`targe` ：要使用 `Proxy` 包装的目标对象（可以是任何类型的对象，包括原生数组、函数、甚至另一个代理）。

`handler` ：一个通常以函数作为属性的对象，各属性中的函数分别定义了在执行各种操作时代理 `p` 的行为。

### 方法

`Proxy.revocable()` 方法可以用来创建一个可撤销的代理对象。

### handeler functions (处理程序函数)

`handler` 对象是一个容纳一批特定属性的占位符对象。它包含有 `Proxy` 的各个捕获器（trap）。

所有的捕获器是可选的。如果没有定义某个捕获器，那么就会保留源对象的默认行为。





有空了，学习[JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)