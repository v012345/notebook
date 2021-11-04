# Vue 2
## 按需引入
这里的按需引入完全是手动按需引入，我想先玩明白了手动引入之后，再用babel的自动按需要引入的功能，所以下面方法的安装依赖可能用不到第二个命令
1. 安装依赖
   > `npm install element-ui`  
   > `npm install babel-plugin-component`
1. 建立 `/src/plugins/element.js` 文件件
   ```javascript
   import Vue from "vue";
   import { Button } from "element-ui";
   import 'element-ui/lib/theme-chalk/button.css';
   //这里我还不知道 Vue.use() 能不能传入多个组件
   Vue.use(Button);
   ```
1. 在 `/src/main.js` 中加入
   ```javascript
   import "./plugins/element.js";
   ```
1. 在组件中使用 `Button`
   ```html
   <el-button type="primary">Primary</el-button>
   <el-button type="success">Success</el-button>
   ```
1. [使用过渡效果时](https://element.eleme.io/#/en-US/component/transition)
   ```javascript
   import CollapseTransition from 'element-ui/lib/transitions/collapse-transition';
   Vue.component(CollapseTransition.name, CollapseTransition)
   ```
