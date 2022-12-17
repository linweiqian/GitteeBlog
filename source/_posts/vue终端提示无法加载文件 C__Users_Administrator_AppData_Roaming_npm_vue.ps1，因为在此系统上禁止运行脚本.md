---
title: vue终端提示无法加载文件 C__Users_Administrator_AppData_Roaming_npm_vue.ps1，因为在此系统上禁止运行脚本
tags: 
- vue
categories:
- vue
---
**vue : 无法加载文件 C:\Users\Administrator\AppData\Roaming\npm\vue.ps1，因为在此系统上禁止运行脚本**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201125093115892.png#pic_center)
**解决方法：
1、管理员身份运行PowerShell（命令提示符，来源于Linux的命令提示符也叫Shell）**
<!--more-->
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020112509321439.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDgwODY2OA==,size_16,color_FFFFFF,t_70#pic_center)
**2、执行：set-ExecutionPolicy RemoteSigned （签名或运行这些脚本）**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201125093307810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDgwODY2OA==,size_16,color_FFFFFF,t_70#pic_center)
**3.重新在文件创建vue项目：vue create test**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201125093450705.png#pic_center)
**成功！**
