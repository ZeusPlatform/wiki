## 鼠标形状
`cursor: pointer;`

## 两个css类有相同的样式写法
`.<className1>.<className2>`


## flex布局与absolute
```
<div class="xlx-signin__title">  使用flex容器水平垂直剧中
  <img class="xlx-sign__title-img" :src="titleImg" alt="" srcset="">
  <span class="xlx-signin__help">?</span> 使用absolute破坏水平文档流，但是仍然能保持垂直居中
</div>
```

## css模糊
`filter: blur(5px)`

## css动画 animation
`animation: slidein 3s ease-in 1s infinite reverse both running;`
其中 `keyframes-name`可以前置也可以后置
```
<single-animation>#
where 
<single-animation> = <time> || <timing-function> || <time> || <single-animation-iteration-count> || <single-animation-direction> || <single-animation-fill-mode> || <single-animation-play-state> || [ none | <keyframes-name> ]

where 
<timing-function> = linear | <cubic-bezier-timing-function> | <step-timing-function>
<single-animation-iteration-count> = infinite | <number>
<single-animation-direction> = normal | reverse | alternate | alternate-reverse
<single-animation-fill-mode> = none | forwards | backwards | both
<single-animation-play-state> = running | paused
<keyframes-name> = <custom-ident> | <string>

where 
<cubic-bezier-timing-function> = ease | ease-in | ease-out | ease-in-out | cubic-bezier(<number>, <number>, <number>, <number>)
<step-timing-function> = step-start | step-end | steps(<integer>[, <step-position>]?)

where 
<step-position> = jump-start | jump-end | jump-none | jump-both | start | end


```

