---
title: vue引入外部的css文件
tags: 
- vue
categories:
- vue
---
1.全局引入
引入外部文件只需在main.js文件中，例如
import './assets/YmOrder.css'
2.局部引入
在需要用到的vue文件进行局部引入,例如
<style scoped>
@import url('./assets/YmOrder.css');
</style>
