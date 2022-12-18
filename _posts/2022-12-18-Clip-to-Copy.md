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

### 添加 .html

在`_includes\scripts`路径下新建`clipboard.html`和`copy-to-clipboard.html`两个html文件。

<div class="snippet" markdown="1">

{%- include snippets/get-sources.html -%}
{%- assign _sources = __return -%}

<script type="text/javascript" src='{{ _sources.clipboard }}'></script>
{: .language-html}
</div>

```
{%- include snippets/get-sources.html -%}
{%- assign _sources = __return -%}

<script type="text/javascript" src='{{ _sources.clipboard }}'></script>
```

```
{%- include snippets/assign.html target=site.data.variables.default.clipboard
  source0=site.clipboard source1=page.clipboard -%}
{%- if __return == true -%}
  {%- include clipboard.html -%}
<script async>
  {%- include scripts/lib/copy-to-clipboard.js -%}
</script>
{%- endif -%}
```

### 修改 page.html

在`_layouts/page.html`文件中添加执行`copy-to-clipboard.html`的指令：

```
...
{%- include copy-to-clipboard.html -%}
```

### 添加 .scss

在`_sass/additional`路径下添加`_copy-to-clipboard.scss`文件：

```scss
/*styles related to tooltips, borrowed from https://clipboardjs.com/bower_components/primer-css/css/primer.css*/
.tooltipped {
	position: relative
}

.tooltipped:after {
	position: absolute;
	z-index: 1000000;
	display: none;
	padding: 5px 8px;
	font: normal normal 11px/1.5 Helvetica, arial, nimbussansl, liberationsans, freesans, clean, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol";
	color: #fff;
	text-align: center;
	text-decoration: none;
	text-shadow: none;
	text-transform: none;
	letter-spacing: normal;
	word-wrap: break-word;
	white-space: pre;
	pointer-events: none;
	content: attr(aria-label);
	background: rgba(0, 0, 0, .8);
	border-radius: 3px;
	-webkit-font-smoothing: subpixel-antialiased
}

.tooltipped:before {
	position: absolute;
	z-index: 1000001;
	display: none;
	width: 0;
	height: 0;
	color: rgba(0, 0, 0, .8);
	pointer-events: none;
	content: "";
	border: 5px solid transparent
}

.tooltipped:hover:before, .tooltipped:hover:after, .tooltipped:active:before, .tooltipped:active:after, .tooltipped:focus:before, .tooltipped:focus:after {
	display: inline-block;
	text-decoration: none
}

.tooltipped-multiline:hover:after, .tooltipped-multiline:active:after, .tooltipped-multiline:focus:after {
	display: table-cell
}

.tooltipped-s:after, .tooltipped-se:after, .tooltipped-sw:after {
	top: 100%;
	right: 50%;
	margin-top: 5px
}

.tooltipped-s:before, .tooltipped-se:before, .tooltipped-sw:before {
	top: auto;
	right: 50%;
	bottom: -5px;
	margin-right: -5px;
	border-bottom-color: rgba(0, 0, 0, .8)
}

.tooltipped-se:after {
	right: auto;
	left: 50%;
	margin-left: -15px
}

.tooltipped-sw:after {
	margin-right: -15px
}

.tooltipped-n:after, .tooltipped-ne:after, .tooltipped-nw:after {
	right: 50%;
	bottom: 100%;
	margin-bottom: 5px
}

.tooltipped-n:before, .tooltipped-ne:before, .tooltipped-nw:before {
	top: -5px;
	right: 50%;
	bottom: auto;
	margin-right: -5px;
	border-top-color: rgba(0, 0, 0, .8)
}

.tooltipped-ne:after {
	right: auto;
	left: 50%;
	margin-left: -15px
}

.tooltipped-nw:after {
	margin-right: -15px
}

.tooltipped-s:after, .tooltipped-n:after {
	-webkit-transform: translateX(50%);
	-ms-transform: translateX(50%);
	transform: translateX(50%)
}

.tooltipped-w:after {
	right: 100%;
	bottom: 50%;
	margin-right: 5px;
	-webkit-transform: translateY(50%);
	-ms-transform: translateY(50%);
	transform: translateY(50%)
}

.tooltipped-w:before {
	top: 50%;
	bottom: 50%;
	left: -5px;
	margin-top: -5px;
	border-left-color: rgba(0, 0, 0, .8)
}

.tooltipped-e:after {
	bottom: 50%;
	left: 100%;
	margin-left: 5px;
	-webkit-transform: translateY(50%);
	-ms-transform: translateY(50%);
	transform: translateY(50%)
}

.tooltipped-e:before {
	top: 50%;
	right: -5px;
	bottom: 50%;
	margin-top: -5px;
	border-right-color: rgba(0, 0, 0, .8)
}

.tooltipped-multiline:after {
	width: -webkit-max-content;
	width: -moz-max-content;
	width: max-content;
	max-width: 250px;
	word-break: break-word;
	word-wrap: normal;
	white-space: pre-line;
	border-collapse: separate
}

.tooltipped-multiline.tooltipped-s:after, .tooltipped-multiline.tooltipped-n:after {
	right: auto;
	left: 50%;
	-webkit-transform: translateX(-50%);
	-ms-transform: translateX(-50%);
	transform: translateX(-50%)
}

.tooltipped-multiline.tooltipped-w:after, .tooltipped-multiline.tooltipped-e:after {
	right: 100%
}

/*styles related to snippet copy to clipboard, borrowed from https://clipboardjs.com/assets/styles/main.css*/
.fa-copy {
	margin-top: -3px;
	position: relative;
	top: 3px
}

.btn[disabled] .fa-copy {
	opacity: .3
}

.snippet {
	position: relative;
	overflow: visible
}

.snippet .btn {
	-webkit-transition: opacity .3s ease-in-out;
	-o-transition: opacity .3s ease-in-out;
	transition: opacity .3s ease-in-out;
	opacity: 0;
	padding: 2px 6px;
	position: absolute;
	right: 4px;
	top: 4px;
	color: $copy-button-color
}

.snippet:hover .btn, .snippet .btn:focus {
	opacity: 1
}
```
{: .snippet}

为`_sass/skins/highlight`路径下的`.scss`文件添加`copy-button-color`的定义。其中`_default.scss`和`_tomorrow.scss`定义颜色为：

```scss
// copy button color
$copy-button-color: #000;
```
{: .snippet}

其它`.scss`文件中定义颜色为：

```scss
// copy button color
$copy-button-color: #fff;
```
{: .snippet}

在`assets/css/main.scss`中添加样式：

```scss
...
"additional/copy-to-clipboard"
...
```

### 修改 _config.yml

最后在`_config.yml`文件中将`clipboard`默认值设置为`false`

```yml
...
## => Clipboard
##############################
clipboard: false
...
```

## 激活代码块一键复制

到此为止我们就完成了全部的配置工作。由于`clipboard`默认为`false`，新建的文档不会自动支持代码块的一键复制功能。对于需要激活一键复制的文档需要在header中将`clipboard`设置为`true`：

```md
---
...
clipboard: true
...

---
```

然后对于需要使用一键复制功能的代码块，只需要在结尾处添加`{: .snippet}`即可。

<div class="snippet" markdown="1">

~~~
<div class="snippet" markdown="1">

```
def hello():
    print('Hello world!')
```
{: .language-python}
</div>
~~~
{: .language-html}
</div>


## Reference

- [为博客添加代码块一键复制功能](https://be-my-only.xyz/blog/TeXt-copy-to-clipboard/)