这是我的markdown笔记信息
==========

*insert title '`C-c C-t t`'*

* 帮助信息：`C-c C-h`


* * * * *

### 锚标签(Anchors '`C-c C-a`') ###
- C-c C-a l : [liwei's blog](http://www.liwei.tk) 超链接
- C-c C-a w: 

### 常用命令(Commands '`C-c C-c`') ###
- `C-c C-c m` :will run Markdown on the current buffer. m在另一个Buffer显示输出
- `C-c C-c p` : will run preview the output in another buffer。 p在浏览器中预览输出
- `C-c C-c e` : for html。e输出html文件到相同的前缀文件中。
- `C-c C-c v` : to view the exported file in a browser. v输出并且在浏览器中查看
- `C-c C-c c` : 检查是否有未定义的链接。
	
### 插入图片(Image '`C-c C-i`') ###	
- `C-c C-i i` : inserts an images. ![image](image1.jpg)

### 物理样式(Pyci Style '`C-c C-p`') ###
- `C-c C-p b` : 将选中的文字加粗 **bold** 如果未选中则插入加粗标志****
- `C-c C-p f` : 将选中的文字设置成等宽字体. `width text` <code>width text</code>
- `C-c C-p i` : 将选中的文字设置成斜体。 *italic* \*italic \*

### 逻辑样式(Logical Style '`C-c C-s`') ###
- `C-c C-s b` : blockquote > liwei. b设备引用> backquoted.
- `C-c C-s p` : preformatted     liwei. p 预格式，在之前插入4个空格默认<pre>pre text</pre>
- `C-c C-s c` : code `liwei` c插入代码块<code>code here</code>
- `C-c C-s e` : emphasis *liwei* e强调emphasis \*emphasis\*
- `C-c C-s s` : strong **liwei** s加强**strong** \*\*strong\*\*
	
### 标题章节(Headers '`C-c C-t`') ###	
- `C-c C-t n` : liwei # liwei #  ##h2## ###h3### n插入标题1-6
- `C-c C-t t` : t 插入一个title. top - level ==============
- `C-c C-t s` : liwei hello world. s插入一个section. section ---------
- `C-c -` : 插入一条分割线。

* * * * *

## 导航 ##

### 大纲导航 ###
- `TAB` : TAB折叠或者展开标题.
- `C-M-n` & `C-M-p` : 在上下可见的标题中前后移动。
- `C-M-f` & `C-M-b` : 在同一级的标题中前后移动。
- `C-M-u` : 回到上一级标题。

### wiki导航 ###
- `M-p` & `M-n` : 切换上一个或下一个wiki-link

* * * * *

