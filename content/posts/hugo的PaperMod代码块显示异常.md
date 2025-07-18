---
title: "hugo的[PaperMod](https://github.com/adityatelange/hugo-PaperMod/)代码块显示异常"
date: "2025-07-18"
tags: ["Hugo", "PaperMod"]
---

如果没有设置代码语言的话，会显示异常，会被当成svg解析。

比如下面的：

```
int a = 100;
```

会显示成这样的

图片

可以通过修改配置修复

```
markup:
  highlight:
    noClasses: false
    guessSyntax: true
    codeFences: true
    style: monokai
```

