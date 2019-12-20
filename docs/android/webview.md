# android webview 初始化与前端页面加载时间的讨论
之前看美团2017年的技术文章，有疑问 https://tech.meituan.com/2017/06/09/webviewperf.html


首次初始化时间	二次初始化时间
iOS（UIWebView）	306.56	76.43
iOS（WKWebView）	763.26	457.25
Android	192.79 *	142.53

> *Android外卖客户端启动后会在后台开启WebView进程，故并不是完全新建WebView时间。
我们来讨论一下Android上的webview的初始化和前端加载时间
你将会知道：
1. 我对Android webview初始化时机的粗略讨论
2. webViewClient回调方法onPageStarted和onPageFinished在Android端的调用时机
3. 使用curl和chrome Network面板查看http请求建立TCP链接的简单分析
4. HTTP 1.1连接时间会保持多久
5. 浏览器dns缓存时间
6. html文档引用js和css资源对于加载时间的影响
7. RTT (Round Trip Time往返时间)

这篇文章主旨在1和2两点

下面展开我们的讨论

## 实验方法
1. 为了确定webview的加载时间，我们在Android的java代码中打印日志，使用前端页面中的`window.performance.timing`来标记前端页面的加载时间
2. 测试的Android app 源码 https://github.com/jiangbo0216/Deva
3. 测试页面为https://juejin.im


## 几个假设
1. 假定在使用的Android debug app的日志的计时准确
2. 前端页面的window.performance.timing的计时准确
3. 假定除webview组件的其他组件加载时间为几十毫秒，一个包含webview的简单的activity，页面所有组件的初始化大部分耗时发生在webview的初始化
4. 假定android客户端webview初始化之后，立即加载网页，可以使用`window.performance.timing`来捕捉时间

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

### 几组数据值
预定义  `window.performance.timing` 为客户端时间
客户端的log为客户端时间
对应表示时间相近，相差小于50ms

