---
title: 从 V2 版本升级迁移指南
date: "2024-06-24 23:34:45"
categories: 迁移
tags:
- 教程
#sticky:
#cover:
comments: true
toc: true
excerpt: "从 V2 版本升级到 V3 版本的迁移指南"
---

## 配置变更

V3 版本为了去掉历史遗留的兼容性包袱问题，对配置文件的格式进行了一次大的重写，这意味着您不能像从 V1 升级到 V2 那样，直接沿用旧的配置文件。

由于配置文件的改动部分过多，一一赘述会显得冗余且繁杂，结构性变更（例如大小写格式或位置排布等）请参考 [配置结构](/posts/configurations/) 进行修改，此处仅列出一些功能性变更的内容。

### 下雪与点击特效

由于这两种特效较为消耗资源，它们已不再被内置于主题中，而是以外部挂载的插件形式来引入。

具体请参阅：

- [下雪](https://eco.krt.moe/posts/effect-snow/)
- [点击效果](https://eco.krt.moe/posts/effect-click/)

### 打赏与分享

V3 版本的打赏功能不再依赖外部库，而是使用了主题内部的样式实现，因而也对打赏进行了自由平台实现的优化。具体的变更请参照 [配置结构](/posts/configurations/) 中对应章节的介绍。

V3 的分享功能使用了固定二维码 + 自定义平台模板的实现，请先阅读配置结构中对应部分的介绍。或者如果只是想要继续沿用 V2 版本中的那些平台的话，可以参考这个配置：

```yaml
# 分享组件设置
share:
  enable: true
  title: "分享这一刻"
  message: "让朋友们也来瞅瞅！"
  platforms:
    - name: "QQ"
      icon: "qq"
      color: "#00bfff"
      link: "https://connect.qq.com/widget/shareqq/index.html?url=$URL&title=$TITLE&desc=&summary=$SUMMARY&site=$SITE"
    - name: "QQ空间"
      icon: "star"
      color: "#fece00"
      link: "https://sns.qzone.qq.com/cgi-bin/qzshare/cgi_qzshare_onekey?url=$URL&title=$TITLE&desc=&summary=$SUMMARY&site=$SITE"
    - name: "微博"
      icon: "weibo"
      color: "#e6162d"
      link: "https://service.weibo.com/share/share.php?url=$URL&title=$TITLE"
    - name: "X"
      html: |
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon icon-tabler icons-tabler-outline icon-tabler-brand-x">
          <path stroke="none" d="M0 0h24v24H0z" fill="none" />
          <path d="M4 4l11.733 16h4.267l-11.733 -16z" />
          <path d="M4 20l6.768 -6.768m2.46 -2.46l6.772 -6.772" />
        </svg>
      color: "#000"
      link: "https://x.com/intent/tweet?text=$TITLE&url=$URL"
    - name: "Facebook"
      icon: "facebook"
      color: "#3e569b"
      link: "https://www.facebook.com/sharer/sharer.php?u=$URL"
```

### 评论与站点统计

由于评论系统丰富且更新较为频繁，想要支持市面上尽可能多的评论系统就会让主题变得臃肿，因而 V3 版本的评论功能不再内置于主题中，而是以外部挂载的插件形式来引入。您可以在周边站点的 [评论](https://eco.krt.moe/categories/%E8%AF%84%E8%AE%BA/) 分类中找到各个 V2 中旧有的评论系统的配置方案。

V3 版本同时也抽离了站点统计功能的支持，您可以在周边站点的 [访问统计](https://eco.krt.moe/categories/%E8%AE%BF%E9%97%AE%E7%BB%9F%E8%AE%A1/) 中尝试是否能找到一些您喜欢的统计工具。

### 站点验证

由于站点验证方式各不相同，在 V3 版本中同样抽离了特定平台的站点验证功能支持，而是推荐直接使用注入项来改动页面。

以下是 V2 中几个搜索引擎各自对应的站点验证方案配置，请选择您实际需要的来参考使用：

```yaml
additional_injections:
  head: | # 注意每一行对应一种搜索引擎（ Google / 百度 / Bing ），不是全部都要使用上的
    <meta name="google-site-verification" content="<Google搜索验证ID>" />
    <meta name="baidu-site-verification" content="<百度搜索验证ID>" />
    <meta name="msvalidate.01" content="<Bing搜索验证ID>" />
```

### （中国大陆网络服务）备案号

由于并不是每个站点都需要备案，在 V3 版本中不再内置备案图片资源与链接支持。您可以通过配置项来引入：

```yaml
footer:
  components:
    additional:
      - - <a href="https://beian.miit.gov.cn" rel="external nofollow" target="_blank">工信部备案号</a>
        - <a href="http://www.beian.gov.cn" rel="external nofollow" target="_blank"><img src="https://www.unpkg.com/hexo-theme-kratos-rebirth@2.2.0/source/images/psr.webp" width="12" height="12" loading="lazy" decoding="auto" />公安备案号</a>
```

### 友链

V3 版本中不再为友链设置单独的功能，而是使用 `linklist` 组件来实现。具体请参考 [标签组件](/posts/tag-widgets/) 中的 `链接列表 (LinkList)` 一节。

如果您使用的是页面生成模式，您只需要创建一个同名的页面，并放置一个对应的 linklist 组件即可。

### 随机文章封面图

由于 V2 版本中使用的随机图片存在版权问题，在 V3 版本中不再提供这些资源。我们提供了一个简单的实现脚本样例供您参考： [随机文章封面图](https://eco.krt.moe/posts/other-random-post-cover/) 。

## Front-Matter 更新

V3 版本的 Front-Matter 主要变更如下：

- `pic` 更名为 `cover`
- `only` 更名为 `show_in`
- `expire` 类型更改为指定过期天数

## 标签组件

标签组件主要更新为：

- `alertbox` 更名为 `alertbar`
- `colorpanel` 更名为 `alertpanel`

## 媒体资源

V2 版本中使用了一些未经版权许可的媒体资源，例如随机图片库、横幅及背景图片等，为了避免可能出现的版权纠纷，我们在 V3 版本中删去了这些资源，改用了完全自主可控的媒体资源来作为主题的呈现。

如果您仍想使用旧的资源，推荐您自己手动下载到本地使用（可以参考仓库的版本归档分支，或是参考旧的发布记录），或是使用指定版本的 npm 包的 CDN 来实现。
