---
title: 快速开始
date: "2024-06-24 01:12:16"
categories: 使用
tags:
- 教程
sticky: 1
#cover:
comments: true
toc: true
excerpt: "快速开始使用 Kratos : Rebirth 主题"
---
## 准备环境

Hexo 是一个基于 [Node.js] 的项目，所以您需要先准备 Node.js 环境来运行它。
- 我们推荐使用最新的 Node.js 稳定发布版本以支持新的特性，但通常情况下您也可以使用最新的 LTS 版本，具体差异请参考 Node.js 的版本发布说明。
- 我们没有测试过部分兼容的第三方环境（例如 bun 或 deno ）的支持，如果您在使用这些工具时遇到了奇怪的问题，欢迎随时 [开启一个 issue] 来让我们一起研究。

我们推荐您使用 `pnpm` 作为 Node.js 项目的依赖项管理工具。您可以参照 [pnpm 的 安装教程] 来安装它。

Kratos : Rebirth 是一个 Hexo 主题，所以您也需要在您的设备上预先 [安装 Hexo 命令行工具]。当然，如果您希望使用进阶管理方案，那么可以忽略这一步。

[Node.js]: https://nodejs.org/
[开启一个 issue]: https://github.com/Candinya/Kratos-Rebirth/issues/new/choose
[pnpm 的 安装教程]: https://pnpm.io/zh/installation
[安装 Hexo 命令行工具]: https://hexo.io/zh-cn/docs/

## 安装主题

### 新建一个实例

如果您想从零开始新建一个实例，我们为您准备了一个简单的启动模板仓库 [kratos-rebirth/quickstart] ，仅需三步即可创建：

1. 使用这个模板仓库，创建一个新的仓库。
    {% asset_img use-template.webp 使用模板 %}
    {% asset_img create-new-repository.webp 创建一个新的仓库 %}
2. git clone 您的仓库到本地。
3. 运行 `pnpm i` 来安装依赖环境。

[kratos-rebirth/quickstart]: https://github.com/kratos-rebirth/quickstart

### 已有的实例迁移

对于已经建立起 Hexo 实例，希望迁移到这个主题的用户来说，您只需要这样做：

1. 使用您的包管理工具（如 pnpm 或是 yarn 等） 安装 `hexo-theme-kratos-rebirth` 依赖。
2. 在您的站点配置文件 `_config.yml` 中，将 `theme` 配置改成 `kratos-rebirth` 。
3. 下载模板仓库的 `_config.kratos-rebirth.yml` 默认主题配置文件至您的仓库目录。

当您再启动 Hexo 实例时，应该就能看到这个新的主题了。

需要注意的是，如果您的旧主题存在一些特有的 自定义组件 ，那么它们在您更换主题后可能会出现错误。针对这种情况，我们推荐您尝试使用这个主题特有的 [自定义组件] 来替换它们。

[自定义组件]: /posts/custom-components/

{% alertpanel warning "尚未正式发布的版本" %}

当前主题的 V3 版本仍然处于开发阶段，暂时还未发布稳定版本；所以如果您需要使用它，请指定 `@next` 标记。例如：

```shell
pnpm i hexo-theme-kratos-rebirth@next
```

{% endalertpanel %}
