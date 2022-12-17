---
title: vue 写相对路径图片不显示
tags: 
- vue
categories:
- vue
---

我们一般直接在vue的文件中直接引入路径是不能显示的,如图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200622151559220.png)
原因是因为webpack打包后本地路径丢失，所以我们在data中可以通过require去引入
改正后的代码
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200622151911814.png)
在data中定义值并传入路径
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200622151953826.png)
欧克欧克，大功告成
