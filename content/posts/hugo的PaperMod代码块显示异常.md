---
title: "hugo的PaperMod代码块显示异常"
date: "2025-07-18"
tags: ["Hugo", "PaperMod"]
---

如果没有设置代码语言的话，会显示异常，会被当成svg解析。

比如下面的：

```
int a = 100;
```

会显示成这样的

![image-20250718142236677](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718142245759.png)

可以通过修改配置修复

```
markup:
  highlight:
    codeFences: true        # ✅ 支持 Markdown 中的代码块语法
    guessSyntax: true       # ✅ 没写语言时尝试自动识别
    noClasses: false        # ✅ 启用 class，配合 CSS 生效
    style: monokai          # ✅ 你喜欢的代码样式
```

