---
layout: article
title: 建站备忘录-一键复制代码
tags: ["Customization"]
key: customization-02
clipboard: true
aside:
  toc: true
sidebar:
  nav: customization
---

> 为代码块添加一键复制功能。
<!--more-->

代码块的一键复制是非常实用的功能，不过原生TeXt主题却没有提供支持。这里参考[《为博客添加代码块一键复制功能》](https://be-my-only.xyz/blog/TeXt-copy-to-clipboard/)来实现相应的功能。

## 修改配置文件

要实现代码块的一键复制需要添加和修改如下配置文件：

```
jekyll-TeXt-theme
 ├── _data
 |     ├── variables.yml
 |     └── ...
 ├── _includes
 |     ├── scripts
 |     |    ├── lib
 |     |    ├──  ├── copy-to-clipboard.js
 |     |    |    └── ...
 |     |    └── ...
 |     ├── clipboard.html
 |     ├── copy-to-clipboard.html
 |     └── ...
 ├── _layouts
 |     ├── page.html
 |     └── ...
 ├── _sass
 |     ├── additional
 |     |    ├── _copy-to-clipboard.scss
 |     |    └── ...
 |     └── skins
 |     |    └── highlight
 |     |         ├── _default.scss
 |     |         ├── _tomorrow-night-blue.scss
 |     |         ├── _tomorrow-night-bright.scss
 |     |         ├── _tomorrow-night-eighties.scss
 |     |         ├── _tomorrow-night.scss
 |     |         └── _tomorrow.scss
 |     └── ...
 ├── assets
 |     ├── css
 |     |    └── main.scss
 |     └── ...
 ├── _config.yml
 └── ...
```

### 修改 variable.yml

在`_data/variables.yml`文件中添加`clipboard`变量以及资源地址，这里默认将`clipboard`设置为`false`。

```yml
default:
    ...
    clipboard: false
    ...

...
sources:
    bootcdn:
        ...
        clipboard: 'https://cdn.jsdelivr.net/npm/clipboard@2/dist/clipboard.min.js'

    unpkg:
        ...
        clipboard: 'https://unpkg.com/clipboard@2/dist/clipboard.min.js'
```

### 添加 copy-to-clipboard.js

在`_includes\scripts\lib`路径下新建`copy-to-clipboard.js`文件：

```js
(function() {
	// This script is built on clipboard.js, cf: https://clipboardjs.com/
	// 1. find all code blocks defined under snippet class
	var snippets = document.querySelectorAll('pre');
	[].forEach.call(snippets, function(snippet) {
		if (snippet.closest('.snippet') !== null) {
			snippet.firstChild.insertAdjacentHTML('beforebegin', '<button class="btn" data-clipboard-snippet><i class="far fa-copy"></i></button>');
		}
	});
	var clipboardSnippets = new ClipboardJS('[data-clipboard-snippet]', {
		target: function(trigger) {
			return trigger.nextElementSibling;
		}
	});
	clipboardSnippets.on('success', function(e) {
		e.clearSelection();
		showTooltip(e.trigger, 'Copied!');
	});
	clipboardSnippets.on('error', function(e) {
		showTooltip(e.trigger, fallbackMessage(e.action));
	});

	// 2. add event listener for all created copy button
	var btns = document.querySelectorAll('.btn');
	for (var i = 0; i < btns.length; i++) {
		btns[i].addEventListener('mouseleave', clearTooltip);
		btns[i].addEventListener('blur', clearTooltip);
		btns[i].addEventListener('mouseenter', showToolhint);
	}

	function clearTooltip(e) {
		e.currentTarget.setAttribute('class', 'btn');
		e.currentTarget.removeAttribute('aria-label');
	}

	function showTooltip(elem, msg) {
		elem.setAttribute('class', 'btn tooltipped tooltipped-s');
		elem.setAttribute('aria-label', msg);
	}

	function showToolhint(e) {
		e.currentTarget.setAttribute('class', 'btn tooltipped tooltipped-s');
		e.currentTarget.setAttribute('aria-label', 'copy to clipboard');
	}

	function fallbackMessage(action) {
		var actionMsg = '';
		var actionKey = (action === 'cut' ? 'X' : 'C');
		if (/iPhone|iPad/i.test(navigator.userAgent)) {
			actionMsg = 'No support :(';
		} else if (/Mac/i.test(navigator.userAgent)) {
			actionMsg = 'Press ⌘-' + actionKey + ' to ' + action;
		} else {
			actionMsg = 'Press Ctrl-' + actionKey + ' to ' + action;
		}
		return actionMsg;
	}
})();
```
{: .snippet}

## 激活代码块一键复制

## Reference

- [为博客添加代码块一键复制功能](https://be-my-only.xyz/blog/TeXt-copy-to-clipboard/)