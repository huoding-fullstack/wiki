# 前端框架-饿了么搭建

关于前端框架，在我们没有设计人员的情况之下，我们选择使用饿了么开发的前端框架，element-ui (https://element.eleme.io/#/zh-CN)。

# 搭建vue

首先第一步是需要搭建vue，我们使用vue的脚手架直接进行搭建

首先安装vue-cli:
```
npm install -g vue-cli
```
然后查看vue list，看到有六种vue的脚手架框架，我们选择使用了webpack-simple这种方案

```
vue init webpack-simple frontend
```

在安装的过程中有很多选项，项目名称我就命名为frontend, 咨询我是否打开sass支持的时候，我就选择了支持。

于是我们在frontend这个目录下就看到了package.json, webpack.config.js

我们先把依赖包下载下来

```
npm install
```

然后运行 `npm run dev`

就打开了一个页面，显示vue安装成功

# 安装elememt-ui

按照官网推荐的，使用命令`npm i element-ui -S` 安装

修改main.js

```
import Vue from 'vue'
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
import App from './App.vue'
import MyHeader from './components/header'

Vue.use(ElementUI)
Vue.component('my-header', MyHeader)

new Vue({
  el: '#app',
  render: h => h(App)
})

```

src下创建components/header.vue
```
<template>
    <div class="headerWrapper">
        <header class="header" ref="header">
            <div class="container">
                <h1>
                    logo
                </h1>
                <ul class="nav">
                    <li class="nav-item nav-algolia-search">
                        搜索
                    </li>
                    <li class="nav-item">
                        链接1
                    </li>
                    <li class="nav-item">
                        链接2
                    </li>
                    
                </ul>
            </div>
        </header>
    </div>

</template>
<script>
export default {
    
}
</script>

```
运行，发现问题

```
ERROR in ./node_modules/element-ui/lib/theme-chalk/fonts/element-icons.ttf
```

查看了一下google，是ttf的解析没有解析对，修改webpackage.conf.js, 增加对ttf文件的解析：
```
      {
        test: /\.(eot|woff|ttf)$/,
        loader: 'file-loader'
      },
```

# 结束

至此，vue和element-ui的框架就搭建完成了