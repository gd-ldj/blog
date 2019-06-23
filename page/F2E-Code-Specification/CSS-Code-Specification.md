 
 ## CSS-Code-Specification

### 基本规约
+ 缩进, 和html缩进保持一致，2或4个空格；
+ 在每个声明块的左括号前添加一个空格
```css
/* bad */
.element{
  width: 20px;
}

/* good */
.element {
  width: 20px;
}
```
+ 每个声明块的右括号应单独成行
```css
/* bad */
.element {
  width: 20px;}

/* good */
.element {
  width: 20px;
}
```
+ 每条声明语句的：后应有一个空格，前没有空格
```css
/* bad */
.element {
  width:20px;
}

/* good */
.element {
  width: 20px;
}
```
+ 每条声明语句都应；结尾
```css
/* bad */
.element {
  width: 20px
}

/* good */
.element {
  width: 20px;
}
```
#### 空格
+ 以下几种情况不需要空格：
  + 属性名后
  + 多个规则的分隔符','前
  + !important '!'后
  + 属性值中'('后和')'前
  + 行末不要有多余的空格
+ 以下几种情况需要空格：
  + 属性值前
  + 选择器'>', '+', '~'前后
  + '{'前
  + !important '!'前
  + @else 前后
  + 属性值中的','后
```css
/* bad */
.element {
    color :red! important;
    background-color: rgba(0,0,0,.5);
}

/* good */
.element {
    color: red !important;
    background-color: rgba(0, 0, 0, .5);
}

/* bad */
.element ,
.dialog{
    ...
}

/* good */
.element,
.dialog {

}

/* bad */
.element>.dialog{
    ...
}

/* good */
.element > .dialog{
    ...
}

/* bad */
.element{
    ...
}

/* good */
.element {
    ...
}

/* bad */
@if{
    ...
}@else{
    ...
}

/* good */
@if {
    ...
} @else {
    ...
}
```


### 命名规约
+ 类名使用小写字母，以中划线分隔
+ id采用驼峰式命名
```css
/* bad */
.element_box {
  width:20px;
}
.elementBox {
  width:20px;
}

/* good */
.element-box {
  width: 20px;
}
```
### 选择器规约
+ 不使用通用选择器 *
+ 不使用 ID 选择器
+ 不使用无具体语义定义的标签选择器
```css
/* bad */
*{}
#jdc {}
.jdc div{}

/* good */
.jdc {}
.jdc li {}
.jdc li p{}
```
+ 为选择器分组时，将单独的选择器单独放在一行
```css
/* bad */
.element, .element-mod {
  width: 20px;}

/* good */
.element,
.element-mod {
  width: 20px;
}
```
+ 为选择器中的属性添加双引号
```css
/* bad */
.element[type=text] {
  width: 20px
}

/* good */
.element[type="text"] {
  width: 20px;
}
```
+ 建议选择器的层级不要超过5级
```css
/* bad */
.element .top .left .conetent .dox .txt {
  width: 20px
}

/* good */
.conetent .dox .txt {
  width: 20px;
}
```

### 属性规约
#### 属性顺序
+ 布局定位属性：display / position / float / clear / visibility / overflow
+ 自身属性：width / height / margin / padding / border / background
+ 文本属性：color / font / text-decoration / text-align / vertical-align / white- space / break-word
+ 其他属性（CSS3）：content / cursor / border-radius / box-shadow / text-shadow / background:linear-gradient …
> 定位可以从正常的文档流中移除元素，还能覆盖盒模型相关的样式，因此排在最前面，文本属性只影响元素的细节样式变化，排在下面
```css
/* bad */
.element {
  width: 20px;
  font-size: 16px;
  position: absolute;
  display: block;
  top: 0;
  left: 0;
  line-height: 1.5;
  z-index: 2;
  padding: 20px;
}

/* good */
.element {
  /* 布局定位 */
  display: block;
  position: ablosute;
  top: 0;
  left: 0;
  z-index: 2;
  /* 自身 */
  width: 20px;
  padding: 20px; 
  /* 文本其它 */
  font-size: 16px;
  line-height: 1.6;
}
```
#### 简写形式的属性声明
+ 对于background、font的简写形式的属性声明，要么就显示声明所有的值，要么就分开写
```css
/* bad */
.element {
  background: url(image.pnd);
}

/* good */
.conetent {
   background-image: url(image.pnd);
}
```
+ 0 后面不加单位
```css
/* bad */
.element {
   width: 0px；
}

/* good */
.conetent {
   width: 0;
}
```
+ 应避免16进制表示法与rgb表示法混用，优先使用16进制表示法
```css
/* bad */
.element {
   color: #F37327；
}
.box {
   color: rgb(233, 23, 233)；
}

/* good */
.element {
   color: #f37327；
}
.box {
   color: #fcfcfc；
}
```
+ 小数省略前面的 0
```css
/* bad */
.element {
   opacity: 0.8；
}

/* good */
.conetent {
  opacity: .8；
}
```
+ 属性选择器或属性值用""，url()不使用引号
```css
/* bad */
.element {
   background-image: url("image.pnd");
}

/* good */
.conetent {
  background-image: url(image.pnd);
}
```
### 注释规约
+ 模块注释
```css
/*
 * 整个列表页样式入口文件
 */
```
+ 单行注释
```css
/*注释*/
```

### 参考资料
 + [http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh](http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh) 
 + [https://www.w3cschool.cn/wematy/p2acvozt.html](https://www.w3cschool.cn/wematy/p2acvozt.html)
 + [https://juejin.im/post/599ececb5188252423583c27](https://juejin.im/post/599ececb5188252423583c27)
 + [https://guide.aotu.io/docs/html/code.html](https://guide.aotu.io/docs/html/code.html)
