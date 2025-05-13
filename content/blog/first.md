---
title: 使用hugo搭建个人博客
date: 2025-05-11T22:02:34+08:00
tags: []
series: []
featured: true
---
如何使用hugo快速搭建个人博客的静态页面

<!--more-->

## hugo简介

🚀 超快构建速度：号称“世界上最快的静态网站生成器”，通常几百页内容也能在几秒钟内构建完成。  
📁 基于目录的内容组织：支持按照文件夹结构管理内容，易于维护。  
🧩 支持 Markdown 编写文章：用 Markdown 写内容，结构清晰，排版轻松。  
🎨 灵活的主题系统：拥有大量开源主题，支持自定义布局和样式。  
🔄 内置服务器支持热更新：hugo server 可启动本地预览服务器，修改内容后自动刷新页面。  
🌍 多语言支持：内建国际化功能，适合构建多语种网站。  
🧠 强大的模板引擎：支持条件语句、循环等，适合复杂内容展示。  
## 安装hugo
- macos安装方式
```bash
brew install hugo
```

安装完成之后的校验
```shell
hugo version
```
后续过程需要使用到git，请自行完成git的安装，也可以使用homebrew进行安装

```shell
brew install git
```
安装之后测试对github的连通性

```shell
ping github.com
```


## 快速初始化hugo

```shell
hugo new site quickstart
cd quickstart
git init
# 这条命令用于为hugo仓库添加主题，主题放置在 themes文件夹下，名为ananke
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
echo "theme = 'ananke'" >> hugo.toml
# 在本地启动hugo服务，默认在浏览器地址栏使用localhost:1313访问,同样可以使用127.0.0.1:1313进行访问
hugo server
```
可选ladder主题
```shell
git submodule add https://github.com/guangzhengli/hugo-theme-ladder themes/hugo-theme-ladder
```
若要使用ladder主题，请将`quickstart/hugo.toml`文件中的theme字段修改为
```shell
theme = 'hugo-theme-ladder'
```
修改保存之后，对应的修改会同步渲染到真在运行的服务器


## 配置理解

```shell
.
|-- archetypes
|-- assets
|-- content # 内容，后续博客文章将放置在这里
|-- data
|-- hugo.toml # 配置文件，菜单、评论、网站统计等所有功能，均可以通过直接配置进行开启
|-- i18n # 多语言
|-- layouts
|-- public
|-- resources
|-- static # 静态文件，如头像图片等
|-- themes # 所有主题以子文件夹的形式存放
```

## 创建博客
quickstart下 archetypes 文件夹中的 default.md 文件是用于控制创建新博客时的模板。

模板内容引用自up主白泽hugo教程
```shell
---
title: 博客标题
date: {{ .Date }}
tags: []
series: []
featured: true # 该参数决定了是否能在首页看到这篇文章的推荐
---
这是摘要

<!--more-->

这是内容

```
## 配置主页菜单

接下来继续配置根目录下的 `hugo.toml` ，创建几个菜单管理不同类目的博客。事实上，hugo 支持 toml 和 yaml 格式的配置文件，如果你并不习惯使用 toml，可以删除根目录的 `hugo.toml`，并创建 `hugo.yml` 进行相同配置的录入，也是可以生效的。
```toml
baseURL = 'https://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'hugo-theme-ladder'

[[menu.main]]
  name = "文章"
  url = "/blog/"
  weight = 1

[[menu.main]]
  name = "归档"
  url = "/archive/"
  weight = 2

[[menu.main]]
  name = "联系"
  url = "/contact/"
  weight = 3

[[menu.main]]
  name = "网站统计"
  url = "/xx/"
  weight = 4
```
### 尝试给首页加图片

```toml
baseURL = 'https://baize.github.io'
languageCode = 'en-us'
title = 'h2sl'
theme = 'hugo-theme-ladder'

[params]
    brand  = '主页'
    author = 'h2sl'
    info = '输出一些不会爆炸的有趣内容'
    authorDescription = "阅读｜思考｜产出｜进步"
    darkModeTheme = "data-dark-mode"
    #该目录为以contnet为根目录的相对目录
    avatarURL = "images/polarbear.png" 
   # favicon = "images/polarbear.png"
[params.options]
  showDarkMode = true
```


## 参考资料
[hugo官方doc](https://gohugo.io/getting-started/quick-start/)

[up主白泽hugo教程](https://baize.wiki/blog/how-to-build-blog/#ladder-主题)

