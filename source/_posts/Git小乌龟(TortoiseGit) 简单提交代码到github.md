---
title: Git小乌龟(TortoiseGit) 简单提交代码到github
tags: 
- github
- (TortoiseGit)小乌龟
categories:
- github
- 工具
---
> 前言:由于提交代码到github时总是要提示验证登录,所以使用ssh提交方式

**第一步:检查本地主机是否已经存在ssh key**

```bash
cd ~/.ssh
ls
//看是否存在 id_rsa 和 id_rsa.pub文件，如果存在，说明已经有SSH Key
```
<!--more-->
![在这里插入图片描述](https://img-blog.csdnimg.cn/52d2decb1f48482ab99f5fcdc002a34b.png)
**第二步：生成ssh key**
如果不存在ssh key，使用如下命令生成

```bash
ssh-keygen -t rsa -C "xxx@xxx.com"
//执行后一直回车即可
```
生成完以后再用第二步命令，查看ssh key

**第三步：获取ssh key公钥内容（id_rsa.pub）**

```bash
cd ~/.ssh
cat id_rsa.pub
```

如下图所示，复制该内容
![在这里插入图片描述](https://img-blog.csdnimg.cn/72eae8753daf42018373a59b4efa418f.png)
**第四步：Github账号上添加公钥**
进入Settings设置
![在这里插入图片描述](https://img-blog.csdnimg.cn/24121ce90bd7436dab547c764cf87cce.png)
添加ssh key，把刚才复制的内容粘贴上去保存即可
![在这里插入图片描述](https://img-blog.csdnimg.cn/f65ac3b01e4f4c09be976577ec20bad0.jpeg)
**第五步：验证是否设置成功**

```bash
ssh -T git@github.com
```
显示如下信息表明设置成功
![在这里插入图片描述](https://img-blog.csdnimg.cn/08f6daec72c24a1c944050f7201a6a29.png)设置成功后，即可不需要账号密码clone和push代码
**注意之后在clone仓库的时候要使用ssh的url，而不是https！**

**第六步:小乌龟TortoiseGit配置:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/19b9a11cd3ec48df9804fab07053ed77.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/3d169ddd02e143fbaaf506a54d4cd6a7.png)
**验证原理**

> SSH登录安全性由非对称加密保证，产生密钥时，一次产生两个密钥，一个公钥，一个私钥，在git中一般命名为id_rsa.pub,
> id_rsa
> 
> 那么如何使用生成的一个私钥一个公钥进行验证呢？
> 
>  - 本地生成一个密钥对，其中公钥放到远程主机，私钥保存在本地
>  -  当本地主机需要登录远程主机时，本地主机向远程主机发送一个登录请求，远程收到消息后，随机生成一个字符串并用公钥加密，发回给本地。本地拿到该字符串，用存放在本地的私钥进行解密，再次发送到远程，远程比对该解密后的字符串与源字符串是否等同，如果等同则认证成功。

**[参考链接跳转](https://blog.csdn.net/weixin_42310154/article/details/118340458)**
