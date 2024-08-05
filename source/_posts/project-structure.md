---
title: 项目结构
date: "2024-06-24 23:41:28"
categories: 开发
tags:
- 教程
#sticky:
#cover:
comments: true
toc: true
excerpt: "Kratos : Rebirth 主题的结构详解"
---
Kratos : Rebirth 的主题结构与一般的 Hexo 主题（如默认的 landscape ）相似，但由于打包构建工具的引入所以又有些不同。各个目录与对应的内容如下：

## 平台相关

- `.github/` 目录中存放与 GitHub 相关的内容，例如构建流水线的定义与 issue 模板等，属于托管平台的专属内容，与主题本身无关。
- `.gitignore` 是使用 Git 作为版本管理工具时忽略掉的文件，避免无关文件对项目仓库造成不必要的污染。
- `.npmignore` 是在 NPM 平台发布软件包时需要忽略掉的文件，避免浪费额外的资源在没必要发布的文件上。

## 开发相关

- `.husky/` 存放的是使用 Husky 这个工具进行 git 联动的钩子，用于在 commit 时调用代码格式化工具。
- `devtools/` 里放置的是构建主题资源文件使用的脚本，包含以下三个文件：
  - `build-options.js` 构建配置。
  - `build-once.js` 单次构建。
  - `build-watch.js` 持续构建。
- `scripts` 里放置的是主题注入到 Hexo 使用的一些注入脚本文件。
  - `lib/cdn.js` 与 `cdn-optimize-helpers.js` 配合工作，引用 CDN 资源来加快一般站点加载速度。
  - `check-update.js` 在每次运行时检查主题是否有更新的发布版，以便提醒用户及时升级。
  - `additional-pages.js` 生成几个额外的页面： 404 页面、分类聚合页面、标签聚合页面。
  - `search.js` 提供搜索功能。
  - `tag-widgets.js` 提供主题自定义的 [标签组件](/posts/tag-widgets/) 。
  - `gen-jsconfig.js` 为 JavaScript 脚本生成运行时所需的配置项。
- `.prettierignore` 和 `.prettierrc` 是代码格式化工具 Prettier 使用的配置。
- `package.json` 和 `pnpm-lock.yaml` 是使用 pnpm 作为软件包及依赖管理工具时，所需的配置文件。
  - `package.json` 是所有 Node.JS 项目都有的项目信息文件。
  - `pnpm-lock.yaml` 是使用 pnpm 安装依赖时锁定的依赖版本。

## 主题相关

### i18n 国际化翻译

- `languages/` 里放置的是主题的 i18n 文件，目前仅有简体中文 `zh-CN` 的支持。

### 结构

- `layout/` 里放置的是主题的 HTML 结构代码模板（使用的是 ejs 模板引擎），其中各个目录与文件的作用如下（省略 .ejs 扩展名）：
  - `_index_style/` 存放的是三种首页文章的样式。
    - `card` 与 `half` 是二选一的选项
      - `card` 是经典的 Kratos 主题文章卡片
      - `half` 是类 landscape 那种展示一部分可以再展开阅读的样式。
  - `_modals/` 存放的是两个模态框（弹出窗口），分别是 `donate` 捐赠和 `share` 分享。
  - `_pages/` 存放的是几个主要页面的布局：
    - `categories` 是分类聚合页面
    - `tags` 是标签聚合页面
    - `search` 是搜索页面
    - `404` 是没有路径匹配时的回落页面
  - `_partial/` 存放的是一些共用的组件：
    - `head` 是页面头信息，主要存储页面的元数据，这些内容不会渲染到页面上，而是影响其他行为（例如标签页上的标题或是 OpenGraph 等）
    - `header` 是页面顶部，例如导航栏和桌面端的顶部横幅。
    - `footer` 是页面底部，例如页面底部的社交链接和底部文字。
    - `after-footer` 是页面不会渲染出来的底部内容，主要是存放与 JavaScript 脚本相关的内容。
    - `sidebar` 是站点的侧边栏结构。
    - `breadcrumb` 是分类索引页面和标签索引页面的文章列顶部的分级导航。
  - `_widget/` 存放的是侧边栏的小组件，具体组件可以参考配置里的介绍。
  - `layout` 是主要的结构文件，所有的页面都遵循这个结构。可以看到这里引用了很多上面提到的组件。
  - `index` 是首页的结构配置。
  - `archive` 是文章归档页面。
  - `category` 是分类索引页面。
  - `tag` 是标签索引页面。
  - `post` 是各个具体的文章（放置在站点的 source/_posts 目录中）渲染使用的页面。
  - `page` 是各个具体的页面（在站点的 source 目录中除 _posts 之外的目录）渲染使用的页面。

### 资源

- `source` 里存放的是会在站点实例构建时直接被应用的文件，主要都是些静态资源。
  - `images` 里放置的是主题默认的图片资源。
  - `vendors` 里放置的是主题使用到的依赖资源。
- `src` 里存放的是需要使用构建工具构建出主题资源文件时使用的原始文件。
  - `js` 里存放的是 JavaScript 脚本文件。
  - `scss` 里存放的是会构建成 CSS 样式表的样式定义文件。

### 其他

- `LICENSE` 是主题使用的开源授权。
- `ReadMe.md` 是主题的首屏介绍文档。
- `_config.yml` 是主题的默认基础配置。
