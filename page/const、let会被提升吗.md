## const、let是ES6的新特性，可以声明块级作用域
+ 到底会不会声明被提升，现在说法不一，主流是不会被提升
+ 个人认为也不会被提升，但是和var一样不能先使用再声明
+ var 声明的变量会被提升到顶部，再赋值
   ```javascript
   console.log(a) // undefined
   var a = 1
   ```
 + const、let会在声明地方到块级顶部形成临时性死区，在这区间使用该变量都会被报错
   ```javascript
   console.log(a) // VM92:1 Uncaught SyntaxError: Identifier 'a' has already been declared
   let a = 1
  ```
