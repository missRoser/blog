---
title: git_ssh
date: 2017-02-21 13:54:56
tags:
categories: 'tools'
---

git提交代码到github上和多个github帐号的SSH key切换

<!--more-->

第一步 创建ssh key
=============
在c盘users/Administrator下查看是否有.ssh文件.如果有,证明你已经创建过了,跳过该步骤.
如果没有，打开打开Git Bash，创建SSH Key：ssh-keygen -t rsa -C "自己的邮箱.com"，一路回车，会在~/.ssh/目录下生成id_rsa和id_rsa.pub两个文件。

第二步 登录github
=============
登录你的github账号
![](http://okyal4bzs.bkt.clouddn.com/ssh.png)
按上图中的1、2步打开如图界面，点击3创建一个ssh keys   title随便写，Key就是你本地的id_rsa.pub里的内容.填写完点击add ssh key就可以忘自己github上提交代码了。GitHub允许你添加多个Key，只要把每台电脑的Key都按照上面的方法添加到GitHub，就可以在每台电脑上往GitHub推送了。

第三步 不同github账号生成不同ssh key
=============
生成第二个sshkey ssh-keygen -t rsa -C "自己的邮箱.com"
这次不要一路回车了，给这个文件起一个名字 不然默认的话就覆盖了之前生成的第一个
起个名字  密码的话 可起可不起(随缘吧)

在.ssh/下创建config文件 内容如下

```host
Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa

Host warlock.github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/warlock

```
Host后面的名字随意起，然后测试是否能跑通ssh -T git@github.com

ssh提交的时候默认会读取id_rsa。如果要提交到另一个ssh上的时候需要提交的时候修改提交地址：
例子  git@my.github.com:username/repo.git(end)