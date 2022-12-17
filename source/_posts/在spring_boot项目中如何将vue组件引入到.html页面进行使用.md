---
title: 在spring_boot项目中如何将vue组件引入到.html页面进行使用
tags: 
- spring_boot
- webpack
categories:
- webpack
- 工具
---
开始我们需要导入我们的vue组件的路径到我们当前的js文件目录
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200619103950152.png)
然后我们需要用到一个函数**render**进行渲染，将定义的组件写到**createElements**函数中去
[想要详细了解render函数的使用可以进入](https://segmentfault.com/a/1190000010913794?utm_source=tag-newest)
如图
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020061910451966.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDgwODY2OA==,size_16,color_FFFFFF,t_70)
<!--more-->
 - ~~*在这里我刁侃下我当时是想要通过components函数去添加组件到.html页面去但是失败了，所以才使用了render函数*~~
接着我们需要在.html文件进行引入我们.js文件

```bash
<script src="./webapp/static/dist/custom.js"></script>
```
我再body标签直接写`<div id="app"></div>`就显示出来了,大功告成
