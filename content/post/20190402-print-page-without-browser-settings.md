---
title: 'Print Page without Browser Settings'
date: 2019-04-02T21:42:00+02:00
lastmod: 2019-04-02T21:42:00+02:00
draft: false
tags: []
categories: ['css']
---

## Summary

页面默认有页眉页脚信息，展现到页面外边距范围，通过去除页面模型的外边距，使得内容不会延伸到页面的边缘，再通过设置 body 元素的 margin 来保证 A4 纸打印出来的页面带有外边距。

<!--more-->

## Original posts

[Source](https://juejin.im/post/5c90d8085188252db75694dc)

```css
@media print {
	@page {
		margin: 0;
	}
	body {
		margin: 2cm;
	}
}
```
