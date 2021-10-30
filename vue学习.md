安装cli
npm install -g @vue/cli
创建项目
vue create vc.nightowl.name
(vue2就行)


===
引入elementUI
npm i element-ui
修改 babel.config.js
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

如果出现这个问题
Error: Cannot find module 'babel-plugin-component'
npm view babel version

npm i babel-plugin-component -D
# For babel6 
npm i babel-plugin-component@0 -D
===


引入less
npm i less
引入less-loader 锁在7就行
npm i less-loader@7

引入vueX
npm i vuex

引入vue-router
npm i vue-router


生成 vue.config.js
module.exports = {
    //关闭语法检查
    lintOnSave: false,
}
