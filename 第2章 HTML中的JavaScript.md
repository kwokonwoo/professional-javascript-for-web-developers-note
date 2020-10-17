### \<script\>元素
- async：表示应该**立即开始下载**脚本，但不能阻止其他页面动作，比如下载资源或等待其他脚本加载。只对**外部脚本**文件有效。标记为async的脚本不保证按次序执行，保证会在页面的load事件前执行，但可能会在DOMContentLoaded之前或之后，不推荐使用async。
- defer：表示脚本可以延迟到文档完全被解析和显示之后再执行（立即下载，延迟执行）。只对**外部脚本**文件有效。标记为defer的脚本原则上按照它们出现的顺序执行，并且两者都会在DOMContentLoaded事件之前执行。

解释行内JavaScript与外部JavaScript文件页面都会阻塞（阻塞时间包含下载文件的时间）。

\<script\>元素如果使用了src属性，则会忽略行内代码（如果提供的话）。

\<script\>和\<img\>元素很像，src属性可以是一个完整的URL，而且这个URL指向的资源可以跟包含它的HTML页面不在同一个域中。
浏览器在解析这个资源时，会向src属性指定的路径发送一个GET请求，这个请求不受浏览器同源策略的限制，但返回并被执行的JavaScript则受限制（假设请求JavaScript文件）。这个请求仍然受父页面HTTP/HTTPS协议的限制。

将所有JavaScript引用放在\<body\>元素中的页面内容后面是为了让页面在处理JavaScript代码之前完全渲染页面，从而改善用户的体验，因为浏览器显示空白页面的时间变短了。

### 动态加载脚本
通过向DOM中动态的添加script元素加载指定的脚本：

```js
let script = document.createElement('script');
script.src = 'gibberish.js;
document.head.appendChild(script);
```

type属性属于废弃的语法。

推荐将JavaScript代码放在外部文件中是因为：
- 可维护性。
- 缓存。浏览器会根据特定的设置缓存所有外部链接的JavaScript文件，意味着两个页面用到同一个文件的时候，该文件只需要下载一次。

如果省略文档开头的doctype声明，则会默认开启混杂模式。

当浏览器不支持脚本或浏览器对脚本的支持被关闭时，浏览器将显示包含在<noscript>中的内容。

