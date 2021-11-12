## 引入依赖
`npm install vue-router`

## 安装
1. 按大众的习惯,在 `/src` 下生成 `router/index.js` 文件;
1. `/src/router/index.js`
   ```javascript
   import Vue from 'vue';
   import Router from "vue-router";
   Vue.use(Router) //给Vue安装vue-router插件
   import HelloWorld from "../components/HelloWorld" //引入要用的组件
   export default new Router({
      routes: [
         {
               path: "/home",//路径
               component: HelloWorld//组件
         }
      ]
   })
   ```
1. `/src/main.js`
   ```javascript
   import Vue from 'vue'
   import App from './App.vue'
   import router from './router'

   Vue.config.productionTip = false

   new Vue({
   render: h => h(App),
   router
   }).$mount('#app')
   ```
1. 使用
   `/src/App.vue`
   ```html
   <template>
   <div id="app">
      <router-link to="/home">home</router-link>
      <router-view></router-view>
   </div>
   </template>
   ```
