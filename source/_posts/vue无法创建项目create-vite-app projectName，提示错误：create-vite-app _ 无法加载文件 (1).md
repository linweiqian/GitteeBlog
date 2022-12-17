---
title: vue无法创建项目create-vite-app projectName，提示错误：create-vite-app _ 无法加载文件 (1)
tags: 
- vue
categories:
- vue
---
运行命令**create-vite-app projectName**创建项目控制台提示报错如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210222221539631.png)
报错原因：我的是windows10没有管理权限，所以我们需要用管理员身份打开权限
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210222221804323.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDgwODY2OA==,size_16,color_FFFFFF,t_70)
<!--more-->
操作如下：
1.打开**windows PowerShell**右键点击看到以管理员身份运行点击后打开
2.输入 **set-ExecutionPolicy RemoteSigned**运行然后出现以下界面再输入**A**或者**Y**即可成功
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210222222232249.png)
然后我们在我们编辑器控制台重新输入上面的命令**create-vite-app projectName**创建文件即可成功
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210222222356918.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDgwODY2OA==,size_16,color_FFFFFF,t_70)


