# android webview 初始化与前端页面加载时间的讨论
我们来讨论一下Android上的webview的初始化和前端加载时间
你将会知道：
1. 我对Android webview初始化时机的粗略讨论
2. webViewClient回调方法onPageStarted和onPageFinished在Android端的调用时机
3. 使用curl和chrome Network面板查看http请求建立TCP链接的简单分析
4. HTTP 1.1连接时间会保持多久
5. 浏览器dns缓存时间
6. html文档引用js和css资源对于加载时间的影响

这篇文章主旨在1和2两点

下面展开我们的讨论

## 实验方法
1. 为了确定webview的加载时间，我们在Android的java代码中打印日志，使用前端页面中的window.performance.timing来标记前端页面的加载时间
2. 测试的Android app 源码 https://github.com/jiangbo0216/Deva
3. 测试页面为https://juejin.im


## 几个假设
1. 假定在使用的Android debug app的日志的计时准确
2. 前端页面的window.performance.timing的计时准确
3. 假定除webview组件的其他组件加载时间为几十毫秒，一个包含webview的简单的activity，页面所有组件的初始化大部分耗时发生在webview的初始化

## 几个结论
1. 冷启动的webview耗时约为300~400ms
2. Android端触发onPageStarted的时间大致发生在前端 window.performance.timing.domLoading 的时间点，误差30ms左右
3. onPageFinished的时间大致发生在前端 window.performance.timing.domLoading 的时间点，误差30ms左右

## 实验过程
这里默认读者懂得git，会配置java的开发环境，省略android studio的安装过程，接下我们把实验代码拉下来
```sh
git clone https://github.com/jiangbo0216/Deva.git
```

我们连接上设备，点击run app在手机上安装我们的app，查看logcat。
打开chrome://inspect, 远程调试app的h5页面，在console面板中输入`window.performance.timing`
我们分别查看logcat的时间和远程调试窗口的`window.performance.timing`的值


## 从这里展开去
### 使用curl命令测量建立https连接的时间
我们使用命令
```
$ curl -w "TCP handshake: %{time_connect}, SSL handshake: %{time_appconnect}\n" -so /dev/null https://juejin.im
```
会输出TCP握手的时间和SSL握手的时间，

同时我们也可以借助chrome的来看https的连接时间，查看一次连接时间后需要关闭tab，断开tcp连接，或者等待连接断开，具体等多久请看下面的讨论
这两种方法的出来的时间并不一样，其中细节未知

## HTTP1.1 连接会保持多久




  