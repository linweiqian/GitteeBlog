---
title: vue 插槽的作用,用插槽slot-scope获取表格中的数据
tags: 
- vue
categories:
- vue
---

这里我用了**elementui**的表格组件去做表格,如图

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200703150434734.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDgwODY2OA==,size_16,color_FFFFFF,t_70)
我在编辑和删除的组件用**template**去包裹，然后在这个标签去写上**slot-scope="scope"**
<!--more-->
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200703145706564.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDgwODY2OA==,size_16,color_FFFFFF,t_70)
然后在需要点击的按钮去添加一个@click事件，在方法中去写上两个参数，第一个参数是当前点击按钮获取的表格在第几行的id,第二个参数是获取表格中当前行的全部参数
如图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200703150159410.png)
当我点击表格的第一行时我们看看打印出来的数据
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200703150342536.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDgwODY2OA==,size_16,color_FFFFFF,t_70)
现在我们是拿到了当前行的全部数据,大功告成

