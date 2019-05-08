## 为什么null的typeof 是object呢？

typeof 返回的正常类型，是这样的
+ typeof 对于基本类型，除了 null 都可以显示正确的类型
```javascript
typeof 1 // 'number'
typeof '1' // 'string'
typeof undefined // 'undefined'
typeof true // 'boolean'
typeof Symbol() // 'symbol'
typeof b // b 没有声明，但是还会显示 undefined
```
+ typeof 对于对象，除了函数都会显示 object
```javascript
typeof [] // 'object'
typeof {} // 'object'
typeof console.log // 'function'
```
为什么对于基本类型的null 却返回了object呢
+ 对于 null 来说，虽然它是基本类型，但是会显示 object，这是一个存在很久了的 Bug
```javascript
typeof null // 'object'
```
js的bug ？？？ 究竟是什么样的bug

> 为什么会出现这种情况呢？因为在 JS 的最初版本中，使用的是 32 位系统，为了性能考虑使用低位存储了变量的类型信息，000 开头代表是对象，然而 null 表示为全零，所以将它错误的判断为 object 。虽然现在的内部类型判断代码已经改变了，但是对于这个 Bug 却是一直流传下来。

为了避免这种问题，我们可以通过 Object.prototype.toString.call(xx)进行判断类型
