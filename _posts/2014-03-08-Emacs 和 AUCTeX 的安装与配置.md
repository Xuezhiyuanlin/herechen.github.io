---
layout: post
title: Emacs和AUCTeX的安装与配置
---

## 说明 ##
- 系统：Windows 7
- 内容：本文只取主要部分说明，细节可从参考中查阅
- 部分内容上存在交叉
- 更多配置可查看参考

## 预备资源 ##
- Emacs：[https://www.gnu.org/software/emacs/](https://www.gnu.org/software/emacs/)
、[http://mirror.bjtu.edu.cn/gnu/emacs/](http://mirror.bjtu.edu.cn/gnu/emacs/)
- AUCTeX：
[https://www.gnu.org/s/auctex/‎](https://www.gnu.org/s/auctex/‎)

## Emacs 安装 ##
- 运行 Emacs 目录下 `bin` 目录中的 `addpm.exe`
- 在 Emacs 目录下新建 `.emacs` 配置文件
- 在 `.emacs` 文件中添加

    	(setenv "HOME" "C:/Program/emacs")
    	(add-to-list 'load-path "C:/Program/emacs/site-lisp")

## AUCTeX 安装 ##
在配置文件  `.emacs`  中添加

    (add-to-list 'load-path "C:/Program/emacs/auctex/site-lisp/site-start.d")
    (load "auctex.el" nil t t)
    (setq TeX-auto-save t)
    (setq TeX-parse-self t)
    (setq-default TeX-master nil)
    (load "preview-latex.el" nil t t)

## 检查加载是否成功 ##
在 Emacs 中新建后缀 tex 文件后，菜单栏会多出 `Latex` 和 `Preview`，这就说明加载了 `AUCTeX`

## XeLaTeX 编译配置 ##
在配置文件  `.emacs`  中添加

    (add-hook 'LaTeX-mode-hook 
      (lambda()
      (add-to-list 'TeX-command-list '("XeLaTeX" "%`xelatex%(mode)%' %t" TeX-run-TeX nil t))
      (setq TeX-command-default "XeLaTeX")
      (setq TeX-save-querynil )
      (setq TeX-show-compilation t)
    ))

## Emacs 背景色配置 ##
在配置文件  `.emacs`  中添加

    (set-background-color "black")
    (set-foreground-color "grey85")
    (set-face-foreground 'region "green")
    (set-face-background 'region "blue")

## 简单命令 ##
- `C-c C-c` 编译
- `C-c C-v` 预览 PDF

## 参考 ##
- 安装与配置： [http://blog.sina.com.cn/s/blog_4419b53f0100po34.html](http://blog.sina.com.cn/s/blog_4419b53f0100po34.html)
- 安装与配置： [http://emacser.com/auctex.htm](http://emacser.com/auctex.htm)
- 背景颜色设置： [http://blog.sina.com.cn/s/blog_63047caf01017hjg.html](http://blog.sina.com.cn/s/blog_63047caf01017hjg.html)
- XeLaTeX 编译设置： [http://evan7s.blog.163.com/blog/static/108955356201142393254184/](http://evan7s.blog.163.com/blog/static/108955356201142393254184/)
- AUCTex 文档：[www.gnu.org/s/auctex/manual/auctex.pdf](www.gnu.org/s/auctex/manual/auctex.pdf)