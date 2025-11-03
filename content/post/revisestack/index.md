---
title: "魔改stack主题"
date: 2022-04-12T17:34:53+08:00
description: "记录一些魔改的教程"
draft: false
image: 
categories:
    - tech
tags:
    - stack
    - hugo
hidden: false
lastmod: 
slug: "revisestack"
---
## 样式修改
所有自定样式CSS代码都在`\assets\scss\custom.scss`中，修改的地方都已经注释
```css
/* Place your custom SCSS in HUGO_SITE_FOLDER/assets/scss/custom.scss */
// 设置选中字体的区域背景颜色
::selection {
    color: #fff;
    background: #557697;
  }
  
  ::-moz-selection {
    color: #fff;
    background: #557697;
  }
  
  ::-webkit-selection {
    color: #fff;
    background: #557697;
  }

:root {
    // 字体颜色
    --card-text-color-main: #34495e;
}

:root {
    // 行内代码背景色
    --code-background-color: #f8f8f8;
    // 行内代码前景色
    --code-text-color: #e96900;
}

//链接颜色修改
a {
    text-decoration: none;
    color: var(--accent-color);

    &:hover {
        color: var(--accent-color-darker);
    }

    &.link {
        color: #42b983;
        font-weight: 600;
        padding: 0 2px;
        text-decoration: none;
        cursor: pointer;
        
        &:hover{
            text-decoration: underline;
        }
    }
}


//滚动条美化
.widget--toc {
    #TableOfContents {
        max-height: 65vh;

        ol,
        ul {
            list-style-type: none;
        }

        li {
            margin: 10px 10px;

            & > ol,
            & > ul {
                margin-top: 10px;
                padding-left: 10px;
                margin-bottom: -5px;

                & > li:last-child {
                    margin-bottom: 0;
                }
            }
        }
    }
}
//全局滚动条美化
html{
    ::-webkit-scrollbar {
        width: 20px;
      }
      
      ::-webkit-scrollbar-track {
        background-color: transparent;
      }
      
      ::-webkit-scrollbar-thumb {
        background-color: #d6dee1;
        border-radius: 20px;
        border: 6px solid transparent;
        background-clip: content-box;
      }
      
      ::-webkit-scrollbar-thumb:hover {
        background-color: #a8bbbf;
      }
}

// 页面配色样式####################################################################
:root {
    // 右边栏菜单字体大小
    .section-title {
        font-size: 1.8rem;
    }
    // 菜单字体大小
    .menu {
        font-size: 1.9rem;
    }
    // 文章内容图片圆角阴影
    .article-page .main-article .article-content {
        img {
            max-width: 92% !important;
            height: auto !important;
            box-shadow: 0 0px 10px 2px #636b904d;
            border-radius: 8px;
        }
    }
    // 文章内容引用块左边样式
    .article-content {
        blockquote {
            border-left: 6px solid #1bcdfc !important;
            border-radius: 6px;
        }
    }
    // 字体颜色
    --card-text-color-main: #34495e;
    // 默认模式下引用块背景样式
    --blockquote-background-color: #b9ebea4d;
    // 全局字体大小
    --article-font-size: 2.0rem;
    // 表格配色样式
    --tr-even-background-color: #eff0fa54 !important;
    &[data-scheme="dark"] {
        //    暗黑模式下引用块背景样式
        --blockquote-background-color: #313f5645;
        // 整页背景配色
        --body-background: #000;
        // 卡片配色
        --card-background: #191d24;
        // 表格配色样式
        --tr-even-background-color: #1e242ecf !important;
        // 文章内容引用块左边样式
        .article-content {
            blockquote {
                border-left: 6px solid #33619b8c !important;
                border-radius: 6px;
            }
        }
    }
}

```
## 友链引入
主要参考[雨临Lewis](https://lewky.cn/posts/hugo-3.html/)的样式
### 友链界面
新建`\content\page\friends\index.md`
文件内容如下
```markdown
---
title: "Friends"
date: 2022-04-10T20:52:18+08:00
layout: "friends"
slug: "friends"
menu:
    main:
        weight: -50
        params: 
            icon: hash
---
```
### 友链样式
>主要是利用shortcode的原理，具体可参考[shorcodes](https://blog.echosec.top/p/hugo-shortcode/)
新建`assets\scss\friend.scss`,添加如下代码
```css
.friend.url {
    text-decoration: none !important;
    color: black;
}

.friend.logo {
    width: 56px !important;
    height: 56px !important;
    border-radius: 50%;
    border: 1px solid #ddd;
    padding: 2px;
    margin-top: 14px !important;
    margin-left: 14px !important;
    background-color: #fff;
}

.friend.block.whole {
    height: 92px;
    margin-top: 8px;
    margin-left: 4px;
    width: 31%;
    display: inline-flex !important;
    border-radius: 5px;
    background: rgba(14, 220, 220, 0.15);

    &.shadow {
        margin-right: 4px;
        box-shadow: 4px 4px 2px 1px rgba(0, 0, 255, 0.2);
    }
    &.borderFlash {
        border-width: 3.5px;
        border-style: solid;
        animation: borderFlash 2s infinite alternate;
    }
    &.led {
        animation: led 3s infinite alternate;
    }
    &.bln {
        animation: bln 3s infinite alternate;
    }
}

.friend.block.whole {
    &:hover {
        color: white;
        & .friend.info {
            color: white;
        }
    }

    &.default {
        --primary-color: #215bb3bf;
        &:hover {
            background: rgba(33, 91, 179, 0.75);
        }
    }
    &.red {
        --primary-color: #e72638;
        &:hover {
            background: rgba(231, 38, 56, 0.75);
        }
    }
    &.green {
        --primary-color: #2ec58d;
        &:hover {
            background: rgba(21, 167, 33, 0.75);
        }
    }
    &.blue {
        --primary-color: #2575fc;
        &:hover {
            background: rgba(37, 117, 252, 0.75);
        }
    }
    &.linear-red {
        --primary-color: #e72638;
        &:hover {
            background: linear-gradient(to right, #f9cdcd 0, #e72638 35%);
        }
    }
    &.linear-green {
        --primary-color: #2ec58d;
        &:hover {
            background: linear-gradient(to right, #1d7544 0, #2ec58d 35%);
        }
    }
    &.linear-blue {
        --primary-color: #2575fc;
        &:hover {
            background: linear-gradient(to right, #6a11cb 0, #2575fc 35%);
        }
    }
}

.friend.block.whole .friend.block.left img {
    &.auto_rotate_left {
        animation: auto_rotate_left 3s linear infinite;
    }
    &.auto_rotate_right {
        animation: auto_rotate_right 3s linear infinite;
    }
}
.friend.block.whole:hover .friend.block.left img {
    &.rotate {
        transition: 0.9s !important;
        -webkit-transition: 0.9s !important;
        -moz-transition: 0.9s !important;
        -o-transition: 0.9s !important;
        -ms-transition: 0.9s !important;
        transform: rotate(360deg) !important;
        -webkit-transform: rotate(360deg) !important;
        -moz-transform: rotate(360deg) !important;
        -o-transform: rotate(360deg) !important;
        -ms-transform: rotate(360deg) !important;
    }
}

.friend.block.left {
    width: 92px;
    min-width: 92px;
    float: left;
}

.friend.block.left {
    margin-right: 2px;
}

.friend.block.right {
    margin-top: 18px;
    margin-right: 18px;
}

.friend.name {
    overflow: hidden;
    font-weight: bolder;
    word-wrap:break-word;
    word-break: break-all;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 1;
    -webkit-box-orient: vertical;
}

.friend.info {
    margin-top: 3px;
    overflow: hidden;
    word-wrap:break-word;
    word-break: break-all;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    line-height: normal;
    font-size: 0.8rem;
    color: #7a7a7a;
}

@media screen and (max-width: 900px) {
    .friend.info {
        display: none;
    }
    .friend.block.whole {
        width: 45%;
    }
    .friend.block.left {
        width: 84px;
        margin-left: 15px;
    }
    .friend.block.right {
        height: 100%;
        margin: auto;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .friend.name {
        font-size: 14px;
    }
}

@keyframes bln {
	0% {
		box-shadow: 0 0 5px grey,inset 0 0 5px grey,0 1px 0 grey;
		box-shadow: 0 0 5px var(--primary-color,grey),inset 0 0 5px var(--primary-color,grey),0 1px 0 var(--primary-color,grey)
	}

	to {
		box-shadow: 0 0 16px grey,inset 0 0 8px grey,0 1px 0 grey;
		box-shadow: 0 0 16px var(--primary-color,grey),inset 0 0 8px var(--primary-color,grey),0 1px 0 var(--primary-color,grey)
	}
}

@keyframes led {
	0% {
		box-shadow: 0 0 4px #ca00ff
	}

	25% {
		box-shadow: 0 0 16px #00b5e5
	}

	50% {
		box-shadow: 0 0 4px #00f
	}

	75% {
		box-shadow: 0 0 16px #b1da21
	}

	to {
		box-shadow: 0 0 4px red
	}
}

@keyframes borderFlash {
	0% {
		border-color: white;
	}

	to {
		border-color: grey;
		border-color: var(--primary-color,grey)
	}
}

@keyframes auto_rotate_left {
	0% {
		transform: rotate(0)
	}

	to {
		transform: rotate(-1turn)
	}
}

@keyframes auto_rotate_right {
	0% {
		transform: rotate(0)
	}

	to {
		transform: rotate(1turn)
	}
}

```
### 创建友链shortcode
新建文件`layouts\shortcodes\friend.html`，添加如下代码
```html
{{ $options := (dict "targetPath" "/scss/friend.css" "outputStyle" "compressed" "enableSourceMap" true) }}
{{ $style := resources.Get "scss/friend.scss" | css.Sass $options }}

<link rel="stylesheet" href="{{ $style.RelPermalink }}">

{{ if .IsNamedParams }}
{{ $defaultImg := "https://sdn.geekzu.org/avatar/d41d8cd98f00b204e9800998ecf8427e?d=retro" }}
	<a target="_blank" href={{ .Get "url" }} title={{ .Get "name" }}---{{ .Get "word" }} class="friend url">
	  <div class="friend block whole {{ .Get "primary-color" | default "default"}} {{ .Get "border-animation" | default "shadow"}}">
		<div class="friend block left">
		  <img class="friend logo {{ .Get "img-animation" | default "rotate"}}" src={{ .Get "logo" }} onerror="this.src='{{ $defaultImg }}'" />
		</div>
		<div class="friend block right">
		  <div class="friend name">{{ .Get "name" }}</div>
		  <div class="friend info">"{{ .Get "word" }}"</div>
		</div>
	  </div>
	</a>
{{ end }}
```
### 友链使用
在你想要引入友链的文章里使用下面的代码即可自动渲染成对应的友链：
```css
{/{< friend
name="雨临Lewis的博客"
url="lewky.cn"
logo="https://cdn.jsdelivr.net/gh/lewky/lewky.github.io@master/images/avatar.jpg"
word="不想当写手的码农不是好咸鱼_(xз」∠)_"
>}/}
```
上面添加`/`只是为了转义，防止识别错误，使用过程中不添加。

上面代码里的四个属性为必填项，还可以额外指定三个不同的属性来选择友链内置的多种样式，如下：
```
//边框及鼠标悬停的背景颜色，允许设置渐变色
//支持7种：default、red、green、blue、linear-red、linear-green、linear-blue
primary-color="default"

//头像动画：rotate(鼠标悬停时旋转，此为默认效果)、auto_rotate_left(左旋转)、auto_rotate_right(右旋转)
img-animation="rotate"

//边框动画：shadow(阴影，此为默认效果)、borderFlash(边框闪现)、led(跑马灯)、bln(主颜色呼吸灯)
border-animation="shadow"
```
效果如下：

{{< friend
name="雨临Lewis的博客"
url="lewky.cn"
logo="https://cdn.jsdelivr.net/gh/lewky/lewky.github.io@master/images/avatar.jpg"
word="不想当写手的码农不是好咸鱼_(xз」∠)_"
>}}


## 添加文章自动更新功能
在`config.yml`中添加
```
enableGitInfo: true
frontmatter:
  #lastmod: [":fileModTime", "lastmod"]
    lastmod: [":git", "lastmod"]
```

>主要参考
>[小球飞鱼](https://mantyke.icu/2022/stack-theme-mod/)
>[Echosec](https://blog.echosec.top/p/custom-hugo-theme-styles/)
>[XR_G's Blog](https://xrg.fj.cn/p/%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA%E6%8C%87%E5%8D%973/)
>[雨临Lewis](https://lewky.cn/posts/hugo-3.html/)
>[zhixuan's Blog](https://blog.zhixuan.dev/posts/ac760353/)
>[L1nSn0w's Blog](https://blog.linsnow.cn/)