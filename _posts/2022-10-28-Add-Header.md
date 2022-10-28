---
layout: article
title: 建站备忘录-添加新的标题页
tags: ["Customization"]
key: customization-01
aside:
  toc: true
sidebar:
  nav: customization
---

> 如何在TeXt主题中添加[Project](/projects.html)标题页进行项目展示。
<!--more-->

需要为网站添加新的标题页时可以按如下步骤进行操作：

## 添加页面文件夹

在根目录下新建文件夹`_projects`用来存放页面。

## 添加根页面

在根目录下新建文件`projects.md`作为根页面，文件内容可根据实际页面需求进行填写。


```yml
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

注意`data_source: site.projects`一行，这表示根页面会自动检索`site.projects`作为根页面下的文章。

## 修改config

修改根目录下的`_config.yml`文件，在`collections`项中添加`projects`：

```yml
collections:
  projects:
    output: true
```

然后在下面的`defaults`中添加新的scope：

```yml
defaults:
  ...

  ## Projects
  - scope:
      layout: article
      path: "_projects"
    values:
      nav_key: projects
    show_date: false
```

这样就把根目录下的`_projects`文件夹指定为`site.projects`。

## 修改navigation

修改`./_data`目录下的`navigation.yml`文件，在`header`项中添加标题：

```yml
header:
  ...

  - title:      Projects
    url:        /projects.html
    key:        projects
  
  ...
```

这样就把标题项Projects链接到`projects.md`上。