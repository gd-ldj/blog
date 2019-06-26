## Sass 编码规约

### 基本规约
所有CSS规约完全适用于Sass

#### 专属规约

+ 声明的排序
  + 属性声明， 首先列出除去@include和嵌套选择器之外的所有属性声明
  + @include声明，紧随后面的是@include内容
  + 嵌套选择器放到最后，中间用空格隔开
  ```sass
  .page {
    width: 100px;
    @include transition(background 0.5s ease);
    .home {
       width: 10px;    
    }
  }
  ```
  + 变量名使用中划线`$my-width`
  
  + 不要让嵌套选择器的深度超过三层
