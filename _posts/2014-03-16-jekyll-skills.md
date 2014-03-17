---
date: 2014-03-16 12:42:29
origindate: 2014-03-16 12:42:29
layout: post
title: Jekyll 博客搭建略记
thread: 5
categories: 方案
tags: jekyll 软件 
---

## 要点提要

在本地安装 Jekyll 及其配套工具，再注册 GitHub 账号，本地编辑，并将内容上传到 GitHub，用 GitHub 的服务器和域名。关于工具的安装和配置不作细致描述。

## 环境与工具

环境：Windows 7  
Ruby：[http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)  
DevKit：[http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)
git：[http://git-scm.com/downloads](http://git-scm.com/downloads)  
Jekyll：[http://jekyllrb.com/](http://jekyllrb.com/)

## GitHub

注册一个 [GitHub](https://github.com/) 账号，并新建一个 respository，用来放博客。

接下来又几个需要注意的：

- master 和 gh-pages：在 git 中用到，后者是作为项目主页。
- ssh 和 https：用后者每次提交需要输入密码，前者需要配置 ([查看](http://www.blogways.net/blog/2013/04/10/generating-ssh-keys-4-github.html))。 两者对应的 remote add 方式不同，前者为 git@github.com:XXXX/YYYY.git，后者为 https://github.com/XXXX/YYYY.git。ssh 方式时 respository 可以建为 XXXX.github.io。 

## git 指令

git init // 当前项目 git 化  
git add . // 当前目录加入 git 跟踪  
git add filename // 当前文件 filename 参加 git 跟踪  
git commit -m "XXXX" // 提交信息，交给 git 经管，提交到本地库  
git remote add origin git@github.com:XXXX/YYYY.git // 与 GitHub 上项目链接 (ssh 方式)  
git push -u origin master // 将本地库提交到 GitHub 上，另一种是 gh-pages  
git rm -rf directory // 删除库中指定文件夹 directory 所有内容  
git rm filename // 删除库中指定文件 filename 内容   
git clone git＠github.com:XXXX/YYYY.git // 将 GitHub 上的项目下载下来  

一切妥当后，常用的是：  
git add .  
git commit -m "XXXX"  
git push -u origin master  
jekyll server // 本地预览

## 中文错误

jekyll server 本地查看可能会出现 GBK 错误。更改 Ruby 目录中的文件 convertible.rb，我的路径是 C:\Program\Ruby\lib\ruby\gems\2.0.0\gems\jekyll-1.4.2\lib\jekyll。原来的是  File.read_with_options(File.join(base, name),merged_file_read_opts(opts))  
更改后  
File.read_with_options(File.join(base, name),:encoding=>"utf-8")  

由于版本不同,语句上会存在一定一些差异，未必完全一样。

## 网站分析

网站分析，目的在于了解网站的访问情况，此博客使用的是 [Google Analytics](https://www.google.com/intl/zh-CN/analytics/)。

注册后，将里面的 script 拷贝到 default.html 模板的 body 标签结束前即可。可以在本页的源码结尾处看到，每个账号自然是不一样的，不要胡乱拷贝啊....同学。

## 评论与分享

本站使用的是说多的评论，同样，注册一个 [duoshuo](http://duoshuo.com/) 账号，然后然后会有一个对应的 script。也可以用[友言](http://www.uyan.cc/)作为社交评论。至于社交分享，可以使用[加网](http://www.jiathis.com)。

## 参考

博客搭建入门：[搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)  
中文乱码：[Jekyll在Windows下面中文编码问题解决方案](http://www.cnblogs.com/aleda/articles/Jekyll-in-Windows-following-Chinese-encoding-problem-solutions.html)  

一些功能引用在网站的**关于**中的资源引用有说明。
