---
date: 2014-03-27 12:51:10
creatdate: 2014-03-27 12:51:10
layout: post
title: Kindle 笔记格式化导出（预告）
thread: 10
categories: 作品
tags: MATLAB
---

项目更新地址：[https://github.com/HereChen/KindleClippingsExport](https://github.com/HereChen/KindleClippingsExport)

Author：[HereChen](http://herechen.github.io/)  
Version：目前尚不可有效使用  
update：2014-03-27

鉴于连基本的使用功能都尚未达到，对于实现细节和算法等等，暂不做细致描述。此文仅作为预告。

###项目描述

本项目旨在提取 Kindle 笔记信息，并作分离，然后实现格式化导出。这里的格式化将针对 Markdown，但最终期望是实现笔记的提取以及按条件提取，并且可以自定义导出文本格式。

###使用描述

`clipExport = KindleClippingsExport(clipImportFile, clipExportFile)`

`clipExport`--导出数据  
`clipImportFile`--笔记原始文件，如 `'My Clippings.txt'`  
`clipExportFile`--笔记导出文件名，如 `'exportclip.txt'`

`RunKindleClippingsExport.m`--是一个导出demo  
`KindleClippingsExport.m`--为导出函数

###当前实现功能

- 四行一循环的信息分离
- 标题，作者，位置，时间可提取

###已知bug

- 标注内容部分多行情况
- 笔记及其对应内容的结合

###尚需添加功能

- 笔记类型的提取
- 按条件提取笔记
- 笔记提取和导出部分分离
- 添加参数 varargin，实现可选参数，比如，文件读取编码，导出条件


###资源

- [unkeltao-kindle-note-format](http://www.unkeltao.com/blog/2014/03/14/kindlebi-ji-zhuan-huan/)
- [kindleclippings](http://www.ruby-doc.org/gems/docs/k/kindleclippings-1.3.2/README_markdown.html)
- [Kindle-Clippings-Export](https://github.com/rydjones/Kindle-Clippings-Export)
- [klipbook](https://github.com/grassdog/klipbook)
- [kindle-clips](https://github.com/minejo/kindle-clips)
- [kindle-clippings](https://github.com/lxyu/kindle-clippings)