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

### cscope-indexer -r ###

### 生成索引文件(cscope -Rbkq) ###

要使用cscope的强大功能，首先需要为我们的代码生成一个cscope数据库文件。
生成数据库很简单，在我们的项目根目录运行'`cscope -Rbkq`'即可。

运行完命令后会生成三个: *cscope.out*, *cscope.in.out*, *cscope.po.out*.其中cscope.out是基本的符号索引，后两个文件是使用"-q"选项生成的。可以加快cscope的索引速度。

这几个参数意义如下：

- '`-R`' : 在生成索引文件时，搜索子目录树中的代码。
- '`-b`' : 在生成索引文件时，不进行cscope的界面。
- '`-k`' : 在生成索引文件时，不搜索/usr/include目录。
- '`-q`' : 生成cscope.in.out, cscope.po.out文件，加快cscope的索引速度。
- '`-i`' : 如果保存文件列表的文件名不是cscope.files时，需要加此选项告诉cscope到哪儿去找源文件列表。可以使用“-”，表示由标准输入获得文件列表。
- '`-I dir`' : 在-I选项指出的目录中查找头文件.
- '`-u`' : 扫描所有文件，重新生成交叉索引文件.
- '`-C`': 在搜索时忽略大小写.
- '`-P path`' : 在以相对路径表示的文件前加上的path，这样，你不用切换到你数据库文件所在的目录也可以使用它了.


- Cscope只在第一次解析时扫描全部文件，以后再调用cscope，它只扫描那些改动过的文件，这大大提高了cscope生成索引的速度。 
- 在缺省情况下，cscope在生成数据库后就会进入它自己的查询界面，我们一般不用这个界面，所以使用了“-b”选项。如果你已经进入了这个界面，按CTRL-D退出。 
- Cscope在生成数据库中，在你的项目目录中未找到的头文件，会自动到/usr/include目录中查找。如果你想阻止它这样做，使用“-k”选项。
- Cscope缺省只解析C文件(.c和.h)、lex文件(.l)和yacc文件(.y)，虽然它也可以支持C++以及Java，但它在扫描目录时会跳过C++及Java后缀的文件。如果你希望cscope解析C++或Java文件，需要把这些文件的名字和路径保存在一个名为cscope.files的文件。当cscope发现在当前目录中存在cscope.files时，就会为cscope.files中列出的所有文件生成索引数据库。

* * * * *

    find . -name "*.h" -o -name "*.c" -o -name "*.cc"  -o -name "*.cpp" -o -name "*.hpp" > cscope.files
	cscope -bkq -i cscope.files

* * * * *

### 快捷键命令 ###

	> C-c s s : Find symbol.查找函数或者变量。
	> C-c s d : Find global definition.
	> C-c s g : Find global definition(alternate binding).查找函数或者变量的定义。
	> C-c s G : Find global definitoin without prompting.
	> C-c s c : Find functions calling a function.查找函数在哪里被调用了。
	> C-c s C : Find called functions(list functions called from a function). 查找该函数调用了哪些函数。
	> C-c s t : Find text string.
	> C-c s e : find egrep pattern.
	> C-c s f : find a file.
	> C-c s i : Find files #include a file
	> C-c s p : 查找到的函数上次出现的位置。
	> C-c s n : 查找到的函数下次出现的位置。

* * * * *

