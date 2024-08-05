---
title: 标签组件
date: "2024-06-24 22:18:22"
categories: 使用
tags:
- 教程
#sticky:
#cover:
comments: true
toc: true
excerpt: "主题特有的自定义标签组件"
---

## 提示横幅 (AlertBar)

提示横幅是以横幅形式出现的提示信息。

### 格式

```md
{% alertbar <样式> <内容> %}
```

### 参数

#### 样式

共有 5 种样式可选：

{% alertbar primary "这是 `primary` 样式" %}

{% alertbar success "这是 `success` 样式" %}

{% alertbar info "这是 `info` 样式" %}

{% alertbar warning "这是 `warning` 样式" %}

{% alertbar danger "这是 `danger` 样式" %}

```md
{% alertbar primary "这是 `primary` 样式" %}
{% alertbar success "这是 `success` 样式" %}
{% alertbar info "这是 `info` 样式" %}
{% alertbar warning "这是 `warning` 样式" %}
{% alertbar danger "这是 `danger` 样式" %}
```

#### 内容

内容会被使用 Markdown 解析器解析。建议您在内容的两端加上英文的双引号，以确保参数传递正确。

{% alertbar primary "这是一个 提示横幅 (AlertBar) `alertbar`" %}

```md
{% alertbar primary "这是一个 提示横幅 (AlertBar) `alertbar`" %}
```

您可以设置多行内容，但出于美观考虑，不建议放置块状元素，如代码框等。

{% alertbar success "
这也是一个 提示横幅(AlertBar) 。

1. 提示内容 1
2. 提示内容 2
3. 提示内容...
" %}

```md
{% alertbar success "
这也是一个 提示横幅(AlertBar) 。

1. 提示内容 1
2. 提示内容 2
3. 提示内容...
" %}
```

## 提示面板 (AlertPanel)

提示面板是以内容框形式出现的大段提示信息。

### 格式

```md
{% alertpanel <样式> <标题> %}
<内容>
{% endalertpanel %}
```

### 参数

#### 标题

标题为提示面板顶端的信息。它会保留原格式，不会被解析。

{% alertpanel info "这是一个 提示面板 (AlertPanel)" %}
提示面板的内容
{% endalertpanel %}

#### 样式

共有 4 种样式可选：

{% alertpanel success "这是 success 样式" %}
success 的内容
{% endalertpanel %}

{% alertpanel info "这是 info 样式" %}
info 的内容
{% endalertpanel %}

{% alertpanel warning "这是 warning 样式" %}
warning 的内容
{% endalertpanel %}

{% alertpanel danger "这是 danger 样式" %}
danger 的内容
{% endalertpanel %}

```md
{% alertpanel success "这是 success 样式" %}
success 的内容
{% endalertpanel %}

{% alertpanel info "这是 info 样式" %}
info 的内容
{% endalertpanel %}

{% alertpanel warning "这是 warning 样式" %}
warning 的内容
{% endalertpanel %}

{% alertpanel danger "这是 danger 样式" %}
danger 的内容
{% endalertpanel %}
```

#### 内容

内容会被使用 Markdown 解析器解析，您可以自由加入任何您想要的元素。

{% alertpanel success "这是一个 提示面板 (AlertPanel)" %}

1. 提示内容 1
2. 提示内容 2
3. 提示内容...

```md
{% alertpanel success "这是一个 提示面板 (AlertPanel)" %}

1. 提示内容 1
2. 提示内容 2
3. 提示内容...

...其他东西

{% endalertpanel %}
```

{% endalertpanel %}

## 折叠内容 (Collapse)

折叠内容是以内容框形式出现的可以收缩或展开的信息。

### 格式

```md
{% collapse <标题> <打开?> %}
<内容>
{% endcollapse %}
```

### 参数

#### 标题

标题为折叠内容在折叠情况下用户唯一能看见的信息。它会保留原格式，不会被解析。

{% collapse 这是一个折叠内容 %}

这里是内容

{% endcollapse %}

```md
{% collapse 这是一个折叠内容 %}

这里是内容

{% endcollapse %}
```

#### 打开? *(可选)*

当这个选项被指定为 `open` 时，折叠内容在初始情况下是展开的，可以通过点击标题框来收缩。

{% collapse 这是一个预先展开的折叠内容 open %}

这里是内容

{% endcollapse %}

```md
{% collapse 这是一个预先展开的折叠内容 open %}

这里是内容

{% endcollapse %}
```

#### 内容

内容会被使用 Markdown 解析器解析，您可以自由加入任何您想要的元素。

{% collapse 您可以在折叠内容里放置任何内容 %}

```md
{% collapse 您可以在折叠内容里放置任何内容 %}

1. 被折叠的内容 1
2. 被折叠的内容 2
3. 被折叠的内容...

{% endcollapse %}
```

{% endcollapse %}

## 模糊字符 (Blur)

模糊字符是被模糊处理的字符。

### 格式

```md
{% blur <内容> %}
```

### 参数

#### 内容

内容是需要模糊的字符。它会保留原格式，不会被解析。

这里有一些{% blur 被模糊的字符 %}

```md
这里有一些{% blur 被模糊的字符 %}
```

## 链接列表 (LinkList)

链接列表是一块用于呈现包含图片、标题和描述的链接使用的组件。

与其他组件不同的是，它的数据并不直接配置在组件内部，而是通过 [链接列表](/posts/linklist/) 来管理。

### 格式

```md
{% linklist <列表ID> <列表顺序?> %}
```

### 参数

#### 列表ID

列表 ID 是指在链接列表里用于标记整个列表的唯一标识符，具体请参考链接列表页面的说明，此处不再赘述。

#### 列表顺序 *(可选)*

这个参数用于指引列表中各个链接具体使用的排序方式。它有两个可选值，分别为 `order` 和 `random` ，代表有序（遵从链接列表文件中的配置）或是无序的列表。

默认值是 `order` 。

为了优化性能，有序列表会在站点渲染时直接固化，而无序列表则会在储存列表信息后由运行时的浏览器随机生成。
