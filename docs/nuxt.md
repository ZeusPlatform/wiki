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