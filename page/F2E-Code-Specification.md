# 此前端代码规范，经由本人结合各大互联网公司以及自身实践总结编制而成
+ 暂时包含html代码规范、css代码规范、js代码规范
> 欢迎各位同仁批评指正，不喜勿喷！
---
## HTML-Code-Specification

### 基本规范
1. 使用符合语义的标签写HTML文档，选择恰当的元素表达所需的含义；
2. 元素的标签和属性名称必须要小写，属性值必须加双引号，不要使用单引号；
3. 元素的嵌套遵循（X）HTML Strict嵌套规则，嵌套的节点应该缩进；
4. 正确区分闭合元素和非闭合元素，非法闭合可能会导致页面嵌套错误问题，以及IE下面样式等诡异问题；
5. 通过给元素设置自定义属性来存放与Javascript交互的数据，属性名为data-xx；
6. 缩进使用soft tab（4个空格或2个空格，团队规范要统一）；

### DOCTYPE 
+ 页面文档类型统一使用HTML5 DOCTYPE
```
<!DOCTYPE html>
<html>
    ...
</html>
```

### lang属性
+ 根据HTML5规范：
> 应在html标签上加上lang属性。这会给语音工具和翻译工具帮助，告诉它们应当怎么去发音和翻译。
+ 没有业务需求可不加
```
<!DOCTYPE html>
<html lang="zh-CN">
    ...
</html>
```

### 编码 
+ 声明方法基于HTML5规范，通过声明一个明确的字符编码，让浏览器轻松、快速的确定适合网页内容的渲染方式，通常指定为'UTF-8
```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
    </head>
    ...
</html>
```

### IE兼容模式
+ 使用兼容性<meta>标签来指定使用什么版本的IE来渲染页面
```
<!-- 优先使用 IE 最新版本和 Chrome Frame -->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
```

### 引入css、js以及内部写法规范
+ 根据HTML5规范, 通常在引入CSS和JS时不需要指明 type，因为 text/css和 text/javascript 分别是他们的默认值。
+ CSS必须在<head></head>标签里引入或者直接内部写。对于Javascript，除了基础库比较基础的脚本文件，其它都在靠近body结束前引入。
```
<!-- External CSS -->
<link rel="stylesheet" href="code_guide.css">

<!-- In-document CSS -->
<style>
    ...
</style>

<!-- External JS -->
<script src="https://7n.w3cschool.cn/attachments/image/cimg/script>

<!-- In-document JS -->
<script>
    ...
</script>
```

### 属性顺序
+ 属性应该按照特定的顺序出现以保证易读性，以及一致的属性顺序提高压缩率
+ class是为高可复用组件设计的，所以应处在第一位；
+ id更加具体且应该尽量少使用，所以将它放在第二位。
  + class
  + id
  + name
  + data-*
  + src, for, type, href, value , max-length, max, min, pattern
  + ...
```
<a class="..." id="..." data-modal="toggle" href="#">Example link</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```

### boolean属性
+ boolean属性指不需要声明取值的属性，XHTML需要每个属性声明取值，但是HTML5并不需要；
+ 总之，尽量不要为boolean属性添加取值；
> boolean属性的存在表示取值为true，不存在则表示取值为false。
```
<!-- bad -->
<input type="text" disabled="disabled">

<input type="checkbox" value="1" checked="checked">

<select>
    <option value="1" selected="selected">1</option>
</select>

<!-- good -->
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
    <option value="1" selected>1</option>
</select>
```

### 标签规约
+ 不要在自动闭合标签的结尾处使用斜线，如 br、hr、input、source
```
<!-- bad -->
<br/>

<!-- good -->
<br>
```

### 减少标签数量
+ 在编写HTML代码时，需要尽量避免多余的父节点；
```
<!-- bad -->
<span class="avatar">
    <img class="avatar" src="..." alt="...>
</span>

<!-- good -->
<img class="avatar" src="..." alt="...">
```

### 媒体退化
+ 为img标签添加alt属性以声明代替文本；
+ 在多媒体标签内部提供浏览器不支持该标签的说明，如object、audio、video；
```
<img class="avatar" src="..." alt="...">

<audio controls>
  <source src="..." type="...">
  Your brower does not support the audio tag.
```

### 资源加载
+ http或https一般不要写死，写成根据当前域名的协议去加载；
+ https的网站加载http的资源，会有问题；
```
<img src=”//static.chimeroi.com/hello-world.jpg”>
```

### 特殊符号
+ 不要直接把Unicode的特殊符号直接拷到html文档里面，要使用它对应的实体Entity；
+ 不要从UI里面直接拷一个unicode的字符过去，如果直接拷过去会比较丑，它取的是用的字体里面的符号；
```
<!-- bad -->
<span>
    &
</span>

<!-- good -->
<span>
    &amp；
</span>

```

### 注释规约
+ 对于html代码中建议超过10行的页面模块进行注释，以降低开发人员的嵌套成本与后期维护成本；
+ 由于HTML代码一般不会经过预处理，处于安全考虑，html代码中不能出现任何关于业务相关敏感信息的注释；
```
<!-- sample start -->
<div class="sample">
  <!-- sample module -->
</div>
<!-- sample end -->
```
### 初始化HTML模板
+ 标准版
```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<title>HTML5标准模版</title>
</head>
<body>
	
</body>
</html>
```
+ PC端
```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="keywords" content="your keywords">
<meta name="description" content="your description">
<meta name="author" content="author,email address">
<meta name="robots" content="index,follow">
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
<meta name="renderer" content="ie-stand">
<title>PC端HTML模版</title>
<link rel="stylesheet" href="css/index.css" >
</head>
<body>

<script src="example.js"></script>
</body>
</html>
```
+ 移动端
```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, shrink-to-fit=no" >
<meta name="format-detection" content="telephone=no" >
<title>移动端HTML模版</title>
<link rel="stylesheet" href="css/index.css" >
</head>
<body>

<script src="example.js"></script>
</body>
</html>
```
### 参考资料
 + 内部资料不便透露
 + [http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh](http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh) 
 + [https://www.w3cschool.cn/wematy/p2acvozt.html](https://www.w3cschool.cn/wematy/p2acvozt.html)
 + [https://juejin.im/post/599ececb5188252423583c27](https://juejin.im/post/599ececb5188252423583c27)
 + [https://guide.aotu.io/docs/html/code.html](https://guide.aotu.io/docs/html/code.html)
 
 
 ## CSS-Code-Specification

### 基本规约
+ 缩进, 和html缩进保持一致，2或4个空格；
+ 在每个声明块的左括号前添加一个空格
```
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
```
/* bad */
.element {
  width: 20px;}

/* good */
.element {
  width: 20px;
}
```
+ 每条声明语句的：后应有一个空格，前没有空格
```
/* bad */
.element {
  width:20px;
}

/* good */
.element {
  width: 20px;
}
```
+ 每条声明语句都应；结尾，不能省略
```
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
```
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
```
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
```
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
```
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
```
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
```
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
```
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
```
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
```
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
```
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
```
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
```
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
```
/*
 * 整个列表页样式入口文件
 */
```
+ 单行注释
```
/*注释*/
```


