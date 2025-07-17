---
title: "Cloudflare Pages 部署Hugo blog 体验"
date: "2025-07-17"
tags: ["cloudflare"]

---

# frok模板仓库

今天研究了一下通过cloudflare部署一个网站，快是真的快。fork了一个hugo的官方模板

```js
https://github.com/adityatelange/hugo-PaperMod
```

# 建目录

然后新建了一个content/post和archives和search目录。

![image-20250717183116496](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250717183118386.png)

archives的模板

```yaml
---
title: "归档"
layout: "archives"
---
```

search的模板

```yaml
---
title: "搜索"
layout: "search"
---

```

# 配置config

新建了一个config.yml文件，简单配置下，提交，cloudflare就自动部署了，支持自定义子域名。

```js
baseURL: "https://blog.neoqingyi.xyz"
title: "Neo 的博客"
theme: "PaperMod"
languageCode: "zh-cn"
defaultContentLanguage: "zh"
pagination:
  pagerSize: 5  # 每页 5 篇文章

outputs:
  home:
    - HTML
    - RSS
    - JSON  # 🔍 搜索功能用到

taxonomies:
  tag: "tags"
  category: "categories"

menu:
  main:
    - name: 首页
      url: /
      weight: 1
    - name: 文章
      url: /posts/
      weight: 2
    - name: 标签
      url: /tags/
      weight: 3
    - name: 归档
      url: /archives/
      weight: 4
    - name: 搜索
      url: /search/
      weight: 5

# config.yaml
params:
  comments: true  
  # 1. 列表页全局隐藏封面
  cover:
    hiddenInList: true   # 只影响列表
  # 2. 详情页全局启用封面
  ShowCover: true        # 只影响文章页
  defaultTheme: auto
  ShowBreadCrumbs: true
  ShowPostNavLinks: true
  ShowWordCount: true
  ShowReadingTime: true

  homeInfoParams:
    Title: "你好，我是 Neo 👋"
    Content: "10年iOS工程师，热爱独立开发与写作。这个博客记录我探索 AI、自动化、自由生活的旅程。"

  socialIcons:
    - name: github
      url: "https://github.com/xxx"
    - name: twitter
      url: "https://twitter.com/xxx"
```



不过比较坑的就是调试样式，chatgpt给到的都是一些过时的语法，反复尝试修改配置文件，就是解决不了列表页面不展示图片，详情页展示图片的问题。最后询问kimi2解决了。

# 接入评论

然后就是配置评论系统，gpt推荐了很多，有的需要github账户才能评论，有的需要部署服务，挑选了一个最简单的，几乎零配置的---Cusdis。非常的简单，注册一个账户就有一定的免费额度

![image-20250717182829637](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250717182830895.png)

配置也相当的简单，加了一段div标签到comments.html里面

![image-20250717182715163](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250717182720547.png)

```html
<div id="cusdis_thread"
     data-host="https://cusdis.com"
     data-app-id="你的 App ID"
     data-page-id="{{ .Permalink }}"
     data-page-url="{{ .Permalink }}"
     data-page-title="{{ .Title }}">
</div>
<script async defer src="https://cusdis.com/js/cusdis.es.js"></script>
```

因为single.html内有引入comment.html的内容，所以无需再自己引入了

然后全局在config中打开评论，就成了。

```js
comments: true
```

唯一美中不足的是评论是一个iframe，单独的一个滚动区域，而不是跟着整体页面一起滚动，看起来比较丑陋。

![image-20250717183554363](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250717183555855.png)

尝试设置了下css总是不生效。也是chatgpt的内容过时了，现在要加到一个extended的目录下，而不是css目录下。

```js
your-project/
└── assets/
    └── css/
        └── extended/
            └── extra.css  ← 放在这里
```

# 感受

然后最后一个问题就是页面加载实在是太卡了。大概就是是因为挂在到了海外节点吧。哦，对了，还有一个问题，就是评论居然还要手动审核通过才能放粗来，有点不智能，ai时代了还需要手动处理，也太low了，最好不用approve最好，不过这样就可能有敏感信息的问题，算了，这些都不重要。

# 有用的命令

一个比较有用的命令是

```js
hugo server -D  
```

可以本地启动调试样式，避免部署之后才能看到效果。

重要的是没有输出，是在是不知道写什么。