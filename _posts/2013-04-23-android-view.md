---
layout: post
title: "android 界面开发"
description: ""
category: 
tags: []
---
{% include JB/setup %}

> 习惯了VC设计界面中快捷方便的控件拖放，使用Eclipes开发Android程序设计界面还真是有些不习惯，界面的布局必须的一行一行的按照XML文档要求去输入，心中的愤怒就油然而生。不过仔细想了下，可以开发一个这样的工具，按照Android布局的规范产生XML文件就可以了。在Google中搜索了下，就发现了Android界面开发工具DroidDraw。官方网站http://www.droiddraw.org

Android工程中包含这个一个R.java文件，这个文件到底是干什么用的呢? 其实Android自己维护这一个public final class R类主要是跟新资源文件，这个R.java无需我们自己去修改，如果你不了解千万不要去修改它，它定义的每个资源值都是唯一的，不会和系统冲突。这个文件由ADT插件自动更新，当你编辑过Res文件后保存，这个类就会自动更新。

R.java里面一般有attr、drawable、id、raw、layout、string以及xml等，根据你工程使用的资源而定。当Rjava文件丢失时，就需要重建这个，但是可能会存在一些问题，比如资源无法自动更新。

R.java这个文件是会自动生成的。但是有时候你写错xml文件的时候，R.java是不会自动生成对应的值。这个时候我们会很习惯去clean一下这个项目，这个时候会突然发现，R.java竟然不见了。

这个时候的你肯定非常的气愤，你可能会拼命在网上找答案，网上会有很多答案告诉你 右键项目--》Android Tools--> fix project properties。可能你怎么fix都不能把R.java弄出来。这个时候你就要考虑一下是不是某些xml写错了，出了问题。只要xml文件有问题，系统是绝对不会给你自动生成这个R.java文件，因为他要参照你的每张xml里的数据来生成R.java，所以自然就生成不了了。

所以当你clear项目以后，错误就变了，跟变成空包，错误也是src包中的错误，若果你遇到这样的错误，并且项目中几十个xml文件，那肯定要郁闷死了，甚至崩溃了。

不过没关系。这个时候你再clean项目 ，这时console会打印出一次错误的信息提示：

例如：[2011-08-21 18:14:19 - myweibo] F:\android_workplace\myweibo\res\layout\home_list.xml:6: error: Error: No resource found that matches the given name (at 'src' with value '@drawable/usericon').
 
你就可以根据这些提示去查找哪个xml有问题，然后修改过来。再刷新一下项目，这个时候R.java文件就会出现了。

在android开发中，我们离不开资源文件的使用，从drawable到string，再到layout，这些资源都为我们的开发提供了极大的便利，不过我们平时大部分时间接触的资源目录一般都是下面这三个。

    /res/drawable
    /res/values
    /res/layout

在android开发中，我们往往都喜欢用真机进行测试，毕竟真机与模拟器还是有很大的区别！

真机调试步骤如下：

1）下载驱动（http://download.csdn.net/source/2916281）

2）在Run Configuration或Debug Configuration中配置Target为Manual

3)  在AndroidManifest.xml中application标签中添加android:debuggable="true"

4）通过以上步骤就可进行联机运行或测试


