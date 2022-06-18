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
Github Actions 可以帮你自动执行 Hugo 的编译、部署，配置好之后平时只需要维护一份 hugo 博客的源码，push 时自动发布到 Github Pages 上。
### Github Action文件
你的 Github Pages 仓库需要有两个分支：一个分支 hugo 保存 hugo 博客源码，一个分支 `gh-pages` 保存生成的 `public` 静态网站。当然你另建一个独立的仓库保存博客源码也是可以的。

在 hugo 分支下新建 `.github/workflows/main.yml`，参照 actions-hugo 官方文档的描述添加：
```
name: Hugo

on:
  push:
    branches:
      - main  # 當main分支有push操作時

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # 找尋Hugo主題(true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod
      
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.94.2' # hugo 版本
          extended: true  # 如果是使用extended版本的務必取消註解。

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.HUGO_DEPLOY_TOKEN }}
          PUBLISH_BRANCH: gh-pages  # 推送到 gh-pages 分支
          PUBLISH_DIR: ./public     # hugo 生成的目錄
          commit_message: ${{ github.event.head_commit.message }}
```

### Deploy Key
`settings`->`Developer settings`->`Personal access tokens`->`Generate new token`,勾选`repo`即可<br/>
打开你的博客源码仓库，`Settings`->`Secrets`->`New repository secret`，Name 填 `HUGO_DEPLOY_TOKEN`,然后将Token粘贴即可。

## 参考
[使用 Github Actions 自动部署 Hugo 博客](https://zenlian.github.io/posts/tools/github-actions-hugo/#fn:4)</br>
[hugo博客自动化部署到github和云服务器上](https://www.liuvv.com/p/35554ffc.html)
