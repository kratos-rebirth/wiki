---
title: PJAX 事件
date: "2024-08-04 21:00:08"
categories: 开发
tags:
- 教程
#sticky:
#cover:
comments: true
toc: true
---
Kratos : Rebirth 使用了一种名为 PJAX (PushState + AJAX) 的技术来实现页面组件的部分更新，以避免对页面间的共享项（如站点播放器）产生干扰。因为这项技术并不会在页面更新时自动重新执行所有的脚本项，所以我们增加了一些事件，用于指引自定义的脚本在页面重载时被正确执行。
<!-- more -->

## 事件列表

事件列表及对应的详细解释如下：

| 事件          | 触发条件      | 说明                                                   |
| ------------- | ------------- | ------------------------------------------------------ |
| pjax:before   | PJAX 执行前   | 即将执行                                               |
| pjax:success  | PJAX 请求成功 | 已经成功拉取到数据，但还未确认是否为可以执行的有效内容 |
| pjax:complete | PJAX 执行完成 | 确认为有效的数据，并且完成了内容替换                   |
| pjax:error    | PJAX 遇到问题 | 请求失败或为无效内容等                                 |

一般关注的比较多的是 `pjax:success` 事件，例如针对评论系统，可以在监听到这个事件被执行时重新设置 `window.loadComments` 以便在 PJAX 完成后被自动执行。

## 监听事件

这些事件会在 window 载体对象上传播，因而可以直接在 window 上挂载事件监听器，例如：

```js
window.addEventListener(
  'pjax:success', // 事件名称
  () => { // 事件回调函数
    window.loadComments = loadComments;
});
```
