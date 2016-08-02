---
layout: post
title:  "xCode7+ 下 Alcatraz插件安装"
date:   2016-08-02
desc: "xCode7+ 下 Alcatraz插件安装"
keywords: "xCode,Alcatraz"
categories: [IDE]
tags: [xCode]
icon: icon-javascript
---


Alcatraz是xCode上一款插件，通过它能够搜索其他插件进行安装。
![img1](/Resource/imgs/post_1/1.png)
下载地址: https://github.com/alcatraz/Alcatraz
通用安装/卸载方式见其官网。
xCode升级到7.3之后，发现安装不上了，原因是:

xCode插件放置在~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins/目录下，格式为.xcplugin，而xcplugin文件格式中存在一个info.plist文件，其中有一项DVTPluglnCompatibilityUUIDs。插件通过DVTPluglnCompatibilityUUIDs来指定能够运行此插件的xCode版本，因此DVTPluglnCompatibilityUUIDs存放的是xCode版本对应的UUID，xCode加载插件时，将当前的UUID与插件info.plist中的DVTPluglnCompatibilityUUIDs存放的UUID进行匹配，如果没有匹配项，说明此插件无法在该版本的xCode中运行，视为插件失效。解决办法:<br />将DVTPluglnCompatibilityUUIDs添加到Alcatraz工程的info.plist中。1.下载Alcatraz工程.<br />
![img1](/Resource/imgs/post_1/2.png)2.打开Terminal输入: defaults read /Applications/Xcode.app/Contents/Info DVTPlugInCompatibilityUUID查看本机xCode的DVTPlugInCompatibilityUUID<br />![img1](/Resource/imgs/post_1/3.png)3.打开Alcatraz工程，在工程的Info栏目下找到DVTPlugInCompatibilityUUID项，将本机的DVTPlugInCompatibilityUUID添加到集合中。<br />
![img1](/Resource/imgs/post_1/4.png)4.运行Alcatraz工程，将会弹出对话框，选择Load Bundle.<br />
![img1](/Resource/imgs/post_1/5.png)5.安装完成，重启xCode.可在xCode的menu -> Window栏目下看到Package Manager.<br />
![img1](/Resource/imgs/post_1/6.png)
<br />*安装其他插件也可依据此法.*
