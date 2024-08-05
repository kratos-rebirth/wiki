---
title: 周边开发流程
date: "2024-06-24 23:47:16"
categories: 开发
tags:
- 教程
#sticky:
#cover:
comments: true
toc: true
excerpt: "对主题周边生态组件的开发流程"
---
针对主题的周边开发，核心在于灵活使用注入代码功能提供的接口。
<!-- more -->
以评论系统为例，首先是在 `comments` 配置段里添加注入模板，之后就是通过 `additional_injections` 配置段引入需要额外引入的文件。例如：

- 在 `head` 引入样式表文件
- 在 `footer` 配置段中往 DOM 中加入组件
- 在 `after_footer` 引入执行脚本

{% alertbar info "

从表现形式来讲， additional_injections 配置段的 footer 和 after_footer 的功能一致，并没有什么区别，拆开这两个主要是出于语义上的区分需要，即 footer 用于安置组件，而 after_footer 用于引入代码。您也可以使用您自己喜欢的配置方式来管理。

" %}

由于此处注入的脚本并不会在 PJAX 时自动重载，请添加针对 [PJAX 事件](/posts/pjax-events/) 的监听以确保重载后函数能在页面更新时被再次执行。

我们提供了一个 [周边站点](https://eco.krt.moe) 用于陈列一些周边的配置方案，如果您有相关开发参照或使用的需求，欢迎随时前往参考。
