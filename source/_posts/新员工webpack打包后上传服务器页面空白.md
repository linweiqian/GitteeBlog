---
title: 新员工webpack打包后上传服务器页面空白
tags: 
- github
- (TortoiseGit)小乌龟
categories:
- github
- 工具
---

>某天同事小白使用了[webpack](https://so.csdn.net/so/search?q=webpack&spm=1001.2101.3001.7020)开发vue项目，在项目开发完成后，使用命令：npm run build对项目进行打包后发布服务器页面显示空白


![在这里插入图片描述](https://img-blog.csdnimg.cn/629f24153fec411087f2b053d0f19aa2.png)

排查后发现：webpack打包的时候引入js时使用的是绝对路径导致的
<!--more-->
## 解决方案如下

### 修改webpack打包文件中的配置：
- **webpack.prod.conf.js**中增加**publicPath:’./’** ；  

![在这里插入图片描述](https://img-blog.csdnimg.cn/3853a36695a24efa89c14da5273f5e1d.png)


- **util.js**中增加**publicPath:’./’**；(可选用或不用)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20ac18a376da47569da6493c4f19d7c6.png)

- **config/index.js**修改**assetsPublicPath：‘./’**;

![在这里插入图片描述](https://img-blog.csdnimg.cn/1063c7988a0e459c847d2246c7c46acf.png)

