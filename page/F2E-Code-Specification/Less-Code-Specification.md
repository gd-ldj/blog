## Less 编码规约

### 基本规约

所有适用于CSS的规约均适用于Less

### 专属规约

- @import 必须声明于文件的头部位置
  ```less
  // bad
  .page {
    width: 100px;
  }
  
  @import "global.less"
  
  // good
  @import "global.less"
  
  .page {
    width: 100px;
  }
  ```
 - 文件全局的变量仅次于@import声明， 局部变量在块的头部声明
   ```les
  // bad
   ```less
   // bad
  .page {
    width: @width;
    @width： 100px；
  }
  
  // good
  .page {
    @width： 100px；
    width: @width;
  }
  ```
  
 - 变量命名必须用中划线 - 号连接`@big-width`
    ```css
  // bad
  .page {
    @bigWidth： 100px；
  
    width: @bigWidth;
  }
  
  // good
  
  .page {
    @big-width： 100px；
  
    width: big-width;
  }
  ```
