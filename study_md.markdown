这是我的markdown笔记信息
==========

*insert title '`C-c C-t t`'*

* 帮助信息：`C-c C-h`


* * * * *

### 锚标签(Anchors '`C-c C-a`') ###
	- C-c C-a l : [liwei's blog](http://www.liwei.tk)
	- C-c C-a w: 

* Commands: `C-c C-c`:
	- `C-c C-c m` :will run Markdown on the current buffer.
	- `C-c C-c p` : will run preview the output in another buffer
	- `C-c C-c e` : for html
	- `C-c C-c v` : to view the exported file in a browser.
	
* Images: `C-c C-i`:
	- `C-c C-i i` : inserts an images. ![image](image1.jpg)
	
* Logical style: `C-c C-s`:
	- `C-c C-s b` : blockquote > liwei
	- `C-c C-s p` : preformatted     liwei    
	- `C-c C-s c` : code `liwei`
	- `C-c C-s e` : emphasis *liwei*
	- `C-c C-s s` : strong **liwei**
	
* Headers: `C-c C-t`:
	- `C-c C-t n` : liwei # liwei #
	- `C-c C-t s` : liwei hello world.
----------

* Other elements:
	- `C-c -` : inserts a horizontal rule.
	
* * * * *

* insert code: start table
    #include <stdio.h>
    int main(int argc, char *argv[])
    {
	  printf("Hello Markdown");
	  return 0;
	  
    }


`code`


[[emacs emacs]]

