## React 编码规约

### 基本
+ 每个文件只写一个组件，但是多个无状态组件可以放到单个组件中

### 组件
+ 有内部状态，方法或者是要对外暴露的ref组件，使用ES6 Class写法
```js
// bad 
const Listing = React.createClass({
  // ...
  render() {
    return <div>{this.state.text}</div>
  }
})

// good
class Listing extends React.Component {
// ...
  render() {
    return <div>{this.state.text}</div>
  }
}
```
+ 没有内部状态，方法或者无需对外暴露ref的组件，使用函数的写法
```js
// bad 
class Listing extends React.Component {
  render() {
    return <div>{this.state.text}</div>
  }
}

// good
const Listing = ({ text }) => (
  <div>{text}</div>
)
```
### PropTypes/DefaultProps
