## vue学习笔记  

Vue.js（读音 /vjuː/，类似于 view 的读音）是一套构建用户界面(user interface)的渐进式框架。与其他重量级框架不同的是，Vue 从根本上采用最小成本、渐进增量(incrementally adoptable)的设计。  

作者：尤雨溪，现居美国新泽西，全职开发维护vue，以及vue生态系统。  

官方团队成员：全职两个，尤雨溪、蒋豪群，还有很多全球各地的贡献者。  

Vue是从Angular优化而来， AngularJS 是 Vue 早期开发的灵感来源。然而，AngularJS 中存在的许多问题，在 Vue 中已经得到解决。后面又加入了虚拟dom。 

Vue.js是一个用于创建用户界面的开源JavaScript框架，也是一个创建单页面应用的Web应用框架。  

Vue的初始版本在2014年发布, 现在主流版本2.0  3.0版本今年即将发布  

Vue相对其它两大框架Angular、React的优势：体积小，易上手  

Vue的模版式语法，不同于React的JSX语法。Vue.js 的核心是，可以采用简洁的模板语法来声明式的将数据渲染为 DOM   

我们只需要关注于底层逻辑，更新应用程序的状态，而无需触及 DOM - 所有的 DOM 操作都由 Vue 来处理。

### 语法学习

#### Vue 实例
每个 Vue 应用程序都是通过 Vue 函数创建出一个新的 Vue 实例开始的
> 作为约定，通常我们使用变量 vm (ViewModel 的简称) 来表示 Vue 实例
```js
var data = { message: 'hello vue'}
var vm = new Vue({
  el: '#example', // 绑定作用域
  data: data,  // 组件状态数据
  created: function () { // 生命周期函数
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
  },
  methods: { // 自定义方法
    getData: function () {
      this.message = '你好 vue' // 可以修改状态数据
    }
  }，
  computed: {  // 计算属性
    // 一个 computed 属性的 getter 函数
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  },
    watch: { // 监听属性变化
    // 只要 message 发生改变，此函数就会执行
    message: function (newMessage, oldMessage) {
      // ...
    }
  },
})

// 除了 data 属性， Vue 实例还暴露了一些有用的实例属性和方法。这些属性与方法都具有前缀 $，以便与用户定义(user-defined)的属性有所区分
vm.$data === data // => true
vm.$el === document.getElementById('example') // => true

// $watch 是一个实例方法
vm.$watch('a', function (newValue, oldValue) {
  // 此回调函数将在 `vm.a` 改变后调用
})
```
> 在控制台里可以修改app.message的值
> 不要在选项属性或者回调函数中使用箭头函数（例如，created: () => console.log(this.a) 或 vm.$watch('a', newValue => this.myMethod())）。因为箭头函数会绑定父级上下文，所以 this 不会按照预期指向 Vue 实例，经常会产生一些错误  

