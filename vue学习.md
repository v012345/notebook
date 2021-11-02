## 安装
```shell
//全局安装cli
$ npm install -g @vue/cli
//创建项目
$ vue create vc.nightowl.name
//(vue2就行)
```
---

## 引入elementUI

```shell
$ npm i element-ui
```
修改 babel.config.js
```javascript
module.exports = {
  presets: [
    '@vue/cli-plugin-babel/preset',
    /**之前是es2015 */
    ["@babel/preset-env", { "modules": false }]
  ],
  plugins: [
    [
      "component",
      {
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```

如果出现这个问题  
`Error: Cannot find module 'babel-plugin-component'`
```shell
$ npm view babel version
$ npm i babel-plugin-component -D
# For babel6 
$ npm i babel-plugin-component@0 -D
```

## 引入less
```shell
$ npm i less
//引入less-loader 锁在7就行
$ npm i less-loader@7
```

## 引入vueX
```shell
$ npm i vuex
```
## 引入vue-router
```shell
$ npm i vue-router
```

## 生成 vue.config.js
```javascript
module.exports = {
    //关闭语法检查
    lintOnSave: false,
}
```

# 使用
## 父组件捕获子组件发出的事件

```html
<child @childEmitEventName="parentMethod"></child>
```

## $nextTick
> 写法可以去看[官网](https://vuejs.org/v2/api/#vm-nextTick)
> 作用大概就是，在一个方法中，改变某个值时，真实dom还没变，这个时候去拿真实dom中的值明显不对，`this.$nextTick(function(){})`可以保证真实dom刷新后再去执行里面的回调