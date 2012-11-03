Install Cscope to read code
==========

*insert title by `C-c C-t t`*

source code install cscope
----------

*insert one section by `C-c C-t s`*



* * * * *

### 找到xcscope.el文件，将其放在~/.liw_emacs.d目录下 ###

*'`find / -name 'xcscope.el'`'* 

一般在`/usr/share/cscope/xcscope.el`目录下。

*'`cp /usr/share/cscope/xcscope.el ~/.liw.emacs.d/`'*

### 然后在.emacs里面增加加载命令(require 'xcscope) ###

**详细的教程请阅读'`xcscope.el`文件即可。**
## cscope-indexer -r ##

## 快捷键命令 ##

	> C-c s s : Find symbol.
	> C-c s d : Find global definition.
	> C-c s g : Find global definition(alternate binding).
	> C-c s G : Find global definitoin without prompting.
	> C-c s c : Find functions calling a function.
	> C-c s C : Find called functions(list functions called from a function)
	> C-c s t : Find text string.
	> C-c s e : find egrep pattern.
	> C-c s f : find a file.
	> C-c s i : Find files #include a file

