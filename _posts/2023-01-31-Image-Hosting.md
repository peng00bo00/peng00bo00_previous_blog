---
layout: article
title: 建站备忘录-图床
tags: ["Customization"]
key: customization-03
clipboard: true
aside:
  toc: true
sidebar:
  nav: customization
---

> 使用图床加载图片。
<!--more-->

利用图床可以方便地加载外部图片链接，而无需将图片上传到gitpage中。不过由于[Imgur](https://imgur.com/)在国内无法直接访问，在设置图片链接时需要使用一些**图片镜像缓存服务**来进行处理。具体来说只需要在图片的链接前添加镜像缓存的地址即可。

- 修改前图片链接：

```
https://i.imgur.com/agozP0s.gif
```

<div align=center>
<img src="https://i.imgur.com/agozP0s.gif" width="60%">
</div>

- 修改后图片链接：

```
https://pic1.xuehuaimg.com/proxy/i.imgur.com/agozP0s.gif
```

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/agozP0s.gif" width="60%">
</div>