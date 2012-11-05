cc-mode 学习笔记
==========

### 1.概述 ###
cc-mode已经集成于emacs内，无需安装，只要打开相应后缀文件即可启用该模式。

[ccmode](http://www.gnu.org/software/emacs/manual/html_mono/ccmode.html)

insert anchors: *'`C-c C-a l`'*

### 2.配置cc-mode ###

**'`c-basic-offset`'** : 设置缩进字符数。

    (setq c-basic-offset 2)
	
**The (indentation) style** :

	(setq c-default-style '((java-mode . "java")
		(awk-mode . "awk")
		(other . "linux")))

**Making the <RET> key indent the new line** :

	(defun my-make-CR-do-indent ()
		(define-key c-mode-base-map "\C-m" 'c-context-line-break))
	(add-hook 'c-initialization-hook 'my-make-CR-do-indent)

* * * * *

### 3.Command ###

#### 3.1 格式化 ####

**`C-j(newline-and-indent)`**:
	插入一行新行且格式化此行。

**`C-M-q(c-indent-exp)`**:
	格式化一对大括号，圆括号代码。注意，光标一定要置于左括号上。
	*Indents an entire balanced brace or parenthesis expression. Note that point must be on the opening brace or parenthesis of the expression you want to indent.*

**`C-c C-q(c-indent-defun)`**:
	格式化一个函数.
	
**`C-M-\(indent-region)`**:
	indent region
	
#### 3.2 Comment Commands ####

**`C-c C-c(comment-region)`**:
	comment region
	
**`M-;(comment-dwim or indent-for-comment)`**:
	在行尾插入注释。如果是空行则直接插入一行注释。

#### 3.3 Movement Commands ####

**`C-M-a(c-beginning-of-defun)`** :
	移动到函数首.
	
**`C-M-e(c-end-of-defun)`** : 
	移动到函数尾。
	
**`M-a(c-beginning-of-statement)`**

**`M-e(c-end-of-statement)`**

**`C-c C-u(c-up-conditional)`**
	在预处理之中来回跳转.
