---
title: vscode关于vue项目无法将文件push到github的错误命令
tags: 
- github
categories:
- github
---

## 错误提示一:

remote: Invalid username or password.
fatal: Authentication failed for 'https://github.com/linweiqian/master.git/'

## 错误提示二:

fatal: 'origin' does not appear to be a git repository
fatal: Could not read from remote repository.
<!--more-->
## 错误提示三:

Please make sure you have the correct access rights
and the repository exists.

## 错误提示四:

fatal: unable to access 'https://github.com/linweiqian/master.git/': Failed to connect to 127.0.0.1 port 1080: Connection refused

## 错误提示五:

On branch master,nothing to commit, working tree clean

## 错误提示六：

fatal: remote origin already exists.


## 解决办法

**重置设置**

```bash
git config --global credential.helper store
```

