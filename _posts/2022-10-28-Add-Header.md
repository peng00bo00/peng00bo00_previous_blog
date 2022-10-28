---
layout: article
title: 建站备忘录-添加新的Header
tags: ["Customization"]
key: customization-01
aside:
  toc: true
sidebar:
  nav: customization
---

> 如何在TeXt主题中添加[Project](/projects.html)进行项目展示。
<!--more-->

需要为网站添加新的Header时可以按如下步骤进行操作：

## 添加页面文件夹

在根目录下新建文件夹`_projects`用来存放页面。

## 添加根页面

在根目录下新建文件`projects.md`作为根页面，文件内容可根据实际页面需求进行填写。


```md
---
layout: articles
title: Projects
key: projects
articles:
  data_source: site.projects
  type: grid
---

<div class="article__content" markdown="1">
```