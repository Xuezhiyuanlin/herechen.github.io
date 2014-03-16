---
date: 2014-03-16 09:29:27
origindate: 2014-03-16 09:29:27
layout: post
title: Web 资源集锦
thread: 6
categories: 资源
tags: font web
---

## 摘要

首先，这是篇文章目的在于资源收集，并针对于 web 方面的资源。

----

## 字体 webfonts

**Brick Webfonts**  
[http://brick.im/](http://brick.im/)  
这是几款 web 字体的合集，特点在于漂亮、快速、开源，并且是在不修改的情况下渲染。使用起来也比较简单，当然，它并不是中文字体。该字体的使命如此描述：
> In the age of the Internet, we've found ourselves in yet another typographic battle. In an effort to speed up loading times, we've compressed fonts, and along the way, we've lost the majority of the quality of rendered type. 
> 
> Let's change that. The fonts served by Brick are clones of the original, converted without modification to WOFF format for high quality rendering and fast loading across all modern browsers.

<center>
![](/assets/ebgaramond.png)
</center>

## css

**纯 css 作图**  
[http://css-tricks.com/examples/ShapesOfCSS/?=derp](http://css-tricks.com/examples/ShapesOfCSS/?=derp)  

<center>
<div class="shape">
	<div id="burst-12"></div>
	<style scoped contenteditable>
		#burst-12 {
		    background: red;
		    width: 80px;
		    height: 80px;
		    position: relative;
		    text-align: center;
		}
		#burst-12:before, #burst-12:after {
		    content: "";
		    position: absolute;
		    top: 0;
		    left: 0;
		    height: 80px;
		    width: 80px;
		    background: red;
		}
		#burst-12:before {
		    -webkit-transform: rotate(30deg);
		       -moz-transform: rotate(30deg);
		        -ms-transform: rotate(30deg);
		         -o-transform: rotate(30deg);
		}
		#burst-12:after {
		    -webkit-transform: rotate(60deg);
		       -moz-transform: rotate(60deg);
		        -ms-transform: rotate(60deg);
		         -o-transform: rotate(60deg);
		}
	</style>
</div>
</center>

**分形图**  
[http://rectangleworld.com/blog/archives/tag/fractal](http://rectangleworld.com/blog/archives/tag/fractal)  
分形图的优点是可以用一些规则来作图，这样就可以是动态的，并且节省本地内存。用的基于 Canvas 画出来的，这个主页上还有一些其他的作品，倒是可以用来作网站背景。  
<center>
![](/assets/fractalline.png)
</center>