生命周期示意图
![生命周期](https://vue.docschina.org/images/lifecycle.png)
所有的钩子函数在调用时，其 this 上下文都会指向调用它的 Vue 实例

#### 模板语法
Vue.js 使用基于 HTML 的模板语法，允许声明式地将要渲染的 DOM 和 Vue 实例中的 data 数据绑定  
在底层的实现上，Vue 将模板编译为可以生成 Virtual DOM 的 render 函数。结合响应式系统，在应用程序状态改变时，Vue 能够智能地找出重新渲染的最小数量的组件，并应用最少量的 DOM 操作。
+ 插值(Interpolations)
  + 文本(Text)
    数据绑定最基本的形式，就是使用 “mustache” 语法（双花括号）的文本插值
    ```js
    <span>{{ Message }}</span>
    ```
    mustache 标签将会被替换为 data 对象上对应的 msg 属性的值。只要绑定的数据对象上的 msg 属性发生改变，插值内容也会随之更新  
    也可以通过使用 v-once 指令，执行一次性插值，也就是说，在数据改变时，插值内容不会随之更新。但是请牢记，这也将影响到同一节点上的其他所有绑定
    ```js
    <span v-once>这里的值永远不会改变：{{ Message }}</span>
    ```
  + 原始 HTML(Raw HTML)
    双花括号语法，会将数据中的 HTML 转为纯文本后再进行插值。为了输出真正的 HTML，你需要使用 v-html 指令：
    ```js
    <p>使用双花括号语法：{{ rawHtml }}</p>
    <p>使用 v-html 指令：<span v-html="rawHtml"></span></p>
    ```
    > 在网站中动态渲染任意的 HTML 是非常危险的，因为这很容易导致网站受到 XSS 攻击。请只对可信内容使用 HTML 插值，绝对不要对用户提供的内容使用 HTML 插值。
  + 属性(Attributes)
    ```html
    <div v-bind:id="dynamicId"></div>
    ```
  + 使用 JavaScript 表达式
    Vue.js 实际上能够支持通过完整的 JavaScript 表达式，将模板与任意的数据绑定在一起
    ```js
    {{ number + 1 }}

    {{ ok ? 'YES' : 'NO' }}

    {{ message.split('').reverse().join('') }}

    <div v-bind:id="'list-' + id"></div>
    ```
    每个绑定都只能包含单个表达式，所以以下示例都无法运行
    ```js
    <!-- 这是语句，不是表达式 -->
    {{ var a = 1 }}

    <!-- 流控制也无法运行，请使用三元表达式 -->
    {{ if (ok) { return message } }}
    ```

  + 指令系统
    v-都是vue封装好的指令，可以直接绑定到DOM上使用
    ```js
    <p v-if="seen">Now you see me</p>
    ```
    + v-bind：传递属性  简写 :
    + v-if 控制元素的显示
    + v-for 遍历数组的元素展示
    + v-on:  绑定事件 简写 @
    + v-model 表单输入和应用程序状态之间的双向绑定

  + 参数(Arguments)
    一些指令能够接收一个“参数”，在指令名称之后以 : 表示
    ```js
    <a v-bind:href="url"> ... </a>
    <a v-on:click="doSomething"> ... </a>
    ```
  + 修饰符(Modifiers)
    修饰符(modifier)是以 . 表示的特殊后缀，表明应当以某种特殊方式绑定指令。
    ```js
    <form v-on:submit.prevent="onSubmit"> ... </form>
    // .prevent 修饰符告诉 v-on 指令，在触发事件后调用 event.preventDefault()
    ```
### computed 属性和 watcher
+ computed
  像绑定普通属性一样，可以将 computed 属性的数据，绑定(data-bind)到模板中的表达式上。  
  computed的属性依赖于data的属性，data的属性变化时，computed的对应属性也会变化  
  computed 属性会基于它所依赖的数据进行缓存。每个 computed 属性，只有在它所依赖的数据发生变化时，才会重新取值(re-evaluate)。  
  这就意味着，只要 message 没有发生变化，多次访问 computed 属性 reversedMessage，将会立刻返回之前计算过的结果，而不必每次都重新执行函数  
+ watcher
 Vue 要通过 watch 选项，来提供一个更加通用的响应数据变化的方式。  
 当你需要在数据变化响应时，执行异步操作，或高性能消耗的操作，自定义 watcher 的方式就会很有帮助
### class 和 style 绑定
+ class
  在使用 v-bind 指令来处理 class 和 style 时，Vue 对此做了特别的增强。表达式除了可以是字符串，也能够是对象和数组
  ```js
  // active 这个 class 的存在与否，取决于 isActive 这个 data 属性的 truthy 值
  <div v-bind:class="{ active: isActive }"></div>
  
  // 可以通过在对象中添加多个字段，来切换多个 class。此外，v-bind:class 指令也可以和普通 class 属性共存,串联式命名要加引号
  <div class="static" v-bind:class="{ active: isActive, 'text-danger': hasError }"> </div>
  
  // 绑定对象，也可以无需内联，而是外部引用 data
  // 还可以将 class 和 style 与某个 computed 属性绑定在一起，此 computed 属性所对应的 getter 函数需要返回一个对象
  <div v-bind:class="classObject"></div>
  data: {
    classObject: {
      active: true,
      'text-danger': false
    }
  }
  // or
  data: {
  isActive: true,
  error: null
  },
  computed: {
    classObject: function () {
      return {
        active: this.isActive && !this.error,
        'text-danger': this.error && this.error.type === 'fatal'
      }
    }
  }
  // 向 v-bind:class 传入一个数组  
  <div v-bind:class="[activeClass, errorClass]"></div>
  
  // 根据条件，切换 class 列表中某个 class，可以通过三元表达式
  <div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
  
  // 当你在自定义组件中使用 class 属性，这些 class 会被添加到组件的根元素上。根元素上已经存在的 class 不会被覆盖
  Vue.component('my-component', {
    template: '<p class="foo bar">Hi</p>'
  })
  <my-component class="baz boo"></my-component>
  ```
  + style
  v-bind:style 的对象语法是非常简单直接的 - 看起来非常像 CSS，其实它是一个 JavaScript 对象。CSS 属性名称可以使用驼峰式(camelCase)或串联式(kebab-case)（使用串联式需要加引号）：
  ```js
  data: {
    activeColor: 'red',
    fontSize: 30
  }
  <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
  
  // 通常，一个比较好的做法是，直接与 data 中的 style 对象绑定，这样模板看起来更清晰
  data: {
    styleObject: {
      color: 'red',
      fontSize: '13px'
    }
  }
  <div v-bind:style="styleObject"></div>
  
  // v-bind:style 的数组语法，可以在同一个元素上，使用多个 style 对象
  <div v-bind:style="[baseStyles, overridingStyles]"></div>
  
  // 在 v-bind:style 中使用具有浏览器厂商前缀(vendor prefixes)的 CSS 属性时（例如 transform），Vue 会自动检测并向 style 添加合适的前缀。
  // 你可以为每个 style 属性提供一个含有多个（前缀）值的数组，最终，这只会从数组中找出「最后一个浏览器所支持的值」进行渲染
  <div v-bind:style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
  ```  
  
#### v-if 和 v-show

v-if 是“真实”的条件渲染，因为它会确保条件块(conditional block)在切换的过程中，完整地销毁(destroy)和重新创建(re-create)条件块内的事件监听器和子组件。

v-if 是惰性的(lazy)：如果在初始渲染时条件为 false，它不会执行任何操作 - 在条件第一次变为 true 时，才开始渲染条件块。

相比之下，v-show 要简单得多 - 不管初始条件如何，元素始终渲染，并且只是基于 CSS 的切换。

通常来说，v-if 在切换时有更高的性能开销，而 v-show 在初始渲染时有更高的性能开销。因此，如果需要频繁切换，推荐使用 v-show，如果条件在运行时改变的可能性较少，推荐使用 v-if。  
+ v-if  

v-if 可以配合 v-else 、v-else-if使用。v-else必须紧跟在 v-if 或 v-else-if 元素之后 - 否则无法识别它
由于 v-if 是一个指令，因此必须将其附加到一个单独的元素上。但是如果我们想要切换多个元素呢？在这种场景中，我们可以将 <template> 元素，作为多个元素的无形容器  
  使用 key 控制元素是否可复用
  ```js
    <template v-if="loginType === 'username'">
      <label>用户名</label>
      <input placeholder="请输入用户名" key="username-input">
    </template>
    <template v-else>
      <label>邮箱</label>
      <input placeholder="请输入邮箱" key="email-input">
    </template>
    // label 元素仍然被有效地复用，因为它们没有 key 属性。
  ```  
  
 + v-show
  具有 v-show 的元素会始终渲染并保留在 DOM 中。v-show 只会切换元素的 display 这个 CSS 属性。
  > 注意，v-show 无法用于 template 元素，也不能和 v-else 配合使用。  
  

#### v-if 和 v-show
使用 v-for 指令，将一个数组渲染为列表项。v-for 指令需要限定格式为 item in items 的特殊语法，其中，items 是原始数据数组(source data array)，而 item 是数组中每个迭代元素的指代别名(alias)：  
v-for 还支持可选的第二个参数，作为当前项的索引    

可以不使用 in，而是使用 of 作为分隔符，因为它更加接近 JavaScript 迭代器语  
也可以使用 v-for 来遍历对象的属性。  
可以提供第二个参数，作为对象的键名(key)
> 在遍历一个对象时，是按照 Object.keys() 得出 key 的枚举顺序来遍历，无法保证在所有 JavaScript 引擎实现中完全一致。  
使用v-for时，最好都要加上:key
```js
<ul id="example-1">
  <li v-for="item in items">
    {{ item.message }}
  </li>
</ul>

<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>

<div v-for="item of items"></div>

<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>

<div v-for="(value, key) in object">
  {{ key }}: {{ value }}
</div>

<div v-for="(value, key, index) in object">
  {{ index }}. {{ key }}: {{ value }}
</div>

<div v-for="item in items" :key="item.id">
  <!-- content -->
</div>
```
#### 组件系统
> 在 Vue 中，一个组件本质上是一个被预先定义选项的 Vue 实例

注册组件
```vue
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: '蔬菜' },
      { id: 1, text: '奶酪' },
      { id: 2, text: '其他人类食物' }
    ]
  }
})
```
使用组件
```vue
<todo-item
  v-for="item in groceryList"
  v-bind:todo="item"
  v-bind:key="item.id">
</todo-item>
```
> 组件的 data 选项必须是一个函数，以便每个实例都可以维护「函数返回的数据对象」的彼此独立的数据副本
没有遵循这个规定，操作其中一个组件，会影响其他所有用到此 data 的组件实例  
+ 使用 props 向子组件传递数据
+ 使用 events 向父组件发送消息
+ 在组件中使用 v-model 实现组件的数据双向绑定
