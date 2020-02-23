# fly-frame X公司flyjs模拟器

## 📦 What

X公司flyjs模拟器，可以在vue框架中调用flyjs的iframe模块

## 🚀 Why

X公司内部有段时间曾“盛行”过jquery+knockout组合而成的MVVM框架fly.js，后来由于种种原因，其逐渐退出历史舞台，但也造成了很多的历史债务问题。幸运的是，其主要设计者当时使用了iframe（同域传值）的方式设计了模态框，这意味着，即便开发新的页面，旧有的历史iframe模块页面，如果不需要更改，也能进行一定的复用。我们设计了在vue技术栈中，使用此工具调用旧有技术栈的模块。

```vue
<template>
    <div>
      <FlyFrame ref="flyframe" jquery="path/to/jquery.js" flyjs="path/to/flyjs.js">
    </div>
</template>

<script>
import FlyFrame from 'fly-frame';

export default {
  components: {FlyFrame},
  methods: {
    async open(){
      const data = await this.$refs['flyframe'].popup({
        id: "dialogId",
        title: "弹出框标题",
        width: "850px",
        height: "500px",
        parames: {},
        url: "/path/to/dialog.do"
      });
    }
  }
} 
</script>
```

# 🎮 How

`npm install fly-frame -S`

**jquery**: jquery.js。

**flyjs**: fly.js。

# 🤖 TODO

此版本的设计十分简陋，具体体现在：

* 此工具应当与具体技术选型解耦，当前局限于vue；
* 此工具应当设计为单例模式，且提供ready方法判断前置sdk是否已经装载；
* 此工具内置了当前业务的部分样式片段，通用性不强；

**此工具在当前业务中完全满足使用场景，目前没有计划做长期维护。**