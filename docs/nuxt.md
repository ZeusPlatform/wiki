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


## plugins
如果在plugin进行了异步操作，并且其他组件强依赖该操作的状态，可以在返回一个Promise

## asyncDate fetch 中准确判断 href 不要使用 location.href, 建议使用 route


## 自定义 error 页面
1. Add a layouts/error.vue file
2. Customize it