# Vue static template

这个项目是为了对标 ejs 这样的模板引擎出现的，它的作用就是让你可以使用熟悉的语法来编写模板，而不至于出现下面这样一坨东西

```html
<% if (user) { %>
<h2><%= user.name %></h2>
<% } %>
```

对比一下 Vue 的语法

```html
<h2 v-if="user">{{ user.name }}</h2>
```

是不是觉得简洁多了。

设计初衷：为了使用 Vue 简洁的语法来描述模板，同时在有限的条件下使用 Vue 的组件来达到其他模板引擎继承作用。

## 支持功能

### 指令

- v-if
- v-else
- v-else-if
- v-for
- v-show
- v-text
- v-html
- v-bind 有限支持，只支持:style 和:class

### 特殊元素

- `<slot>`
- `<template>`

### 状态选项

- data
- props
- name
- inheritAttrs
- components

### css 功能

只支持以下列举功能

- `<style>`
- 预处理器
- scoped

以上内容如果有疏漏之处请翻阅官方文档进行查看 [Vuejs](https://cn.vuejs.org/api/)

## 快速入手

从一个展示 hello world 的界面开始

```vue
<template>
  <p>{{ str }}</p>
</template>
<script>
export default {
  data() {
    return {
      str: 'hello wrold',
    };
  },
};
</script>
<style>
p {
  color: red;
}
</style>
```

这里不会具体介绍怎么来完成解析工作，但是最终会生成两段代码，分别为 html 以及 css

```html
<p>hello wrold</p>
<style>
  p {
    color: red;
  }
</style>
```

> 默认 `<style>` 会在每个组件下方展示，后续会暴露出 api 支持输出到指定位置

当然这个例子可能太简单了一些，下面就演示一个 vue 官方自带的例子

结构如下

```sh
- src
  - App.vue
  - components
		- HelloWorld.vue
```

### App.vue

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" width="25%" />
    <HelloWorld msg="Hello Vue in CodeSandbox!" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

### HelloWorld.vue

```vue
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li>
        <a
          href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel"
          target="_blank"
          rel="noopener"
          >babel</a
        >
      </li>
      <li>
        <a
          href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint"
          target="_blank"
          rel="noopener"
          >eslint</a
        >
      </li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li>
        <a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a>
      </li>
      <li>
        <a href="https://forum.vuejs.org" target="_blank" rel="noopener"
          >Forum</a
        >
      </li>
      <li>
        <a href="https://chat.vuejs.org" target="_blank" rel="noopener"
          >Community Chat</a
        >
      </li>
      <li>
        <a href="https://twitter.com/vuejs" target="_blank" rel="noopener"
          >Twitter</a
        >
      </li>
      <li>
        <a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a>
      </li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li>
        <a href="https://router.vuejs.org" target="_blank" rel="noopener"
          >vue-router</a
        >
      </li>
      <li>
        <a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a>
      </li>
      <li>
        <a
          href="https://github.com/vuejs/vue-devtools#vue-devtools"
          target="_blank"
          rel="noopener"
          >vue-devtools</a
        >
      </li>
      <li>
        <a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener"
          >vue-loader</a
        >
      </li>
      <li>
        <a
          href="https://github.com/vuejs/awesome-vue"
          target="_blank"
          rel="noopener"
          >awesome-vue</a
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
```

最终大概会生成这样的一个结构

```html
<div id="app">
  <img alt="Vue logo" src="./assets/logo.png" width="25%" />
  <div data-v-763db97b="" class="hello">
    <h1 data-v-763db97b="">Hello Vue in CodeSandbox!</h1>
    <h3 data-v-763db97b="">Installed CLI Plugins</h3>
    <ul data-v-763db97b="">
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel"
          target="_blank"
          rel="noopener"
          >babel</a
        >
      </li>
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint"
          target="_blank"
          rel="noopener"
          >eslint</a
        >
      </li>
    </ul>
    <h3 data-v-763db97b="">Essential Links</h3>
    <ul data-v-763db97b="">
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://vuejs.org"
          target="_blank"
          rel="noopener"
          >Core Docs</a
        >
      </li>
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://forum.vuejs.org"
          target="_blank"
          rel="noopener"
          >Forum</a
        >
      </li>
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://chat.vuejs.org"
          target="_blank"
          rel="noopener"
          >Community Chat</a
        >
      </li>
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://twitter.com/vuejs"
          target="_blank"
          rel="noopener"
          >Twitter</a
        >
      </li>
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://news.vuejs.org"
          target="_blank"
          rel="noopener"
          >News</a
        >
      </li>
    </ul>
    <h3 data-v-763db97b="">Ecosystem</h3>
    <ul data-v-763db97b="">
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://router.vuejs.org"
          target="_blank"
          rel="noopener"
          >vue-router</a
        >
      </li>
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://vuex.vuejs.org"
          target="_blank"
          rel="noopener"
          >vuex</a
        >
      </li>
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://github.com/vuejs/vue-devtools#vue-devtools"
          target="_blank"
          rel="noopener"
          >vue-devtools</a
        >
      </li>
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://vue-loader.vuejs.org"
          target="_blank"
          rel="noopener"
          >vue-loader</a
        >
      </li>
      <li data-v-763db97b="">
        <a
          data-v-763db97b=""
          href="https://github.com/vuejs/awesome-vue"
          target="_blank"
          rel="noopener"
          >awesome-vue</a
        >
      </li>
    </ul>
  </div>
</div>
<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
<style type="text/css">
  h3[data-v-763db97b] {
    margin: 40px 0 0;
  }
  ul[data-v-763db97b] {
    list-style-type: none;
    padding: 0;
  }
  li[data-v-763db97b] {
    display: inline-block;
    margin: 0 10px;
  }
  a[data-v-763db97b] {
    color: #42b983;
  }
</style>
```

## 其他

### 框架定义

支持运行时使用和编译时使用两种方法，对于运行时使用会有一些额外的限制

- 不能使用 scoped 标签
- 不能在 style 下使用 lang 属性
- 在使用 components 注册组件时，必须传递字符串组件

这些限制是因为没有编译这一步的帮助，上述都无法做到

### 其他

因为这个库的作用就是生成静态模板，所以注意以下差异：

1. 不需要额外写 key，在 vue 中写 key 的作用是为了 diff 节点的时候找到它，确定是否需要重新渲染；
2. 在上述的演示中 App.vue 有这样一段代码 `    <img alt="Vue logo" src="./assets/logo.png" width="25%">`，在使用 vite 和 webpack 等工具时候会自动导入这个图片，但是在这里只会被简单处理为./assets/logo.png，如果你真的需要，请手动 import 导入这个图片
