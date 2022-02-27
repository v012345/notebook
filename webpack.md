### webpack
大项目一般都用到的打包工具

新建一个空项目(文件夹),在项目根目录生成webpack的配置文件
`package.json`
```console
npm init -y
```
安装开发依赖`-D`现在好像可以不写了
```console
npm i -D webpack webpack-cli typescript ts-loader
```
安装完成后`/package.json`会多个下面的内容
```json
{
    ...
    "devDependences":{
        "ts-loadder":"...",
        ...
    }
    ...
}
```
生成webpack的配置文件,在项目根目录下手动生成`webpack.config.js`
```js
// node 提供路径管理模块
const path = require('path');

// webpack中的所有配置信息都应该写在这里
module.exports = {

    // 指定入口文件
    entry:"./src/index.ts",

    // 指定打包文件所在目录
    output: {
        // 指定打包文件的目录
        path: path.resolve(__dirname,"dist"), // 就是 path: "./dist" 啦

        // 打包后文件的文件名
        filename: "bundle.js",
    },

    // 指定webpack打包时要使用的模块
    module:{
        // 指定要加载的规则
        rules:[
            {
                // 用正则指定要作用的文件
                test: /\.ts$/,
                // 指定符合上面正则的文件要使用的loader
                use: "ts-loader",
                // 指定要排除的文件
                exclude: /node_modules/
            }
        ]
    }
}
```
因为这是个新项目啦,所以请手动在项目根目录生成`tsconfig.json`,简易配置
```json
{
    "compilerOptions": {
        "module": "es2015",
        "target": "es2015",
        "strict": true,
    }
}
```
同时在`/package.json`中加入
```json
{
    ...
    "scripts":{
        ...
        "build":"webpack",
        ...
    }
    ...
}
```

使用
```console
npm run build
```

没看完 [继续](https://www.youtube.com/watch?v=j-ziAwVDAIM&list=PLmOn9nNkQxJGwOhSsQ5H9JTPmiXGmy8Zw&index=10&ab_channel=%E5%B0%9A%E7%A1%85%E8%B0%B7IT%E5%9F%B9%E8%AE%AD%E5%AD%A6%E6%A0%A1)