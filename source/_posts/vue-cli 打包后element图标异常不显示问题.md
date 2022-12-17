---
title: vue-cli 打包后element图标异常不显示问题
tags: 
- vue
categories:
- vue
---
vue打包后如下element图标不显示
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200623151544162.png)
控制台报错
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200623151648633.png)
显示没有找到element-icons资源
解决办法：
在build文件下的utils.js文件中添加这一句**publicPath:'../../'**
找到我如下代码中去添加
<!--more-->
```bash

    // Extract CSS when that option is specified
    // (which is the case during production build)
    if (options.extract) {
      return ExtractTextPlugin.extract({
        use: loaders,
        fallback: 'vue-style-loader',
        publicPath:'../../'
      })
    } else {
      return ['vue-style-loader'].concat(loaders)
    }
  }
```
再打包一次
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200623152101665.png)
图标显示出来,大功告成
