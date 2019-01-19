---
layout: post
title: 博客折腾之路[0]
subtitle: 概述这个博客是怎么整出来的
gh-repo: Ezylryb-BK/Ezylryb-BK.github.io
gh-badge:
  - star
  - folk
  - follow
tags:
  - blog
comments: true
published: true
image: /img/qu.jpg
---

## 语言基础

**markdown**

markdown是一门轻量级的标记语言，是写博客的不错选择。我目前接触的两种静态框架`hexo`和`jekyll`都是支持markdown的，所以用起来很不错。除了写博客，利用vscode上的插件(比如我用的是Markdown Preview Enhanced)可以很方便地把md格式转换成html和pdf格式等，这样的话就可以用markdown写出漂亮的论文而不需要花过多精力排版，也可以画流程图，数学公式等而不需要再额外安装Latex。

**HTML**
HTML (Hypertext Markup Language, 超文本标记语言) 是一种用来结构化 Web 网页及其内容的标记语言。HTML 并不是编程语言，它是一种用于定义内容结构的标记语言。HTML 由一系列的元素（elements）所组成，这些元素可以用来封装不同部分的内容，使其以某种方式呈现或者工作。
了解一些主要的html的语法对搭建博客是大有益处的。

**CSS**
CSS (cascating style sheet, 层叠样式表) 也不是真正的编程语言。它也不是标记语言——是样式表语言。也就是说，它允许你有选择性地为 HTML 文档的元素添加样式。
利用CSS就可以为自己的博客设计漂亮的样式了。

**Javascript**
JavaScript 是一门为你的网站添加交互功能的编程语言。JS 是一门成熟的动态编程语言。当应用于 HTML 文档时，它可以在网站上提供动态交互性。
使用JS可以为网站添加一些小小的乐趣，比如跳出一些有趣的弹窗，制作一些动画效果等，目前我也只会写弹窗了，有待学习。

## 博客框架
{: .box-note}
什么是博客框架？
举个栗子叭: 现在假设我们要做一个Pre, 那么你就会去找一个适合你的pre的类型的漂亮的PPT模板，然后在这个模板的基础上做出你自己的PPT，那么我们就可以用PPT类型来类比博客框架，PPT模板来类比博客主题，最后经过适当的修改和创造，你就成功地在别人的脚手架上造出了自己独一无二的个人博客。

**框架的选择**
首先是动态和静态框架的选择。动态框架的主要优势在于它有原生的评论区，而静态框架的评论功能需要依赖于第三方，目前比较流行的第三方是`多说`。由于新手折腾动态比较麻烦，所以我选择的是静态框架。市面上比较受欢迎的两种静态框架是`hexo`和`jekyll`。相较于`jekyll`, `hexo`更方便安装，速度也更快。不过`jekyll`是github page直接支持的，所以为了偷懒我就使用了`jekyll`来搭建。(后来事实证明`jekyll`是非常麻烦的，我们将在后面谈及)

## 域名
搭建网站是要买域名的！！！如果你像我一样不想花钱买域名可以考虑利用github page来做一个个人博客，对一个初级选手来说300MB的大小是绰绰有余的，详细教程可以到github上看。如果购买域名的话万网应该是比较靠谱的。

## jekyll的本地环境搭建
就是这玩意，要在windows系统上搭建`jekyll`本地环境比`hexo`麻烦了N个层级。

安装`git`当然是前提啦。

现在我们要安装`bundler`,为了安装`bundler`我们必须先安装`Ruby`, 但是这里有一个比较大的坑，就是`Ruby`的最新版本是不支持gem的，所以建议下载安装`2.5.x`版本的。

安装完成后，打开git bash，敲入
```
$ gem install bundler
```
稍等一会儿，bundler就安装好了。

 接下来就是把你的远程jekyll site仓库clone到本地啦，这里我建议用GitHub Desktop, 十分方便。
 
 那么接下来将有一个大坑等着我们。网上的教程告诉我们接下来如果你的仓库里有Gemfile的话就敲一通以下命令
```
$ bundle install
```
但是我的却报错了
```
...could not find bundler...
```
探究了一番`bundle install`的原理之后，我意识到问题出在我的repository里还有一个Gerfile.lock文件，它导致了版本不相符的问题，于是我就把它删除了，重新执行bundle install，这条命令会生成新的Gerfile.lock文件。（没错，它install了很久很久...大概，10分钟？）

现在我们把新生成的Gerfile.lock文件push到我们的远程仓库里去，然后再运行
```
$ bundle exec jekyll serve
```
~~就大功告成了~~

大概会出一些岔子，比如我的time zone有问题了，那就运行
```
$ gem install tzinfo
```
接下来是修正bug的关键步骤，敲入：
```
$ bundle update
```
是的我们又要耐着性子等十几分钟了，不过它会帮你把版本全部更新的，这个操作不错。

那么，这时候总弄好了吧！不，`No repo name found`...恭喜你和我一样又入坑了...现在的正确姿势是打开你的_config文件，在底部加入这几行
```
repository: Yourname/Yourname.github.io
```
按理说现在应该搞定了的，可是为什么又冒出来了这个：
```
    Liquid Exception: Tag '{%' was not properly terminated with regexp: /\%}/
```
经过一番捣鼓，我发现有一些html文件里用的是`{%-  -%} `, 这种写法在commit时是不会报错的，但事实上正规的写法也许是`{%  %}`，经过测试，它们的功能应该是一样的，所以把它们一个一个揪出来改正就好啦！

最后我们终于可以欣慰地再来敲这一串命令了
```
$ bundle exec jekyll serve
```
好的，如果你看到这一串东西：
```
Configuration file: D:/Blog/Ezylryb-BK.github.io/_config.yml
            Source: D:/Blog/Ezylryb-BK.github.io
       Destination: D:/Blog/Ezylryb-BK.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 1.602 seconds.
  Please add the following to your Gemfile to avoid polling for changes:
    gem 'wdm', '>= 0.1.0' if Gem.win_platform?
 Auto-regeneration: enabled for 'D:/Blog/Ezylryb-BK.github.io'
Configuration file: D:/Blog/Ezylryb-BK.github.io/_config.yml
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```
Wow!恭喜你从坑里爬出来了，现在本地环境就已经搭建好了呢，可以打开这玩意`http://127.0.0.1:4000/`本地预览你的网站了呢。

持续更新