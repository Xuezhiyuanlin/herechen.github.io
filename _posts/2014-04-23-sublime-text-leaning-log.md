---
date: 2014-04-23 12:43:32
creatdate: 2014-04-23 12:43:25
layout: post
title: Sublime Text Leaning Log
categories: tools
tags: sublime text
---

这是我的 Sublime Text 学习日志. 当前处于更新当中.除了开始的搜索引擎搜索学到的,最主要的学习途径是视频学习.这里推荐两个不错的视频集: Perfect Workflow in Sublime Text 和 Up and Running with Sublime Text.

##快捷键

0. 所有快捷键在 Key Bindings Default 中都有
1. Ctrl + Shift + L 选中多行，可以同时编辑这些行
2. Ctrl + D 可以继续向下同时选中下一个相同的文本进行同时编辑 
3. Ctrl + Shift + Tab 切换 Tab
4. Alt + 数字 直接切换到对应的 Tab
5. Ctrl+K  Ctrl + D来跳过不需要选中的
6. Alt + F3 直接多选
7. Ctrl + Shift + D 多次赋值同一行
8. Shift + 鼠标右键拖动，多行游标
9. Ctrl + D 选中光标所在的单词
10. Ctrl + K K 删除选中的其后行内容
11. Ctrl + K B 侧边栏显示
12. Ctrl + P 快速打开文件,输入文件名或路径名查找,这样甚至可以不用侧边栏
13. Ctrl + R 叫作 Goto Symbol, 到一个标志节或者符号处,可以用 Ctrl + P 加文件名加 @ 到某个文件的某个符号

##Command Palette

1. 通过 Command Palette 可以安装插件，执行快捷方式，快捷设置高亮等。
2. 安装插件：Ctrl + Shift + P ，选中 Install Package 回车，稍等片刻，在此 Ctrl + Shift + P 搜索插件并安装, 卸载 remove...  

##快捷输入 Snippets, 自动补齐

Snippets 通过 Ctrl + Shift + P 输入 snippet: .这个功能类似自动补齐.可以自定义内容,通过某个输入来触发需要输入.也可以通过安装包来实现.

	<snippet>
	<!-- 这里指明tab补齐的内容 -->
		<content><![CDATA[
	Hello, ${1:this} is a ${2:snippet}.
	]]></content>
		<!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
		<!-- 这里指明触发补齐的单词 -->
		<!-- <tabTrigger>hello</tabTrigger> -->
		<!-- Optional: Set a scope to limit where the snippet will trigger -->
		<!-- 这里指明使用tab补齐的后缀文件 -->
		<!-- <scope>source.python</scope> -->
	</snippet>

##Ctrl + Alt + O 打开当前文件文件夹 - Key Bindings User

	{ "keys": ["ctrl+alt+o"], "command": "open_dir", "args": {"dir": "$file_path", "file": "$file_name"} }



##字体设置 - Setting User

	// "font_face": "Ubuntu mono"
	// "font_face": "Courier New"
	"font_face": "Consolas"

##鼠标右键用 Sublime 打开文件夹 - 保存为 reg (未实践)

