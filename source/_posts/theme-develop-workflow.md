---
title: 二次开发流程
date: "2024-06-24 23:46:39"
categories: 开发
tags:
- 教程
#sticky:
#cover:
comments: true
toc: true
excerpt: "对主题本身的二次开发流程"
---
## 文件准备

我们使用 `pnpm` 作为项目的依赖项管理工具。您可以参照 [pnpm 的 安装教程] 来安装它。

[pnpm 的 安装教程]: https://pnpm.io/zh/installation

对于主题开发来说，我们需要尽可能还原一个新手用户的开箱即用的使用体验，因而我们需要暂时离开自己最喜欢最趁手的配置，使用一套较为简陋但不失公允的配置方案。例如，我会喜欢使用 [hexojs/hexo-theme-unit-test] 这个仓库来进行基础样式测试，以确保在一般默认条件下，各项功能和样式都能正常地展现。特别地，在样例站点中，我们使用的也是这一套测试配置。

[hexojs/hexo-theme-unit-test]: https://github.com/hexojs/hexo-theme-unit-test

git clone 这个仓库，创建一个 themes 目录， git clone 主题的仓库到 themes 下的 `kratos-rebirth` 中。整体的命令行看起来会像这样：

```shell
git clone https://github.com/hexojs/hexo-theme-unit-test.git Kratos-Rebirth-Dev
cd Kratos-Rebirth-Dev
mkdir themes
cd themes
git clone https://github.com/Candinya/Kratos-Rebirth.git kratos-rebirth
```

在这些都完成之后，我们需要使用一个简单的主题配置来展现主题的基本状态。推荐直接使用 [quickstart 仓库里的 _config.kratos-rebirth.yml] ，把它放到主目录下就可以。

[quickstart 仓库里的 _config.kratos-rebirth.yml]: https://github.com/kratos-rebirth/quickstart/blob/main/_config.kratos-rebirth.yml

这样就完成了基础的文件准备工作。

## 开发环境

我喜欢用 VSCode 作为开发的主要 IDE ，因为对于这种前端项目来说它足够轻量，同时又具有强大的可扩展性。

在界面排布方面，为方便使用，我会准备至少两个终端（命令行）窗口左右并排：
1. 一个在主目录下，负责控制整个 Hexo 实例的启停，或是 `hexo cl` 这种清空缓存的指令；
2. 另一个在 themes/kratos-rebirth 也就是我们的主题项目目录中，负责调用资源构建使用的代码。

如果屏幕的空间足够，还可以再开启一个终端窗口，方便在前两个都被占用时临时处理一些简单工作。

文件编辑器则可以根据自己的喜好排布，我的习惯也是二分或者三分屏，这样能更高效地利用屏幕空间，但代价是开发久了会开启很多没必要的标签页堆在一起。

## 基础配置

要开发主题，那么首先主题一定要选对。 `hexo-theme-unit-test` 仓库里的主题配置是 landscape ，我们把它改成 kratos-rebirth 就可以。

然后为了避免文件变更高亮被 gitignore 影响，我们可以删除 `hexo-theme-unit-test` 文件里的 themes 行。反正我们也不是向这个项目提交 PR ，所以改掉这里也无所谓。

之后是在两个终端都分别运行 `pnpm i` 来安装对应的基础依赖。不出意外的话，两边都能顺利完成。这样就完成了基础的配置工作。

## 启动预览

在启动实例预览之前，我们先要为主题构建最新的资源。

我们准备了一个简单的带有文件系统变更监听的构建工具脚本，在主题的终端运行 `pnpm watch` 即可调用它。当您看到 `构建资源...` 的输出后光标卡住不动了，那说明它已经成功启动了。

然后就可以在主目录的终端里运行 `hexo s` 来启动一个 Hexo 实例来测试了。

## 更新配置项

如果新引入的功能需要在配置文件里加入内容，那么应该加在哪个文件里呢？

对于主题来说，我们首先需要一个底层结构，以确保它在完全没有任何配置（包括 quickstart 里的样例）的时候也不会崩溃。针对这样的配置项，是需要添加到主题内部的 `_config.yml` 里面的；而一些用于增光添彩的配置项，例如顶部导航、侧边栏、评论与统计等内容，因为它的配置因人而异，提供一个绑定的模板可能会影响用户的使用体验，那么应当将它们放置在 quickstaty 里的样例配置选项中。

特别注意的是，因为 Hexo 在合并配置项时使用的是 deep merge ，这也意味着对应位置的两个数组里的所有成员都会被合并在一起，所以请确保在主题自带的配置文件中使用的所有数组都是空数组，以避免引入用户不想要又删不掉的东西。

## 同步更新相关仓库

有时主题的变更并不仅仅影响主题本身，还需要对相关的仓库，例如这个 Wiki ，或是 quickstart 里的配置样例进行同步的更新。提交 PR 请求的时候，记得不要忘了这些哦。
