面向对象的javascript
```js
var a = {
  b:1,
  log: function () {
    console.log(this.b)
  }
}

a.log() //输出1
```