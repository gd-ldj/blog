## JS-Code-Specification
> 本规范基于ES6

### 编码风格
 + 缩进, 和html缩进保持一致，2或4个空格，团队保持一致即可；
 + 分号，统一以分号结束语句，可以避免JS引擎自动插入机制的怪异行为，语义上也更加明了；
 + 逗号，对于逗号分隔的多行结构，不使用行首逗号；并且始终加上最后一个逗号, 这样可以方便快捷的添加删除；
 ```javascript
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
   + 块的左大括号 { 前有一个空
 ```javascript
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
 ```javascript
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
 ```javascript
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
 ```javascript
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
 ```javascript
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
 ```javascript
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
 ```javascript
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
```javascript
 // bad
callFunc(a , b) ;

// good
callFunc(a, b);
 ```
 + 空行
   + 块的开始和结束不能是空行
 ```javascript
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
 ```javascript
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
```javascript
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
  ```javascript
  // bad
  const foo = 1,
        baz = 2;
        
  // good
  const foo = 1;
  const baz = 2;
  ```
  + 禁止连续赋值，难以阅读和理解，还会导致意想不到的问题
  ```javascript
  // bad
  let foo = baz = 2;
        
  // good
  let foo = 1;
  let baz = foo;
  ```
   + 变量不要与外层作用域已存在的变量同名，如果存在变量同名，会降低可读性，也会导致内层作用域无法读取外层作用域的同名变量
  ```javascript
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
 + 布尔值
   + 类型转换使用 !!
 ```javascript
  // bad
  const foo = 0;
  const baz = Boolean(foo);
        
  // good
  const foo = 0;
  const baz = !!foo;
 ```
   + 在if等条件语句中，将表达式的值强制转化为boolean是多余的
   ```javascript
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
+ 数组
  + 直接使用字面量创建数组，除非是构造具体长度的空数组
  ```javascript
  // bad
  const foo = Array(1, 2);
  const baz = new Array(1, 2);
        
  // good
  const foo = [1, 2];
  const baz = new Array(200);
  ```
   + 数组复制使用扩展运算符...
  ```javascript
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
  ```javascript
  // bad
  const foo = [1, 2];
  const baz = [3].concat(foo);
 
  // good
  const foo = [1, 2];
  const baz = [3, ...foo];
  ```
   + 用解构方法获取数组元素
  ```javascript
  // bad
  const foo = [1, 2, 3];
  const first = foo[0];
  const second = foo[2];
 
  // good
  const foo = [1, 2, 3];
  const {frist, second} = foo;
  ```
+ 对象
  + 直接使用字面量创建对象
  ```javascript
  // bad
  const obj = new Object();
        
  // good
  const obj = {};
  ```
   + 对象的属性名不要使用单引号，除非包含特殊字符
  ```javascript
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
  ```javascript
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
+ 函数
   + 不要用Function构造函数创建函数，使用new Function创建函数会像eval方法一样执行字符串，带来安全隐患
  ```javascript
  // bad
  const fun = new Function('a', 'b', 'return a + b');
        
  // good
  const fun = (a, b) => (a + b);
  ```
   + 使用函数表达式代替函数声明，这样可以保证函数不能在定义前被调用。
  ```javascript
  // bad
  function fun() {
    ...
  }
        
  // good
  const fun = () => {
    ...
  }
  const fun = function () {
    ...
  }
  
  ```
   + 在非函数块if、while等中，不要使用函数声明。
  ```javascript
  // bad
  if (flag) {
    function fun() {
      console.log('inFun');
    }
  }
  fun(); // => inFun
        
  // good
  //不能在块外调用
   if (flag) {
    const fun = function () {
      console.log('inFun');
    }
  }
  fun(); // => fun is not defined
  
  //能在块外调用
  let fun;
   if (flag) {
     fun = function () {
      console.log('inFun');
    }
  }
  fun(); // => inFun
  ```
   + 使用箭头函数代替匿名函数，箭头函数不仅解决了this的指向问题，而且语法简洁。
  ```javascript
  // bad
  [1].map(function (x) {
    ...
  })
        
  // good
  [1].map((x) => {
    ...
  })
  
  ```
   + 不要使用arguments对象，使用剩余参数操作符...代替。
  ```javascript
  // bad
  function fun(a) {
    const args = Array.prototype.slice.call(arguments, fun.length);
    console.log(args);
  }
  fun(1, 2, 3); // => [2, 3]
        
  // good
  function fun(a, ...args) {
    console.log(args);
  }
  fun(1, 2, 3); // => [2, 3]
  
  ```
   + 使用ES6的默认参数，当函数需要默认值时，使用默认参数语法，不要去给参数赋值。
  ```javascript
  // bad
  function fun(a) {
    a = a || 0;
    ...
  }
        
  // good
  function fun(a = 0) {
    ...
  }
  ```
   + 有默认值的函数参数需要放到参数列表的最后，这样才能使用默认参数的便利，否则要传undefined触发参数使用默认值。
  ```javascript
  // bad
  function fun(a = 1, b) {
    console.log(a, b);
  }
  fun(2); // => 2 undefined
        
  // good
  function fun(b, a = 1) {
    console.log(b, a);
  }
  fun(2); // => 2 1
  ```
   + 不要修改参数的值。
  ```javascript
  // bad
  function fun(a) {
    if (!a) {
      a = 1;
    }
  }
        
  // good
  function fun(obj) {
    let b = a;
    if (!a) {
      b = 1
    }
  }
  ```
   + 函数的参数不要过多，当参数较多时，使用对象代替参数列表。
  ```javascript
  // bad
  function fun(a, b, c, d, e) {
    ...
  }
  fun(1, 2, 3, 4, 5);
        
  // good
  function fun({a, b, c, d, e}) {
    ...
  }
  fun({a: 1, b: 2, c: 3, d: 4, e: 5});
  ```
