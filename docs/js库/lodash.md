## [柯里化 _.curry(func, [arity=func.length])](https://lodash.com/docs/4.17.15#curry)
示例代码
```js
 var abc = function(a, b, c) {
  return [a, b, c];
};
 
var curried = _.curry(abc);
 
curried(1)(2)(3);
// => [1, 2, 3]
 
curried(1, 2)(3);
// => [1, 2, 3]
 
curried(1, 2, 3);
// => [1, 2, 3]
 
// Curried with placeholders.
curried(1)(_, 3)(2);
// => [1, 2, 3]
```

