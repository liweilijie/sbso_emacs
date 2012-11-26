gsoap一些备忘
==========


### gsoap方式下实现mtom文件流传输 ###

步骤：

`由java首先生成wsdl文件-》然后利用wsdl工具将xxx.wsdl转为xxx.h文件，注意转化的时间加一些参数
避免有时需要一些头文件。`

`-》再手动地修改xxx.h文件，将相应的文件上传与下载的内容加入其中。`


注意事项：

如果client或者server端是用 **cpp** 写的代码，则在初始化写文件，读文件等回调接口时，此回调的定义不能定义在类里面，当你定义在类里面的成员函数时，其CPP会通过**this**指针来找其函数接口地址，而在编译时其参数会多加一个接口**this**指针在参数的第一个位置，所以其接口参数是不能与回调的接口进行匹配的.

所以如果想要进行回调，那么必须在外部申明函数，且此函数应该是静态的接口才能正常使用。也就是回调函数申请为**非类成员的静态接口即可**。下面是头文件里面定义的接口，实现也在头文件里面（类外面）来实现的dime例子：

    static void putData(struct soap*, int, char**);
	static void getData(struct soap*, int, char**);
	static void getImage(struct soap*, char*);
	static void saveData(ns__Data&, const char*);

	////////////////////////////////////////////////////////////////////////////////
	//
	//	Streaming DIME attachment content handlers
	//
	////////////////////////////////////////////////////////////////////////////////

	static void *dime_read_open(struct soap*, void*, const char*, const char*, const char*);
	static void dime_read_close(struct soap*, void*);
	static size_t dime_read(struct soap*, void*, char*, size_t);
	static void *dime_write_open(struct soap*, const char*, const char*, const char*);
	static void dime_write_close(struct soap*, void*);
	static int dime_write(struct soap*, void*, const char*, size_t);
	    

* * * * *

