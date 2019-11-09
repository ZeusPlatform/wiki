## [Running express.js server over HTTPS](https://timonweb.com/posts/running-expressjs-server-over-https/)
HTTPS is everywhere and more often than not we need to spin an https server or two. Here's how you can do it for your local express.js dev server:
### 1. Generate a self-signed certificate
openssl req -nodes -new -x509 -keyout server.key -out server.cert

### 2. Enable HTTPS in Express
``` js
var express = require('express')
var fs = require('fs')
var https = require('https')
var app = express()

app.get('/', function (req, res) {
  res.send('hello world')
})

https.createServer({
  key: fs.readFileSync('server.key'),
  cert: fs.readFileSync('server.cert')
}, app)
.listen(3000, function () {
  console.log('Example app listening on port 3000! Go to https://localhost:3000/')
})
```

## 全站https
1. 搜索`http://`，依赖的接口改成`https://`
2. 搜索`.js'|"`,保证依赖的`js`文件支持`https`
3. 接口返回的资源链接支持`https`