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
```HTML
<!DOCTYPE html>
<html>
    ...
</html>
```

### lang属性
+ 根据HTML5规范：
> 应在html标签上加上lang属性。这会给语音工具和翻译工具帮助，告诉它们应当怎么去发音和翻译。
+ 没有业务需求可不加
```HTML
<!DOCTYPE html>
<html lang="zh-CN">
    ...
</html>
```

### 编码 
+ 声明方法基于HTML5规范，通过声明一个明确的字符编码，让浏览器轻松、快速的确定适合网页内容的渲染方式，通常指定为'UTF-8
```HTML
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
```HTML
<!-- 优先使用 IE 最新版本和 Chrome Frame -->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
```

### 引入css、js以及内部写法规范
+ 根据HTML5规范, 通常在引入CSS和JS时不需要指明 type，因为 text/css和 text/javascript 分别是他们的默认值。
+ CSS必须在<head></head>标签里引入或者直接内部写。对于Javascript，除了基础库比较基础的脚本文件，其它都在靠近body结束前引入。
```HTML
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
```HTML
<a class="..." id="..." data-modal="toggle" href="#">Example link</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```

### boolean属性
+ boolean属性指不需要声明取值的属性，XHTML需要每个属性声明取值，但是HTML5并不需要；
+ 总之，尽量不要为boolean属性添加取值；
> boolean属性的存在表示取值为true，不存在则表示取值为false。
```HTML
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
```HTML
<!-- bad -->
<br/>

<!-- good -->
<br>
```

### 减少标签数量
+ 在编写HTML代码时，需要尽量避免多余的父节点；
```HTML
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
```HTML
<img class="avatar" src="..." alt="...">

<audio controls>
  <source src="..." type="...">
  Your brower does not support the audio tag.
 </audio>
```

### 资源加载
+ http或https一般不要写死，写成根据当前域名的协议去加载（确保两者下的资源都存在）；
+ https的网站加载http的资源，会有问题；
```HTML
<img src="//static.chimeroi.com/hello-world.jpg">
```

### 特殊符号
+ 不要直接把Unicode的特殊符号直接拷到html文档里面，要使用它对应的实体Entity；
+ 不要从UI里面直接拷一个unicode的字符过去，如果直接拷过去会比较丑，它取的是用的字体里面的符号；
```HTML
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
```HTML
<!-- sample start -->
<div class="sample">
  <!-- sample module -->
</div>
<!-- sample end -->
```
### 初始化HTML模板
+ 标准版

```HTML
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
```HTML
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
```HTML
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
 + [http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh](http://codeguide.co/?spm=a2o8t.11089562.0.0.7a0b6654shFwrh) 
 + [https://www.w3cschool.cn/wematy/p2acvozt.html](https://www.w3cschool.cn/wematy/p2acvozt.html)
 + [https://juejin.im/post/599ececb5188252423583c27](https://juejin.im/post/599ececb5188252423583c27)
 + [https://guide.aotu.io/docs/html/code.html](https://guide.aotu.io/docs/html/code.html)
 
