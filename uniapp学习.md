# Uniapp

## 官方工具HbuilderX
>[下载地址](https://www.dcloud.io/hbuilderx.html)
## [官方组件文档](https://uniapp.dcloud.io/component/)
## 加入自定义组件
```
project
└───components
│   └───component1
│   │   └───component1.vue
│   └───component2
│   └───...
│
└───pages
└───static
└───...
```
引入
```javascript
//@的意思是项目的根目录
import component1 from '@/components/component1/component1.vue'
```

## [官方API](https://uniapp.dcloud.io/api/README)

## 条件编译
```
<!-- #ifdef H5 || APP-PLUS -->
...
<!-- #endif -->

//只有H5不编译
<!-- #ifndef H5  -->
...
<!-- #endif -->
```
## 样式
在style中
```
@import "./index.css"
```
引入外部样式
另外
```
page{
    ...
}
```
就是当前页的样式
单位 rpx 是以750px的基准的

## [生命周期](https://uniapp.dcloud.io/collocation/frame/lifecycle)
<br />

面目配置
=======
1.开起微信开发者工具的安全服务端口
1.在HbuilderX中设置好微信开发工具的路径
