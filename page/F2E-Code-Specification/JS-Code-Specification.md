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
+ 变量声明
  + 使用const、let声明变量，尽量不再使用var
  + 优先使用const，只有当变量会被重新赋值时才使用let
  + 声明数组或者对象时，多数使用const，因为对数组和对象的改变并不是重新赋值
  + 声明的变量和表达式必须被使用，声明但未被使用的变量，表达式，会给维护者造成困扰，可能会带来潜在的问题
  + 哪里使用，哪里声明，这样易于阅读，不会存在声明提升问题
  + const和let归类写在一起，便于阅读
  + 一条声明语句声明一个变量，这样易于增加或者删除
  ```
  // bad
  const foo = 1,
        baz = 2;
        
  // good
  const foo = 1;
  const baz = 2;
  ```
  + 禁止连续赋值，难以阅读和理解，还会导致意想不到的问题
  ```
  // bad
  let foo = baz = 2;
        
  // good
  let foo = 1;
  let baz = foo;
  ```
   + 变量不要与外层作用域已存在的变量同名，如果存在变量同名，会降低可读性，也会导致内层作用域无法读取外层作用域的同名变量
  ```
  // bad
  const foo = 2;
  if (flag) {
    const foo = 2;
    console.log(foo) // => 2
  }
        
  // good
   const foo = 2;
  if (flag) {
    const baz = 1;
    console.log(foo) // => 2
    console.log(baz) // => 1
  }
  ```
    + 不要重复声明变量和函数，ES6中重复声明const、let会直接报错，重复声明var不会报错，也不要重复声明
  ### 布尔值
  + 类型转换使用 !!
   ```
  // bad
  const foo = 0;
  const baz = Boolean(foo);
        
  // good
  const foo = 0;
  const baz = !!foo;
  ```
   + 在if等条件语句中，将表达式的值强制转化为boolean是多余的
   ```
  // bad
  if (!!foo) {
    ...
  }
  const baz = !!foo ? 0 : 1;
        
  // good
   if (foo) {
    ...
  }
  const baz = foo ? 0 : 1;
  ```
 ### 数组
 + 直接使用字面量创建数组，除非是构造具体长度的空数组
  ```
  // bad
  const foo = Array(1, 2);
  const baz = new Array(1, 2);
        
  // good
  const foo = [1, 2];
  const baz = new Array(200);
  ```
  + 数组复制使用扩展运算符...
  ```
  // bad
  const foo = [1, 2];
  const baz = [];
  for (let i = 0; i < foo.length; i++) {
    baz[i] = foo[i];
  }
        
  // good
  const foo = [1, 2];
  const baz = [...foo];
  ```
  + 数组拼接用扩展运算符
  ```
  // bad
  const foo = [1, 2];
  const baz = [3].concat(foo);
 
  // good
  const foo = [1, 2];
  const baz = [3, ...foo];
  ```
  + 用解构方法获取数组元素
  ```
  // bad
  const foo = [1, 2, 3];
  const first = foo[0];
  const second = foo[2];
 
  // good
  const foo = [1, 2, 3];
  const {frist, second} = foo;
  ```
  ### 对象
 + 直接使用字面量创建对象
  ```
  // bad
  const obj = new Object();
        
  // good
  const obj = {};
  ```
  + 对象的属性名不要使用单引号，除非包含特殊字符
  ```
  // bad
  const obj = {
    'foo': 1,
    'data-baz': 2,
  };
        
  // good
  const obj = {
    foo: 1,
    'data-baz': 2,
  };
  ```
  + 优先使用.访问对象的属性，可以提高代码的可读性。在访问动态属性名或包含特殊字符的属性时使用[]
  ```
  // bad
  const obj = {
    foo: 1,
    'data-baz': 2,
  };
  const key = obj['foo'];
        
  // good
  const obj = {
    foo: 1,
    'data-baz': 2,
  };
  const key = obj['data-baz'];
  ```

### 参考资料
 + [http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh](http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh) 
 + [https://www.w3cschool.cn/wematy/p2acvozt.html](https://www.w3cschool.cn/wematy/p2acvozt.html)
 + [https://juejin.im/post/599ececb5188252423583c27](https://juejin.im/post/599ececb5188252423583c27)
 + [https://guide.aotu.io/docs/html/code.html](https://guide.aotu.io/docs/html/code.html)
