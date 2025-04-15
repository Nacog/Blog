+++
date = '2025-04-15T13:28:45+08:00'
draft = true
title = 'MyFirstBlog'
author = 'Nacocx'
+++
# 经过

为了记录并且分享自己的学习经验，我决定搭建一个个人博客

一开始，我发现阿里云有99一年的云服务器，想着买一个配合WordPress搭建个人博客，结果搞了半天发现这玩意得备案，香港服务器又是1000元一年，一搜索如何备案又麻烦的要死，又害怕一些小的可以提供香港服务器的云跑路，就想看看还有没有别的选项，网上搜索了半天资料，准备用Azure，结果学生认证不了，又一搜发现Azure在国内好像没有学生认证免费用的活动了……

最终，在我仔细思考 ~~(问AI)~~ 后决定采用免费的github pages + hugo，然后就有了一堆问题 ~~(主要是我太菜了)~~

一开始我装了hugo的普通版本，用起来也没问题，结果在生成/public，把它放到仓库之后，它的css文件不能正常加载，问ai说是我要用hugo的extend版本

换好版本，再来一遍，还是不行，上网搜索，发现大佬，[解决问题](https://qing.shuncs.com/post/tech/hugo/)

```bash
git config --global core.autocrlf false
```

用这个指令，把回车符配置一下就行了   ~~我还是没懂为什么~~

然后我满怀激动地打开我的网页，博客格式正常了！结果点进博客，它直接给我跳转到了localhost:1313，问ai，说是我hugo.toml的baseURL没配置，我一看还真是:

```toml
baseURL＝"https://example.com/"
```

配置好了再次上传仓库，等待部署，结果，打开一看，还是不行。

然后我一气之下把整个东西删了重搞，结果就成功了？？？

我认为这个问题主要是出在PaperMod这个主题上，因为在我换了主题后，部署一次就成功了😅

而PaperMod非常麻烦，首先，要先把`themes\PaperMod\layouts\partials\templates`下的三个文件的

```html
{{- $images := partial "partials/templates/_funcs/get-page-images" . -}}
```

改成

```html
{{- $images := partial "/templates/_funcs/get-page-images" . -}}
```

就是把 `partials/` 删掉(前面名字`$images`之类的不一定一样，但后面都差不多)

其次，要在`hugo.toml`中加上

```html
[params.social]
    github = "https://github.com/xxx"
    email = "mailto:xxxx@xxxx"
```

很抽象

最终我选择了`hugo-theme-stack`主题,就是这个网站的主题，相当的好用😋