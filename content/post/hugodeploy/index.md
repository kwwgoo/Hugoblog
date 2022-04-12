---
title: "Hugo Deploy"
date: 2022-04-12T13:33:49+08:00
description: "记录Hugo+GithubPage的部署过程"
draft: false
image: 'featured-image-preview.jpg'
categories:
    - tech
tags:
    - Hugo
hidden: false
lastmod: 
---
## 安装Hugo
按照[官方的快速开始](https://gohugo.io/getting-started/quick-start/)即可

也可以利用choco包管理器来进行安装
```
choco install hugo-extended -confirm
```

接着就可以建立自己的网站了

```
hugo new site myblog
```
## 添加主题
可以在 GitHub 仓库的 [Release](https://github.com/CaiJimmy/hugo-theme-stack/releases)页面找到最新的稳定版。 下载后把 hugo-theme-stack-master 改名为 hugo-theme-stack 并放到站点目录的 themes 文件夹下。

如果你在使用 Git 管理来 Hugo 站点的源文件，可以把主题添加为 Submodule。

需要先把Hugo站点文件初始化`git init`

然后使用命令

```
git submodule add https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack
```
但是这样把主题文件添加为子模块后没有文件，还需要两条命令
```
git submodule init
git submodule update
```
这样主题文件就出现了，当写下第一篇文章，并在本地检查没有错误后就可以部署到GithubPage了。

## 自动化部署

具体可以参考这篇文章,[如何將Hugo部落格部署到Github上?](https://yurepo.tw/2021/03/%E5%A6%82%E4%BD%95%E5%B0%87hugo%E9%83%A8%E8%90%BD%E6%A0%BC%E9%83%A8%E7%BD%B2%E5%88%B0github%E4%B8%8A/)
