## Video.js 的踩坑记
最近项目中需求要 web 浏览器直接播放 rtmp 的视频源，强需求，而且资源有限，没办法服务端转其它格式的视频源  

这种情况下，就只有重拾即将淘汰的 flash 方案，作为过渡期 

Video.js 的低于6版本的是有封装 flash 的方案的，确定使用 Video.js 的 flash 方案播放 rtmp 的视频

> 开发一切正常，提交测试  

测试提 bug 过来，不能播放  

> 瓦特？ 我这正常播放啊，是不是你的电脑坏了 ！！  

看过，对比过，确认允许运行 flash，的确是测试的电脑不能播放，难道真的是测试的电脑的问题 ？  

> 开始排查...  

测试的电脑 swf资源 没有下载  

> 再排查...  

MacOS 系统能正常下载 swf资源，windows 系统不能稳定下载 swf资源，强刷之后偶尔下载，普刷不会下载  

> 继续排查... 

直接写在HTML里面，能够正常下载并播放，使用react组件开发，windows 上不能正常下载 swf资源

灵异事件... MacOS + react + Video.js 与 windows + react + Video.js 有什么不同 ？  
 
 macOS 的 chrome 和 windows 的 chrome 的 swf资源下载机制不同 ？
 
问题的来源还没搞明白  

#### 解决问题的办法试了出来   

componentDidMount 的时候手动调用了一下 VideoJs 对象就可以了
```js
import VideoJs from 'video.js'

componentDidMount () {
  VideoJs("my-player");
}
```
#### 具体是什么导致的，还望大神指点一二