我们先把图抬上来
![20191220114116.png](https://raw.githubusercontent.com/jiangbo0216/wiki/pic-bed/20191220114116.png)
connectEnd: 1576812247887  
connectStart: 1576812247593  
domComplete: 1576812252008  
domContentLoadedEventEnd: 1576812249922  
domContentLoadedEventStart: 1576812249922  
domInteractive: 1576812249922  
domLoading: 1576812247994  
domainLookupEnd: 1576812247593  
domainLookupStart: 1576812247561  
fetchStart: 1576812247446  
loadEventEnd: 1576812252009  
loadEventStart: 1576812252008  
navigationStart: 1576812247442  
redirectEnd: 0  
redirectStart: 0  
requestStart: 1576812247887  
responseEnd: 1576812248037  
responseStart: 1576812247975  
secureConnectionStart: 1576812247666  
unloadEventEnd: 0  
unloadEventStart: 0  
![20191220114215.png](https://raw.githubusercontent.com/jiangbo0216/wiki/pic-bed/20191220114215.png)
2019-12-20 11:24:06.865 13400-13400/com.india.deva D/Test: 1576812246865  
2019-12-20 11:24:07.439 13400-13400/com.india.deva D/Test onCreate: 1576812247439  
2019-12-20 11:24:08.027 13400-13400/com.india.deva D/Test onPageStarted: 1576812248027  
2019-12-20 11:24:09.844 13400-13400/com.india.deva D/Test onPageFinished: 1576812249844  
2019-12-20 11:24:12.024 13400-13400/com.india.deva D/Test onPageFinished: 1576812252024  

通过数据对比我们可以得出结论
客户端初始化webview完成的时间 对应于 navigationStart fetchStart 这两个前端时间
客户端时间 onPageStarted 对应于 responseStart responseEnd domLoading 这三个前端时间
客户端第一个onPageFinished 对应于 domInteractive domContentLoadedEventStart domContentLoadedEventEnd 这三个前端时间
客户端第二个onPageFinished 对应于 domComplete loadEventEnd loadEventStart 这三个前端时间

数据仅供参考



## 从这里展开去
### 使用curl命令测量建立https连接的时间
我们使用命令
```
$ curl -w "TCP handshake: %{time_connect}, SSL handshake: %{time_appconnect}\n" -so /dev/null https://juejin.im
```
会输出TCP握手的时间和SSL握手的时间，

同时我们也可以借助chrome的来看https的连接时间，查看一次连接时间后需要关闭tab，断开tcp连接，或者等待连接断开，具体等多久请看下面的讨论
这两种方法的出来的时间并不一样，其中细节未知
![Previewing the timing breakdown of a request.PNG](https://raw.githubusercontent.com/jiangbo0216/wiki/pic-bed/Previewing%20the%20timing%20breakdown%20of%20a%20request.PNG)

结果来说就是从chrome的角度来看，建立连接的速度较 curl 命令快

## HTTP1.1 连接会保持多久

以下文章来源于 https://fastmail.blog/2011/06/28/http-keep-alive-connection-timeouts/ 时间2011年，注意时效性
这个连接时间有客户端（比如chrome）和服务端共同决定，一般来说服务端会设置300秒超时断开，但是这个时间是可以修改的的
总的来说 Chrome在45秒后将发送一个TCP保持活动数据包，并将每45秒执行一次，直到5分钟超时为止。没有其他浏览器会这样做。


The average user of the FastMail website is probably a bit different to most websites. Webmail tends to be a "productivity application" that people use for an extended period of time. So for the number of web requests we get, we probably have less individual users than other similar sized sites, but the users we do have tend to stay for a while and do lots of actions/page views.

Because of that we like to have a long HTTP keep-alive timeout on our connections. This makes interactive response nicer for users as moving to the next message after spending 30 seconds reading a message is quick because we don't have to setup a new TCP connection or SSL session, we just send the request and get the response over the existing keep-alive one. Currently we set the keepalive timeout on our frontend nginx servers to 5 minutes.

I did some testing recently, and found that most clients didn't actually keep the connection open for 5 minutes. Here's the figures I measured based on Wireshark dumps.

* Opera 11.11 – 120 seconds
* Chrome 13 – at least 300 seconds (server closed after 300 second timeout)
* IE 9 – 60 seconds (changeable in the [registry](https://support.microsoft.com/zh-cn/help/813827/how-to-change-the-default-keep-alive-time-out-value-in-internet-explor), appears to apply to IE 8/9 as well though the page only mentions IE 5/6/7)
* Firefox 4 – 115 seconds (changeable in about:config with [network.http.keep-alive.timeout](http://kb.mozillazine.org/Network.http.keep-alive.timeout) preference)

I wondered why most clients used <= 2 minutes, but Chrome was happy with much higher.

Interestingly one of the other things I noticed while doing this test with Wireshark is that after 45 seconds, Chrome would send a TCP keep-alive packet, and would keep doing that every 45 seconds until the 5 minute timeout. No other browser would do this.

After a bunch of searching, I think I found out what's going on.

It seems there's some users behind NAT gateways/stateful firewalls that have a 2 minute state timeout. So if you leave an HTTP connection idle for > 2 minutes, the NAT/firewall starts dropping any new packets on the connection and doesn't even RST the connection, so TCP goes into a long retry mode before finally returning that the connection timed out to the application.

To the user, the visible result is that after doing something with a site, if they wait > 2 minutes, and then click on another link/button, the action will just take ages to eventually timeout. There's a Chrome bug about this here:

http://code.google.com/p/chromium/issues/detail?id=27400

So the Chrome solution was to enable SO_KEEPALIVE on sockets. On Windows 7 at least, this seems to cause TCP keep-alive pings to be sent after 45 seconds and every subsequent 45 seconds, which avoids the NAT/firewall timeout. On Linux/Mac I presume this is different because they're kernel tuneables that default to much higher. (Update: I didn’t realise you can set the idle and interval for keep-alive pings at the application level in Linux and Windows)

This allows Chrome to keep truly long lived HTTP keep-alive connections. Other browsers seem to have worked around this problem by just closing connections after <= 2 minutes instead.

I've mentioned this to the Opera browser network team, so they can look at doing this in the future as well, to allow longer lived keep-alive connection.

I think it's going to be a particularly real problem with Server-Sent Event type connections that can be extremely long lived. We're either going to have to send application level server -> client pings over the channel every 45 seconds to make sure the connection is kept alive, or enable a very low keep-alive time on the server and enable SO_KEEPALIVE on each event source connected socket.

HTTP是一个构建在传输层的TCP协议之上的应用层的协议，在这个层的协议，是一种网络交互需要遵守的一种协议规范。

 

### [HTTP1.0的短连接](https://blog.csdn.net/jiyiqinlovexx/article/details/50500246)
HTTP 1.0规定浏览器与服务器只保持短暂的连接，浏览器的每次请求都需要与服务器建立一个TCP连接，服务器完成请求处理后立即断开TCP连接，服务器不跟踪每个客户也不记录过去的请求。这个过程大概可以描述为：

1. 建立连接：首先DNS解析过程。如把域名变成一个ip，如果url不包含端口号，则会使用该协议的默认端口号，HTTP协议的默认端口号为80。然后三次握手建立一个TCP连接；

2. 请求：连接成功后，开始向web服务器发送请求，这个请求一般是GET或POST请求。

3. 应答：web服务器收到这个请求，进行处理。web服务器会把文件内容传送给响应的web浏览器。包括：HTTP头信息，体信息。

4. 关闭连接：当应答结束后，web浏览器与web服务器必须四次握手断开连接，以保证其它web浏览器能够与web服务器建立连接。

 

### HTTP1.1的长连接
但是HTTP1.1开始默认建立的是长连接，即一旦浏览器发起HTTP请求，建立的连接不会请求应答之后立刻断掉。


1.  一个复杂的具备很多HTTP资源的网页会建立多少TCP连接，如何使用这些连接？

2.  已经建立的TCP连接是否会自动断开，时间是多久？

 

对于第一个问题。现在浏览器都有最大并发连接数限制，应该说如果需要，就会尽量在允许范围内建立更多的TCP持久连接来处理HTTP请求，同样滴，一个TCP持久连接可以不断传输多个HTTP请求，但是如果上一个请求的响应还未收到，则不能处理下一个请求(Pipeling管道技术可以解决这个问题从而进一步提升性能)，所以说很多浏览器其实都可以修改允许最大并发连接数以提升浏览网页的速度。

 

对于第二个问题。问题在于服务器端对于长连接的实现，特别是在对长连接的维护上。FTP协议及SMTP协议中有NOOP消息，这个就可以认为是心跳报文，但HTTP协议没有类似的消息，这样服务器端只能使用超时断开的策略来维护连接。设想超时时间非常短，那么有效空闲时间就非常短，换句话讲：一旦链路上没有数据发送，服务器端很快就关闭连接。

也就是说其实HTTP的长连接很容易在空闲后自动断开，一般来说这个时间是300s左右。

> 虽然http协议没有心跳报文的机制，但是不妨碍chrome会自动维护这个连接，所以和上面的说法不冲突

### [HTTP1.1提升性能的手段](http://www.zhihu.com/question/36469741/answer/67608570)


HTTP1.1里大概规范了几项提高性能的手段：

持久连接 （keep-alive/persistent connection）
并行连接
Pipelining
第一点之前已经说过了，所以不表。

第二点，由于现代网页通常包含了复数个（>=10）资源，而按照默认设定，一个连接中的每一个请求必须等待收到响应后才能发送下一个请求，所以如果复数的资源请求全部在一个连接one by one发送给服务器显然会很慢，而为了弥补这一缺陷，浏览器通常会默认开启多个TCP连接，然后再根据每个连接的状态在其中依次发送数据请求，而且客户端有权任意关闭超发的连接。各个浏览器允许的并行连接数大致是这样的（From SO）：

Firefox 2:  2

Firefox 3+: 6

Opera 9.26: 4

Opera 12:   6

Safari 3:   4

Safari 5:   6

IE 7:       2

IE 8:       6

IE 10:      8

Chrome:     6

由于TCP协议本身有慢启动的特征，会随着时间调谐连接的最大速度，因此在现代浏览器中持久连接和并行连接通常是搭配在一起使用的—— 一方面由于持久连接的存在，每个TCP连接已经处于调谐后的状态，另一方面持久连接可以避免重新三次握手的开销。

关于第三点，
按照HTTP1.1的描述，还有种可以提升性能的方案是管道化，可以在一个连接中发送多个请求不必等待前一个请求返回。但这项技术比较容易踩坑，所以主流面向用户的浏览器，这项技术是被默认关闭。 

关于HTTP2：
HTTP2为了性能做了不少努力，比如提供了规范以支持连接的多路复用。


HTTP1.0需要加上keep-alive的请求首部，否则默认一个请求一个连接。
HTTP1.1之后keep-alive（持久连接）被默认启用，除非在响应中指定connection：close，否则webserver会假定所有连接都是持久的。



### [计量连接耗时（开启keep-alive的必要性）](https://www.jianshu.com/p/7c23f48ab03f)
如果你用 Chrome 的来分析 network 的话，你就会发现小文件如 JS/CSS 瓶颈其实在延时。举个例子假设你有个 JS 大小是 100KB，然后你在用 2Mbps 的 ADSL(下载速度： 2000 / 8 = 250KB/s)，带宽耗时是 400ms。

在开始传输这 100KB 前,还需要在以下三个地方耗费一定时间：
1. DNS 查询要 1 个 RTT（Round Trip Time往返时间，即 ping 时间）
2. 建立 TCP 连接要 1 个 RTT
3. 再建立 SSL 要 3 个 RTT
4. 之后 HTTP 发请求又 1 个 RTT
假设你的 ping 是 25ms，6 个 RTT 就是 150ms。总和 550ms，延时占总和的 27.27%(150 / 550)。这绝对不是个小数字，可以有很大的优化空间。

### 常用设置
1. 开启：http 1.1中默认启用Keep-Alive，目前大部分浏览器都是用http1.1协议，也就是说默认都会发起Keep-Alive的连接请求。

2. 关闭：在http头中设置Connection: close，即可关闭。

3. 设置连接时间： 在http header中设置Keep-Alive: timeout=5, max=1000
timeout是超时时间，单位秒，超过这个时间后就断开连接
max是最多的连接次数，若超过这个次数就强制断开连接

### 延伸：TCP Keep-Alive（三个参数：超时：tcp_keepalive_time，再次发送侦测包时间间隔：tcp_keepalive_intvl，探测次数：tcp_keepalive_probes）
      TCP Keep-Alive是tcp的一种检测tcp连接状况的保鲜机制。其原理大概如下：
      当网络两端建立了TCP连接之后，双方没有任何数据流发送往来tcp_keepalive_time时间后，服务器内核就会尝试向客户端发送侦测包，来判断TCP连接状况(客户端崩溃、强制关闭应用等等情况)。如果没有收到对方的回答，会在tcp_keepalive_intvl时间后再次发送侦测包，直到收到对方的回复，若一直没收到回复，则在尝试tcp_keepalive_probes次后丢弃该tcp连接。

> 这里我的理解和chrome的机制一样

## 浏览器dns缓存时间
