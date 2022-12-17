---
title: vue 渲染列表报错Avoid using non-primitive value as key, use string_number value instead.  found in
tags: 
- vue
categories:
- vue
---
控制台报错
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200622141909928.png)
报错原因说v-for 循环的key值重复了，那就看看自己写的代码
报错时的代码，如下:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200622142203810.png)
我们可以在v-for循环里面再定义个index值,然后写到key 里面去
改正后的代码
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200622142345226.png)
报错解决，大功告成
