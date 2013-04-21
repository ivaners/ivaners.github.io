---
layout: post
title: "github+jekyll搭建博客"
description: ""
category: 
tags: []
---
{% include JB/setup %}

###Jekyll是什么

> Jekyll是一个静态网站生成器，用ruby编写而成，结合了markdown、Liquid等技术，简化了静态网站的构建过程，配合disqus等技术，可以方便的生成具有简单动态功能的网站。 


**Jekyll可以很方便的使用命令来创建文章**

创建日志，可以在配置文件_config.yml中设置URL格式

    $permalink: /:year/:month/:title.html

使用rake命令创建日志文件

    $rake post title="about this blog" //这个名字将会在url中呈现，所以尽量短些好

**创建页面**

    $rake page name="about.md"
	Creating new page: ./about.md

    创建嵌套的页面
	$rake page name="pages/about.md"
	Creating new page: ./pages/about.md

    创建路径页面
	$rake page name="pages/about"
	Creating new page: ./pages/about/index.html
	