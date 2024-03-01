---
title: Solitude主题使用：部署友链朋友圈
date: '2024-01-31 08:35'
tags:
  - - Hexo
  - - 网页前端
categories:
  - - 经验分享
abbrlink: eb9bf33c
cover: 'https://p.wzsco.top//90de851b17633cbcb2b9a272e38696c5.png/cover'
---

## 后端部署
> Docker + Sqlite 的部署方式
> 使用 Ubuntu 22.04 作为服务器，1Panel 作为面板，Docker 作为容器，Sqlite 作为数据库。

1. 打开 1Panel 面板 进入 终端
    ![进入终端](https://p.wzsco.top//6da1fd51bfe90e8eb3b3b6271ece2fe8.gif/blogimg.gif)
2. 创建一个文件夹，用于存放项目文件，并CD进去
    ```bash
    mkdir -p docker/fcircle
    cd docker/fcircle
    ```
3. 克隆项目
    ```bash
    git clone https://github.com/Rock-Candy-Tea/hexo-circle-of-friends.git
    ```
    {% note simple success no-icon %}
    如果无法克隆，可以尝试使用国内镜像
    ```bash
    git clone https://gitee.com/KINGWDY_admin/hexo-circle-of-friends.git
    ```
    {% endnote %}
4. 进入项目文件夹，执行安装脚本，根据提示输入信息（推荐Docker）
    ```bash
    cd hexo-circle-of-friends
    python3 deploy.py
    ```
    {% note simple success no-icon %}
    如果你使用的Docker部署，可以提前pull镜像，加快部署速度
    ```bash
   docker pull yyyzyyyz/fcircle:latest
    ```
    {% endnote %}
5. 尝试请求
    ```bash
    curl 127.0.0.1:8000/all
    ```
   > 8000 端口是刚刚部署时使用的端口，如果你修改了端口，需要修改这里的端口
6. 部署网站
    ![部署网站](https://p.wzsco.top//cb6965c3da6324350741cf1f2a133f89.png/blogimg)
7. 访问
    ![访问](https://p.wzsco.top//269336c5efde981fc3f7f2d4f0da2eff.png/blogimg)

## 前端部署

1. New 一个新的页面
    ```bash
    hexo new page moments
    ```
2. 修改页面的 `index.md` 文件
    ```markdown
    ---
    title: 友链鱼塘
    desc: 最新文章订阅
    date: 2024-01-28 21:29:15
    type: "moment"
    cover: 'you image url'
    leftend: 使用 友链朋友圈 订阅友链最新文章
    ---
    ```
3. 修改主题的配置文件，找到 `moments` 部分
    ```yaml
      moments:
        enable: true # 是否开启鱼塘 / Whether to enable fish pond
        api: https://moment.wzsco.top/ # api地址 / api address
        error_img: https://bu.dusays.com/2023/11/08/654af68b25bb8.jpg # 加载失败显示图片 / Loading failed display image
        sort_rule: created # 排序规则：created：按创建时间排序 / updated：按更新时间排序 : Sort rule: created: Sort by creation time / updated: Sort by update time
        expire_days: 1 # 缓存过期时间（天），默认为1天 / Cache expiration time (days), default is 1 day
        page_init_number: 10 # 页面初始化加载数量，默认为10条 / Page initialization loading quantity, default is 10
        page_turning_number: 5 # 页面翻页加载数量，默认为5条 / Page turning loading quantity, default is 5
        angle: true # 鱼塘随机文章 / Fish pond random article
        appjs: https://cdn.cbd.int/solitude-source@1.0.3/js/fcircle.min.js # 鱼塘js / Fish pond js
        bundlejs: https://cdn.cbd.int/solitude-source/js/moment/bundle.min.js # 鱼塘js / Fish pond js
        randompostjs: https://cdn.cbd.int/solitude-source/js/moment/random_post.min.js # 鱼塘js / Fish pond js
    ```
   api 地址为你刚刚部署的地址
4. 重新生成网站运行查看
    ```bash
    hexo clean && hexo g && hexo s
    ```
5. 访问
    ![访问 Moments ](https://p.wzsco.top//34400cb55cb61aa8bc273c9d4ce582f5.png/blogimg)
6. 点击右下角的 `设置` 按钮，提示你输入密码，初始密码为你当前第一次输入的密码，切记不要忘记
    ![设置](https://p.wzsco.top//9e93f3547318e3fe01716a641c05cc99.png/blogimg)
7. 将其中的 `link` 部分的 `url` 修改为你的友链地址，主题选 `butterfly`

> 缓存过期时间为1天，所以不会实时更新，如果你想实时更新，可以在后端部署时，将 `expire_days` 设置为0