## vue的过滤有很多种，这里先用到一种，之后用到再往里写
```html
<div id="app">
    <button @click="show = !show">
        Toggle
    </button>
    <transition name="fade">
        <p v-if="show">hello</p>
    </transition>
</div>
```

> `transition` 的 name的 fade 对应着 style 中的 fade

```css
<style>
    .fade-enter-active, .fade-leave-active {
        transition: opacity .5s;
    }
    .fade-enter, .fade-leave-to {
        opacity: 0;
    }
</ style>
```