### 原理图
![](../assets/Screenshot%202022-02-12%20150837.png)

### 安装
> vue2 使用 vuex3, 不然不太兼容
```console
npm i vuex@3 
```
### 配置
`/src/store/index.js`
```javascript
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)

const actions={
  add(context,value){
    context.commit("ADD",value)
  }
}
const mutations={
  ADD(state,value){
    state.sum += value
  }
}
const state={
  sum:1,
  user:10086,
}
// 类似与计算属性
const getters={
  multiple(state){
    return state.sum * 10
  }
}

export default new Vuex.Store({
    actions,
    mutations,
    state,
    getters
})
```

`/src/main.js`
```javascript
import Vue from 'vue'
import App from './App.vue'
import store from './store'

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
  store,
}).$mount('#app')
```

## 基本使用
```html
<template>
  <div id="app">
    {{ $store.state.sum }}
    {{ $store.state.getters.multiple }}
  </div>
</template>

<script>
export default {
  name: "App",
  methods: {
    add(){
      this.$store.dispatch("add",1)
    },
    ADD(){
      this.$store.commit("ADD",1)
    }
  },
};
</script>
```

## 高级使用
```html
<template>
  <div id="app">
    {{ sum }}
    {{ multiple }}
  </div>
</template>

<script>
import {mapState,mapGetters,mapMutations,mapActions} from 'vuex'

export default {
  name: "App",
  computed:{
    ...mapState(["sum"]), // 也可以用对象,指调用名称,具体看官网
    ...mapGetters(["multiple"])
  }
  methods: {
    // 生成
    // ADD(value){
    //   this.$store.commit("ADD",value)
    // }
    ...mapMutations(["ADD"]),

    // 生成
    // increment(value){
    //   this.$store.commit("ADD",value)
    // }
    // ...mapMutations({increment:"ADD"}),

    ...mapActions(["add"]),
  },
};
</script>
```

## 模块化,namespace
`/src/store/orders.js`
```javascript
export default {
  namespace:true,
  actions:{
     add(context,value){
      context.commit("ADD",value)
    }
  },
  mutations:{
    ADD(state,value){
      state.sum += value
    }
  },
  state:{
    sum:1,
  },
  getters:{
    multiple(state){
      return state.sum * 10
    }
  }
}
```

`/src/store/users.js`
```javascript
export default {
  namespace:true,
  actions:{
    update(context,value){
      context.commit("UPDATE",value)
    }
  },
  mutations:{
    UPDATE(state,value){
      state.user = value
    }
  },
  state:{
    user:10086,
  }
}
```

`/src/store/index.js`
```javascript
import Vue from 'vue'
import Vuex from 'vuex'
import orders from './orders'
import users from './users'
Vue.use(Vuex)

export default new Vuex.Store({
  modules:{
    orders,
    users
  }
})
```

`/src/main.js`
```html
<template>
  <div id="app">
    {{ sum }}
    {{ user }}
  </div>
</template>

<script>
import {mapState,mapGetters,mapMutations,mapActions} from 'vuex'

export default {
  name: "App",
  computed:{
    // 生成
    // sum(){
    //   return this.$store.orders.sum;
    // }
    ...mapState("orders",["sum"]),
    // 生成
    // multiple(){
    //   return this.$store.getters["orders/multiple"];
    // }
    ...mapGetters("orders",["multiple"]),
    ...mapState("users",["user"]),
  }
  methods: {
    // 生成
    // ADD(value){
    //   this.$store.commit("orders/ADD",value)
    // }
    ...mapMutations("orders",["ADD"]),
    ...mapActions("orders",["add"]),
  },
};
</script>
```