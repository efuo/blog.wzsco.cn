---
title: Git 必备技能：裸库操作
recommend: true
categories:
  - - 经验分享
    - Git
tags:
  - - 教程
  - - Git
abbrlink: 57059d11
cover: 'https://p.wzsco.top/ad73f38cb604bedccfeebe5bfd0a9c16.png/cover'
date: 2023-06-26 00:00:00
---

## 安装 & 创建 Git用户

安装 Git

- CentOS

```SHELL
yum install -y git
```

- Ubuntu

```SHELL
sudo apt-get install git
```

新增 Git 用户

```SHELL
groupadd git
adduser -g git git
```

Git 用户禁止 SSH 登陆
把`/bin/sh`改为`/usr/bin/git-shell`，用户就只能用来克隆或者推送数据到远程 git 仓库，而不能用它登录到主机。

打开文件

```shell
vim /etc/passwd
```

修改

```shell
    找到上一步添加的git用户
    git:x:1002:1002::/home/git:/bin/bash 
    修改
    git:x:1002:1002::/home/git:/usr/bin/git-shell
```

尝试使用 SSH 登录

```shell
    $ ssh git@[IP]
    Welcome to Ubuntu 22.04.2 LTS (GNU/Linux 5.15.0-75-generic x86_64)

    * Documentation:  https://help.ubuntu.com
    * Management:     https://landscape.canonical.com
    * Support:        https://ubuntu.com/advantage

    Welcome to Alibaba Cloud Elastic Compute Service !

    Last login: Mon Jun 26 12:48:56 2023 from [IP]
    fatal: Interactive git shell is not enabled.
    hint: ~/git-shell-commands should exist and have read and execute access.
    Connection to [IP] closed.
```

## 生成 SSH 密钥

打开本地终端，输入以下代码

```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

输出（默认路径即可，根据提示进行设置）

```text
> Generating public/private ALGORITHM key pair.
> Enter a file in which to save the key (/home/YOU/.ssh/ALGORITHM):[Press enter]
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

将 SSH 密钥添加到 ssh-agent

1. 在后台启动 ssh 代理。
    ```shell
    eval "$(ssh-agent -s)"
    # 输出以下内容表示成功
    > Agent pid 59566
    ```
2. 将 SSH 私钥添加到 ssh-agent。 如果使用其他名称创建了密钥或要添加具有其他名称的现有密钥，请将命令中的 id_ed25519
   替换为私钥文件的名称。
    ```shell
    ssh-add ~/.ssh/id_ed25519
    ```

新增 SSH 密钥到服务器

1. 复制本地生成的 SSH 密钥
   ```shell
   cat ~/.ssh/id_ed25519.pub
   ```
2. 将本地服务器生成的公钥放入远程服务器（直接粘贴，如果有多个，则一行一个）
   ```shell
   vim /home/git/.ssh/authorized_keys
   ```

## 裸库操作

初始化一个裸库

   ```shell
   mkdir [name] && cd [name]
   git init --bare [name].git
   ```

赋予Git 当前仓库读写权限

   ```shell
   chown -R git:git [name].git
   ```

本地与远程仓库关联

   ```shell
   git remote add [branch] ssh://git@[IP]/path/[name].git
   git push -u [local branch] [remote branch]
   -u: 将本地仓库的 Branch 和远程的 Branch 关联
   ```

克隆远程仓库

   ```shell
   git clone --branch [Branch] git@[IP]/path/[name].git [local folder]
   ```