+ 类
 + 不要再直接操作prototype，使用class语句声明类，用ES6的语法糖，更加简洁且易于维护
 ```javascript
  // bad
  function fun() {
    this.age = 1;
  }
  fun.prototype.say = function () {
    this.age += 1;
  }
        
  // good
  class fun() {
    constructor() {
      this.age = 1;
    }
    say() {
      this.age += 1;
    }
  }
  ```
  + 使用extend语句进行类的继承，extends是用于原型继承的内建方法，不会破坏instanceof
 ```javascript
  class sen extends far {
    ...
  }
  ```
  + 空construtor或者只调用父类的construtor是没必要的
 ```javascript
  // bad
  class far() {
    construtor() {
    }
    method() {
      ...
    }
  }
  class sen extends far {
    construtor (value) {
      super(value);
    }
    method() {
     ...
    }
  }
        
  // good
   class far() {
    method() {
      ...
    }
  }
  class sen extends far {
    method() {
     ...
    }
  }
  ```
 + 模块
  + 使用ES6的 modules的import/export
  ```javascript
  // bad
  const React = require('react');
  module.exports = React.Component;
        
  // good
   import React, { Compontent } from 'react';
   export default Component;
  ```
   + import语句放到模块的最顶部，import语句会声明提升，防止异常，把他们放到模块上方；
  ```javascript
  // bad
  import foo from 'foo';
  foo.init();
  
  import baz from 'baz';
  baz.init();
        
  // good
  import foo from 'foo';
  import baz from 'baz';
  foo.init();
  baz.init();
  ```
  
  + 操作符
    + 使用严格相等运算符，当要比较的两个值类型不同时，应该将其转换成相同类型再进行比较，不要依赖==和!=的隐式转换，
   ```javascript
  // bad
  const a = '123';
  if (a == 123) {
    ...
  }
  
  // good
  const a = '123';
  if (Number(a) === 123) {
    ...
  }
  ```
   + 避免嵌套三元表达式，嵌套会降低代码的可读性
   ```javascript
  // bad
 const aa = b ? c : d === e ? f : g;
  
  // good
  const bb = d === e ? f : g;
  const aa = b ? c : bb;
  ``` 
   + 避免不必要的三元表达式
   ```javascript
  // bad
 const aa = a ? a : b;
 const bb = b ? true : false;
 const cc = c ? false : true;
  
  // good
 const aa = a || b;
 const bb = !!b;
 const cc = !c;
  ``` 
   + 混合使用多种操作符，用小括号分组，能够清楚的表达代码的意图
   ```javascript
  // bad - 有些人会认为先 a || b
 if (a || b && c) {
   ...
 }
  
  // good
 if (a || (b && c)) {
   ...
 }
  ``` 
  ### 注释
  > 注释的目的，提高代码的可读性
  > 注释的原则，如无必要，请勿注释，如有必要，请必详尽
  + 单行注释使用 //
  + 多行注释使用 /** */，而不是多行 //
  + 注释符要和注释内容之间留一个空格
  + 合理的使用注释标记 // FIME    // TODO
  ```javascript
  /**
  * @title
  * @auther
  */
 function book() {
   // 单行注释
   ...
   // TODO: 执行
 }
  ``` 
 ### 命名
 + 命名要有语义，不要使用单个字符命名
  ```javascript
  // bad
 function g() {
   ...
 }
 
  // good
 function get() {
   ...
 }
  ``` 
   + 使用小驼峰命名对象、函数、实例
  ```javascript
  // bad
 function get_data() {
   ...
 }
 
  // good
 function getData() {
   ...
 }
  ``` 
    + 使用大驼峰命名类和构造函数
  ```javascript
  // bad
 function user() {
   this.name = 'name';
 }
 
  // good
 function User() {
   this.name = 'name';
 }
  ``` 
### 参考资料
 + [http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh](http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh) 
 + [https://www.w3cschool.cn/wematy/p2acvozt.html](https://www.w3cschool.cn/wematy/p2acvozt.html)
 + [https://juejin.im/post/599ececb5188252423583c27](https://juejin.im/post/599ececb5188252423583c27)
 + [https://guide.aotu.io/docs/html/code.html](https://guide.aotu.io/docs/html/code.html)
