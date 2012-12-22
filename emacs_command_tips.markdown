常用的emacs命令备忘录
==========

#### Emacs与其他程序间为什么不能拷贝、粘贴呢？ ####

在~/.emacs加入这句话: "`setq x-select-enable-clipboard t`"



#### 加载一个文件的内容到当前光标处 ####

命令："`C-x i`"


#### 缓冲区操作 ####

- '`C-x C-b`' : 列出当前缓冲区
- '`C-x k <Enter>`' : 杀掉当前缓冲区

#### 复制 ####

- '`C-a C-@ C-e M-w`' : 复制一行
- '`C-a C-@ C-e M-w`' : 复制一行,效率比起VIM来真低呀。

#### 交换位置 ####

- '`C-t`' : 交换两个字符的位置。
- '`M-t`' : 交换两个单词的位置。

#### 跳转 ####

- '`M-x goto-line RET number`' : 跳到指定行。
- ‘`M-<`’ : 缓冲区头部。
- ‘`M->`’ : 缓冲区尾部。

#### 标记 ####

- '`C-@`' : 标记开始区域。
- '`C-x h`' : 标记所有文字。
- '`C-x C-x`' : 交换光标位置和区域标记区开头。

#### 缩进块 ####

- '`C-@ M-> space space space space C-x r o`' : 将代码块进行整块缩进，方法：*选中文本块，包括文本块的下一行，将这一行到缩进的位置，按 C-x r o*

#### 禁止自动产生备份文件 ####

- '`(setq make-backup-files nil)`' : 每次写文件时产生备份文件挺烦人的，于是将其禁止了。

#### 跳转 ####

- '`C-M-n C-M-p`':在大括号之前来回跳转。

#### Buffer is read-only: #<buffer ####

最近在用emacs -nw开发代码时，常常遇到**Buffer is read-only: #<buffer** 这种提示。尤其是在利用cscope进行各种查询跳转时，让人抓狂。

后来在论坛里面发贴有人说到可以使用o,j来进行跳转。

而如果发生read-only的情况。最后利用 `C-x C-q`来进行解除只读后，再进行操作。

    27.7 Read-Only Buffers

	If a buffer is read-only, then you cannot change its contents, although you may change your view of the contents by scrolling and narrowing.

	Read-only buffers are used in two kinds of situations:

	A buffer visiting a write-protected file is normally read-only.
	Here, the purpose is to inform the user that editing the buffer with the aim of saving it in the file may be futile or undesirable. The user who wants to change the buffer text despite this can do so after clearing the read-only flag with C-x C-q.

	Modes such as Dired and Rmail make buffers read-only when altering the contents with the usual editing commands would probably be a mistake.
	The special commands of these modes bind buffer-read-only to nil (with let) or bind inhibit-read-only to t around the places where they themselves change the text.

	— Variable: buffer-read-only
	This buffer-local variable specifies whether the buffer is read-only. The buffer is read-only if this variable is non-nil.

	— Variable: inhibit-read-only
	If this variable is non-nil, then read-only buffers and, depending on the actual value, some or all read-only characters may be modified. Read-only characters in a buffer are those that have non-nil read-only properties (either text properties or overlay properties). See Special Properties, for more information about text properties. See Overlays, for more information about overlays and their properties.

	If inhibit-read-only is t, all read-only character properties have no effect. If inhibit-read-only is a list, then read-only character properties have no effect if they are members of the list (comparison is done with eq).

	— Command: toggle-read-only &optional arg
	This command toggles whether the current buffer is read-only. It is intended for interactive use; do not use it in programs (it may have side-effects, such as enabling View mode, and does not affect read-only text properties). To change the read-only state of a buffer in a program, explicitly set buffer-read-only to the proper value. To temporarily ignore a read-only state, bind inhibit-read-only.

	If arg is non-nil, it should be a raw prefix argument. toggle-read-only sets buffer-read-only to t if the numeric value of that prefix argument is positive and to nil otherwise. See Prefix Command Arguments.

	— Function: barf-if-buffer-read-only
	This function signals a buffer-read-only error if the current buffer is read-only. See Using Interactive, for another way to signal an error if the current buffer is read-only.
	    

#### C-M-k ####

有时候删除一个变量里，利用struct_variable，利用 `M-d` 只能删除struct，而不能全部删除。而利用 `C-M-k` 则可以完全删除了。

##### M-x write-region #####

在vim之中很多时候会将选中的内容另存在一个文件里面，而emacs如何实现呢？ 

`M-x write-region`

这个是由 `C-x C-w` 保存文件的方法是 `write-file`联想到的。


vim中的替换命令r如何实现？
