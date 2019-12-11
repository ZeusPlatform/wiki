[DNS 原理入门](http://www.ruanyifeng.com/blog/2016/06/dns.html)
## DNS 是什么？
DNS （Domain Name System 的缩写）的作用非常简单，就是根据域名查出IP地址。你可以把它想象成一本巨大的电话本。
举例来说，如果你要访问域名math.stackexchange.com，首先要通过DNS查出它的IP地址是151.101.129.69。

## 查询过程
虽然只需要返回一个IP地址，但是DNS的查询过程非常复杂，分成多个步骤。
工具软件dig可以显示整个查询过程。
```sh
$ dig math.stackexchange.com
```
输出了四段信息 （和原文不一致）
```
# 查询参数和统计
; <<>> DiG 9.11.3-1ubuntu1.11-Ubuntu <<>> math.stackexchange.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 3742
;; flags: qr rd ad; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

# 查询内容
;; QUESTION SECTION:
;math.stackexchange.com.                IN      A

# DNS服务器的答复
;; ANSWER SECTION:
math.stackexchange.com. 0       IN      A       151.101.193.69
math.stackexchange.com. 0       IN      A       151.101.65.69
math.stackexchange.com. 0       IN      A       151.101.129.69
math.stackexchange.com. 0       IN      A       151.101.1.69

# 传输信息
;; Query time: 145 msec
;; SERVER: 172.26.16.1#53(172.26.16.1)
;; WHEN: Tue Dec 03 12:08:11 CST 2019
;; MSG SIZE  rcvd: 126

```

如果不想看到这么多内容，可以使用+short参数。
```sh
$ dig +short math.stackexchange.com
151.101.193.69
151.101.65.69
151.101.129.69
151.101.1.69
```

## DNS服务器
下面我们根据前面这个例子，一步步还原，本机到底怎么得到域名math.stackexchange.com的IP地址。

首先，本机一定要知道DNS服务器的IP地址，否则上不了网。通过DNS服务器，才能知道某个域名的IP地址到底是什么。
![20191203121936.png](https://raw.githubusercontent.com/jiangbo0216/wiki/pic-bed/20191203121936.png)
DNS服务器的IP地址，有可能是动态的，每次上网时由网关分配，这叫做DHCP机制；也有可能是事先指定的固定地址。Linux系统里面，DNS服务器的IP地址保存在/etc/resolv.conf文件。
上例的DNS服务器是192.168.1.253，这是一个内网地址。有一些公网的DNS服务器，也可以使用，其中最有名的就是Google的8.8.8.8和Level 3的4.2.2.2。

本机只向自己的DNS服务器查询，dig命令有一个@参数，显示向其他DNS服务器查询的结果。
```
$ dig @4.2.2.2 math.stackexchange.com
```
上面命令指定向DNS服务器4.2.2.2查询。

## 域名的层级
DNS服务器怎么会知道每个域名的IP地址呢？答案是分级查询。

请仔细看前面的例子，每个域名的尾部都多了一个点。

![20191203122313.png](https://raw.githubusercontent.com/jiangbo0216/wiki/pic-bed/20191203122313.png)

比如，域名math.stackexchange.com显示为math.stackexchange.com.。这不是疏忽，而是所有域名的尾部，实际上都有一个根域名。

举例来说，www.example.com真正的域名是www.example.com.root，简写为www.example.com.。因为，根域名.root对于所有域名都是一样的，所以平时是省略的。

根域名的下一级，叫做"顶级域名"（top-level domain，缩写为TLD），比如.com、.net；再下一级叫做"次级域名"（second-level domain，缩写为SLD），比如www.example.com里面的.example，这一级域名是用户可以注册的；再下一级是主机名（host），比如www.example.com里面的www，又称为"三级域名"，这是用户在自己的域里面为服务器分配的名称，是用户可以任意分配的。

总结一下，域名的层级结构如下。

```text
主机名.次级域名.顶级域名.根域名

# 即

host.sld.tld.root
```

