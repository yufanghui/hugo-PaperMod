---
title: "hugo的PaperMod代码块显示异常"
date: "2025-07-18"
tags: ["Hugo", "PaperMod"]
---

如果没有设置代码语言的话，会显示异常，会被当成svg解析。诡异的是我local没问题，远程就不行了。

比如下面的：

```
int a = 100;
```

会显示成这样的

![image-20250718142236677](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718142245759.png)

gpt提示可以这样修复

```
markup:
  highlight:
    codeFences: true        # ✅ 支持 Markdown 中的代码块语法
    guessSyntax: true       # ✅ 没写语言时尝试自动识别
    noClasses: false        # ✅ 启用 class，配合 CSS 生效
    style: monokai          # ✅ 你喜欢的代码样式
```

但是我尝试了没有用，最终还是通过添加代码解决的。把下面这段内容 **新建** 为

```
layouts/_default/_markup/render-codeblock.html
```

（你的站点根目录下如果没有这个路径，就自己把文件夹逐级建好；**不要**放到 `render-image.html` 里，那是专门渲染图片的钩子， 与代码块无关。）

拷贝如下内容

```go-html-template
{{/* 当没有标明语言时，强制用 plaintext 渲染，防止被误判成 SVG */}}
<pre><code class="language-plaintext">{{ .Inner }}</code></pre>
```

保存后，提交，所有没写语言标识的代码块都会以纯文本形式输出，不会被当作 SVG 渲染，也不会再出现异常样式。
