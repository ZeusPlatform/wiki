## start

### create-nuxt-app

`npx create-nuxt-app <name>`
`yarn create nuxt-app <project-name>`

## nuxt context

* app  NuxtAppOtions
* isClient Boolean
* isServer Boolean
* isStatic Boolean
* isDev Boolean
* isHMR Boolean
* route vue router
* from vue router
* store
* env
* params
* query
* req
* res
* redirect Function
* error
* nuxtState client
* beforeNuxtRender(fn) Function

redirect
浏览器路由会变化，类似vue的Vue.$router.push('error')

error
跳转layout/error.vue，浏览器路由不会变化

## plugins

如果在plugin进行了异步操作，并且其他组件强依赖该操作的状态，可以在返回一个Promise

## asyncDate fetch 中准确判断 href 不要使用 location.href, 建议使用 route

## 自定义 error 页面

1. Add a layouts/error.vue file
2. Customize it

## 跳转到错误页面

对于客户端渲染场景在plugin中调用context.error({message:'',statusCode: ''}), 无效，解决办法为, 插件中赋值context.errorMessage
window.onNuxtReady((nuxt) => {nuxt.error({message:'',statusCode: ''})}), 这里判断 nuxt.context.errorMessage，如果存在就展示错误页面

## nuxt vuex 单页面开发，切换页面的时候注意，数据的重置

## 配置开发的host

```json
  "config": {
    "nuxt": {
      "host": "0.0.0.0",
      "port": "8081"
    }
  },

```

## 替换自定义loading

[参考](https://nuxtjs.org/guides/features/loading#using-a-custom-loading-component)
这项配置不能修改应用首次加载loading动效

可行方案

新建component  loading.vue

```html
<div class="a">加载中</div>
<style>.a {backgroud: #FFF}</style>
```

修改nuxt.config.js

```js
export default {
  loadingIndicator: '@/components/loading.vue'
}
```

## 使用布局

```js
export default {
  layout: "common"
}
```

## [nuxt Component](https://nuxtjs.org/api/components-nuxt)

This component is used only in layouts to display the page components.

## [eslint rules](https://eslint.vuejs.org/rules/singleline-html-element-content-newline.html)

## [禁用 singleline-html-element-content-newline](https://stackoverflow.com/questions/54603407/how-do-i-turn-off-this-eslint-error-expected-new-line-break-before-and-after-ht)

'vue/singleline-html-element-content-newline': 'off',
'vue/multiline-html-element-content-newline': 'off',
