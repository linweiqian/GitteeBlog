---
title: 简单搭建一个vue3项目
tags: 
- vue3
categories:
- vue3
---

 - 第一步

```bash
$ npm i -g @vue/cli //全局安装最新vue构建工具 (默认最新)
```
vuecli安装成功如下
![在这里插入图片描述](https://img-blog.csdnimg.cn/0c7ca9da915f4e51aebeb22ae752b3f2.png)
<!--more-->
 - 第二步

```bash
$ vue create testvue3    //创建一个名为testvue3的项目
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/a792817f6e2844dd9bce71ff42fd65cf.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/c5d9781c1e4041a0bede8c85bc048d60.png)
- 第三步
执行$ cd testvue3 和$ npm run serve 命令
![在这里插入图片描述](https://img-blog.csdnimg.cn/f19085e4e57646eea8baea7e80c9e1c9.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/cbd79a9b428e49089de456d30b6bbea2.png)
- 第五步

> 代码文件报错 Parsing error: No Babel config file detected for
> D:\xk-project\demo\vue.config.js. Either disable config file checking
> with requireConfigFile: false, or configure Babel so that it can find
> the config files.eslint

![在这里插入图片描述](https://img-blog.csdnimg.cn/45bacc7b24144e69a1b88b7457b7ed70.png)
在package.json文件,按照下图指示添加"requireConfigFile" : false
![在这里插入图片描述](https://img-blog.csdnimg.cn/12fc91e4454b4516bcb9825b893d04c8.png)