[为文件夹添加右键菜单直接由Sublime Text2打开](http://www.panwenbin.com/2013/11/17/%e4%b8%ba%e6%96%87%e4%bb%b6%e5%a4%b9%e6%b7%bb%e5%8a%a0%e5%8f%b3%e9%94%ae%e8%8f%9c%e5%8d%95%e7%9b%b4%e6%8e%a5%e7%94%b1sublime-text2%e6%89%93%e5%bc%80/)

	Windows Registry Editor Version 5.00
	 
	[HKEY_CLASSES_ROOT\Directory\shell\Open with SubLime Text 2]
	 
	[HKEY_CLASSES_ROOT\Directory\shell\Open with SubLime Text 2\Command]
	@="C:\\Program Files\\Sublime Text 2\\sublime_text.exe -n \"%1\""

##在当前文件路径下打开cmd

[http://stackoverflow.com/questions/12103028/sublime-text-2-open-cmd-prompt-at-current-or-project-directory-windows#12175413](http://stackoverflow.com/questions/12103028/sublime-text-2-open-cmd-prompt-at-current-or-project-directory-windows#12175413)

python 文件,另存为 cmd.py (放于 preference-browse package 路径下)

	import os, sublime_plugin
	class CmdCommand(sublime_plugin.TextCommand):
	    def run(self, edit):
	        file_name=self.view.file_name()
	        path=file_name.split("\\")
	        current_driver=path[0]
	        path.pop()
	        current_directory="\\".join(path)
	        command= "cd "+current_directory+" & "+current_driver+" & start cmd"
	        os.system(command)

添加鼠标右键菜单项,另存为 Context.sublime-menu 

	[
	     { "command": "cmd" }
	]

新建快捷键的方式 - Key Bindings User

	{ "keys": ["alt+c"], "command": "cmd"}

##在 cmd 中用 Sublime 打开文件 (未实践)

[http://stackoverflow.com/questions/9440639/sublime-text-from-command-line-win7](http://stackoverflow.com/questions/9440639/sublime-text-from-command-line-win7)

	doskey subl="C:\Program Files\Sublime Text 2\sublime_text.exe" $*

##对一串字符插入一对括号

选中字符串, Shift + ( 即可插入括号

##Emmet 插件 - 快速代码补齐

这是一个很棒的插件,用于前端开发的,前身叫 Zencode.比如输入下面的语句,并在结尾时按下 tab 键.

	html>head+body>header+.main+footer

	ul>li[list="none"]{nothing}*4

##Gist 插件 - 管理代码片段

[https://github.com/condemil/Gist#generating-access-token](https://github.com/condemil/Gist#generating-access-token) 这是一个让人 "哇哦" 的插件.

1. 安装 Gist 插件
2. 在 Github gist 账户下生成 token [https://github.com/settings/applications](https://github.com/settings/applications)
3. 复制 token,并在 Sublime Package Settings 设置 gist settings - user: `{ "token": "",}`
4. 选中代码创建 gist,不选中,则默认是当前文件.可以通过右键创建,也可以通过 Ctrl + Shift + P 查找 Gist 创建.可以不用输入参数,输入参数第一项是描述,第二项是文件名.
5. 需要查看 Gist 时,通过 Ctrl + Shift + P 搜索 open gist 即可.

##PlainTask 插件 - 任务管理

[https://github.com/aziz/PlainTasks](https://github.com/aziz/PlainTasks) 可用于创建日程管理或者任务管理.

1. 安装 PlainTask
2. Ctrl + Shift + P, 选择 Tasks: New Document 创建一个新的任务管理.
3. 插入一条任务 Ctrl + I/Ctrl + Enter, 标识完成某项任务 Ctrl + D, 任务上下移动 Ctrl + Shift + Up/Down.
4. 用 @ 来标示任务标签.
5. Ctrl + Shift + A 将已完成任务移至 Archive.
6. 输入 `---` 然后 tab 键分割.
7. 如果存在标志乱码或者显示不正常,可以到 Package Settings 设置 Plain Task 的 Settings Default.

##插件推荐

0. Package Control 插件包管理器.
1. Prefixr 对代码提前修正(css).
2. Emmet 前段开发.
3. Markdown Preview 用于预览 Markdown 显示效果.
4. Latextools 通过配置达到 Latex 编辑编译预览一体化操作.
5. Netnuts Fetch 下载文件.
6. Markdown Extended Markdown 高亮扩展.
7. AdvancedNewFile 快速新建文件,可以设定路径 Ctrl + Alt + O.
8. SidebarEnhancements 增强的侧边栏,右键后有更多选项,并且有快速预览文件的功能,比如在浏览器中预览 HTML 文件.
9. SublimeLinter 检查语法错误,Html、Ruby、Javascript、PHP等等,可以设置来禁用.
10. Gist Github gist 的本地化管理,直接上传和查看服务器上的gist
11. DocBlockr [https://github.com/spadgos/sublime-jsdocs](https://github.com/spadgos/sublime-jsdocs) 文档写作,可以便捷的写注释,比如通过识别函数的参数在写注释的时候通过 tab 更加快捷的补充注释.支持的语言有 JavaScript, PHP, ActionScript, CoffeeScript, TypeScript, Java, Groovy, Objective C, C, C++ and Rust.
12. PlainTask 任务管理

