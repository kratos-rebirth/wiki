---
title: 链接列表
date: "2024-08-04 21:00:08"
categories: 使用
tags:
- 教程
#sticky:
#cover:
comments: true
toc: true
---
因链接列表可能包含较为复杂且频繁变动的信息，为了避免给主题的配置选项造成干扰， V3 版本开始的主题使用放置于 `_data` 目录下的 `linklist.yml` 来管理具体对应的内容。
<!-- more -->

## 语法

这个文件使用的是 YAML 语法，也就是主题配置和站点配置文件使用的同一种语法。如果您有遇到语法提示报错，您可以参考相关的语法说明。

## 文件结构

一个链接列表文件中包含若干个平级的列表，每个列表的结构如下所示：

``yaml
<列表ID>:
- <链接成员1>
- <链接成员2>
- <链接成员3>
- <链接成员...>
```

即，每个列表：

1. 由一个 `列表 ID` 引领的若干个列表成员构成。
2. 包含若干个链接成员。

其中， `列表ID` 的命名要求符合一般的字符串规范。为避免可能出现的异常问题，我们推荐您使用小写字母、数字与下划线的组合，且使用小写字母作为开头。

为避免出现冲突，每个 `列表 ID` 均应为局部唯一的：即在这个站点实例的 linklist.yml 文件中，不能包含多个相同的 `列表 ID` ；但对于不同的站点实例来说并没有这个限制。

每个链接成员的结构如下所示：

``yaml
title: <链接标题>
description: <链接描述文本>
image: <链接代表图片地址>
link: <链接地址>
```

这四个字段都是文本型格式，其中 image 和 link 要求为有效的超链接（分别指向图片文件和目标位置），可以是相对路径也可以是绝对路径。

## 样例

一个简单的样例如下所示。

这个样例包含了两个链接列表：第一个的列表 ID 为 `linklistindata` ，包含 3 个链接；第二个的列表 ID 为 `awesome` ，包含 1 个链接。

```yaml
linklistindata:
- title: "猫猫①号"
  description: "喵~"
  image: "/images/user.svg"
  link: "https://candinya.com"
- title: "猫猫②号"
  description: "喵喵"
  image: "/images/user.svg"
  link: "https://candinya.com"
- title: "猫猫⑨号"
  description: "咪啪~"
  image: "/images/user.svg"
  link: "https://candinya.com"
awesome:
- title: "糖菓·部落"
  description: "Never drown the flame of hope"
  image: "https://candinya.com/images/candinya.webp"
  link: "https://candinya.com"
```
