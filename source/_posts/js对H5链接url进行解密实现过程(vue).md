---
title: js对H5链接url进行解密实现过程(vue)
tags: 
- javascript
categories:
- javascript
---

## https.js文件

```javascript
import Vue from 'vue'
export default {
  install(Vue) {
    Vue.prototype.$getQueryVariable = getQueryVariable
  }
};
//关键部分
function getQueryVariable(queryParams, query) {
  const query1 = query || window.location.search.substring(1);
  const vars = query1.split("&");
  for (let i = 0; i < vars.length; i++) {
    const pair = vars[i].split("=");
    if (pair[0] === queryParams) {
      return pair[1];
    }
  }
  return '';
}
```
<!--more-->
## vue文件使用部分

```javascript
let Base64 = require('js-base64').Base64;
let query = Base64.decode(window.location.search.substring(1).split('&')[0]);
//使用例子
//对url解码并匹配type的值
const type = this.$getQueryVariable('type', query);

```

