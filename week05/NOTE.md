# 每周总结可以写在这里

## 宏观和微观任务

一个宏观任务相当于事件循环。在宏观任务中，JavaScript 的 Promise 还会产生异步代码，JavaScript 必须保证这些异步代码在一个宏观任务中完成，因此，每个宏观任务中又包含了一个微观任务队列。
<br/>
Promise 永远在队列尾部添加微观任务。setTimeout 等宿主 API，则会添加宏观任务。

## Reamls

Realm包括一套内置对象，一个ECMAScript全局环境，所有加载到全局环境中的ECMAScript代码以及关联状态和资源。我的理解是，Realm是给代码提供一切外部资源的总集合，全局环境、全局对象等，一个Realm会提供一套完整的资源供ECMAScript代码使用。

## Execution Content

Execution Context，也就是执行上下文，实际上也叫Running Execution Context。每次函数调用，形成的Execution Context，会被推入Execution Context Stack中，也就是执行上下文栈，它的踪迹在ECMAScript标准里随处可寻。。执行栈栈顶的元素就是当前的Execution Context。

* Code evaluation state
* Function
* Script or Module
* Generator
* Lexical Environment
* Variable Environment

## Environment Record

Completion Record 表示一个语句执行完之后的结果，它有三个字段
* [[type]] 表示完成的类型，有 break continue return throw 和 normal 几种类型；
* [[value]] 表示语句的返回值，如果语句没有，则是 empty；
* [[target]] 表示语句的目标，通常是一个 JavaScript 标签（标签在后文会有介绍）。

Chrome 控制台显示的正是语句的 Completion Record 的[[value]]。

## 浏览器核心原理

把一个 URL 变成一个屏幕上显示的网页。具体做了以下几件事：
* 浏览器首先使用 HTTP 协议或者 HTTPS 协议，向服务端请求页面;
* 把请求回来的 HTML 代码经过解析，构建成 DOM 树；
* 计算 DOM 树上的 CSS 属性；
* 最后根据 CSS 属性对元素逐个进行渲染，得到内存中的位图；
* 一个可选的步骤是对位图进行合成，这会极大地增加后续绘制的速度；
* 合成之后，再绘制到界面上。

浏览器通过 HTTP 请求，获取 HTTP 响应的数据流后，会对后边的 DOM 树构建、CSS 计算、渲染、合成、绘制 尽可能地流式处理产出。即不需要等到上一步骤完全结束，就开始处理上一步的输出，这样我们在浏览网页时，才会看到逐步出现的页面。

## HTTP 协议

HTTP 协议是基于 TCP 协议出现的，对 TCP 协议来说，TCP 协议是一条双向的通讯通道，HTTP 在 TCP 的基础上，规定了 Request-Response 的模式。这个模式决定了通讯必定是由浏览器端首先发起的。

另外包括……