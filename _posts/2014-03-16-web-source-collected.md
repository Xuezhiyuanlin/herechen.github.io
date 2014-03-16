---
date: 2014-03-16 23:42:31
origindate: 2014-03-16 23:42:31
layout: post
title: Web 资源集锦
thread: 6
categories: 资源
tags: font web css html javascript
---

## 摘要

首先，这是篇文章目的在于资源收集，并针对于 web 方面的资源。

----

## Brick Webfonts
 
[http://brick.im/](http://brick.im/)  
这是几款 web 字体的合集，特点在于漂亮、快速、开源，并且是在不修改的情况下渲染。使用起来也比较简单，当然，它并不是中文字体。该字体的使命如此描述：
> In the age of the Internet, we've found ourselves in yet another typographic battle. In an effort to speed up loading times, we've compressed fonts, and along the way, we've lost the majority of the quality of rendered type. 
> 
> Let's change that. The fonts served by Brick are clones of the original, converted without modification to WOFF format for high quality rendering and fast loading across all modern browsers.

<img width="100%" height="auto" src="/assets/ebgaramond.png">
<img width="100%" height="auto" src="/assets/roboto.png">

----

## 纯 css 作图
 
[http://css-tricks.com/examples/ShapesOfCSS/?=derp](http://css-tricks.com/examples/ShapesOfCSS/?=derp)  
纯 css 作图可以减少本地内存占用，或者图片加载缓慢这样的问题。以一个三角形为例，其代码如下。

    <div class="shape">
    	<div id="triangle-up"></div>
    	<style contenteditable>
    		#triangle-up {
    		width: 0;
    		height: 0;
    		border-left: 50px solid transparent;
    		border-right: 50px solid transparent;
    		border-bottom: 100px solid red;
    		}
    	</style>
    </div>

<center>
<div class="shape">
	<div id="triangle-up"></div>
	<style contenteditable>
		#triangle-up {
		width: 0;
		height: 0;
		border-left: 50px solid transparent;
		border-right: 50px solid transparent;
		border-bottom: 100px solid red;
		}
	</style>
</div>
</center>

----

## 分形图

[http://rectangleworld.com/blog/archives/tag/fractal](http://rectangleworld.com/blog/archives/tag/fractal)  
分形图的优点是可以用一些规则来作图，这样就可以是动态的，并且节省本地内存。用的基于 Canvas 画出来的，这个主页上还有一些其他的作品，倒是可以用来作网站背景。  

<img width="100%" height="auto" src="/assets/fractalline.png">
<img width="100%" height="auto" src="/assets/fracaline2.png">