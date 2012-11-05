cc-mode 学习笔记
==========

### 1.概述 ###
cc-mode已经集成于emacs内，无需安装，只要打开相应后缀文件即可启用该模式。

[ccmode](http://www.gnu.org/software/emacs/manual/html_mono/ccmode.html)

insert anchors: *'`C-c C-a l`'*

### 2.配置cc-mode ###

'`c-basic-offset`' : 设置缩进字符数。

    (setq c-basic-offset 2)
	
**The (indentation) style** :

	(setq c-default-style '((java-mode . "java")
		(awk-mode . "awk")
		(other . "linux")))

**Making the <RET> key indent the new line** :

	(defun my-make-CR-do-indent ()
		(define-key c-mode-base-map "\C-m" 'c-context-line-break))
	(add-hook 'c-initialization-hook 'my-make-CR-do-indent)

### 3.Command ###
