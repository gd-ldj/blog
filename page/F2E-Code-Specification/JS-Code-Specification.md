## JS-Code-Specification
> 本规范基于ES6

### 编码风格
 + 缩进, 和html缩进保持一致，2或4个空格，团队保持一致即可；
 + 分号，统一以分号结束语句，可以避免JS引擎自动插入机制的怪异行为，语义上也更加明了；
 + 逗号，对于逗号分隔的多行结构，不使用行首逗号；并且始终加上最后一个逗号, 这样可以方便快捷的添加删除；
 ```
 // bad
var obj = {
    a: 1
  , b: 2
  , c: 3
};

// good
var obj = {
    a: 1,
    b: 2,
    c: 3,
};
 ```
 + 空格
   + 块的左大括号{前有一个空
 ```
 // bad
if (condition){
  ...
}

// good
if (condition) {
  ...
}

 // bad
cat.set('attr',{
  age: '1'
})

// good
cat.set('attr', {
  age: '1'
})
 ```
   + if / else / for / while / function / switch / do / try / catch / finally 关键字后，必须有一个空格。
 ```
 // bad
if(condition) {
  ...
}

// good
if (condition) {
  ...
}

 ```
   + 声明函数时，函数名和参数列表之间无空格。
 ```
 // bad
function cat (condition) {
 ...
}

// good
function cat(condition) {
 ...
}

 ```
   + 小括号、方括号内部两侧无空格, 大括号内部两侧有空格。
 ```
 // bad
function cat( condition ) {
 ...
}

// good
function cat(condition) {
 ...
}

 // bad
const foo = [ 1, 2, 3 ];

// good
const foo = [1, 2, 3];

 // bad
const obj = {age: 1}; 

// good
const obj = { age: 1 };

 ```
   + 除了一元运算符两侧无空格，其余运算符两侧有空格，。
 ```
 // bad
const x=y+1;

// good
const x = y + 1;


// bad
const x = ++ 1;

// good
const x = ++1;
 ```
   + 声明函数时，函数名和参数列表之间无空格。
 ```
 // bad
function cat (condition) {
 ...
}

// good
function cat(condition) {
 ...
}
 ```
   + 在对象创建时，属性中的 : 之后必须有空格，: 之前不允许有空格。
 ```
 // bad
{
 age   : 1,
 lenght:2,
}

// good
{
 age: 1,
 lenght: 2,
}
 ```
   + , 和 ; 前不允许有空格
```
 // bad
callFunc(a , b) ;

// good
callFunc(a, b);
 ```
 + 空行
   + 块的开始和结束不能是空行
 ```
 // bad
function cat(condition) {

 console.log(condition)
 
}

// good
function cat(condition) {
 console.log(condition)
}
 ```
   + 块末和新语句间插入一个空行
 ```
  // bad
if(condition) {
  return condition;
}
return far;

// good
if(condition) {
  return condition;
}

return far;

 // bad
const obj = {
  foo() {
  },
  baz() {
  },
}; 
return obj;

// good
const obj = {
  foo() {
  },
  
  baz() {
  },
}; 

return obj;
 ```
 + 换行
  + 每个独立语句结束后必须换行， 单行最大字符数推荐100字符，过长不易阅读和维护，但是字符串和正则表达式不要换行
  + 运算符处换行时，运算符必须在新行的行首
```


// bad
if (a &&
    b &&
    c ||
    d) {
    ...
}

// good
if (a
    && b
    && c
    || d
) {
    ...
}

```
### 语言特性

### 参考资料
 + [http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh](http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh) 
 + [https://www.w3cschool.cn/wematy/p2acvozt.html](https://www.w3cschool.cn/wematy/p2acvozt.html)
 + [https://juejin.im/post/599ececb5188252423583c27](https://juejin.im/post/599ececb5188252423583c27)
 + [https://guide.aotu.io/docs/html/code.html](https://guide.aotu.io/docs/html/code.html)
