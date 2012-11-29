gsoap一些备忘
==========


### gsoap方式下实现mtom文件流传输 ###

步骤：

`由java首先生成wsdl文件-》然后利用wsdl工具将xxx.wsdl转为xxx.h文件，注意转化的时间加一些参数
避免有时需要一些头文件。`

`-》再手动地修改xxx.h文件，将相应的文件上传与下载的内容加入其中。`


注意事项：

如果client或者server端是用 **cpp** 写的代码，则在初始化写文件，读文件等回调接口时，此回调的定义不能定义在类里面，当你定义在类里面的成员函数时，其CPP会通过 **this** 指针来找其函数接口地址，而在编译时其参数会多加一个接口 **this** 指针在参数的第一个位置，所以其接口参数是不能与回调的接口进行匹配的.

所以如果想要进行回调，那么必须在外部申明函数，且此函数应该是静态的接口才能正常使用。也就是回调函数申请为 **非类成员的静态接口即可** 。下面是头文件里面定义的接口，实现也在头文件里面（类外面）来实现的dime例子：

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


另外，我在写服务器程序时用了c语言，而在客户端时用的是c++的方式，这两种语言间的方法应该是这样的。

**server侧利用wsdl文件生成hotel.h文件** -> **手动添加到hotle.h文件传输的部分代码定义**

**client侧利用wsdl文件生成hotel.h文件** -> **手动将server侧的hotel.h文件里面文件传输的代码部分原样地复制过来即可。**



* * * * *

### gsoap文件传输异常 ###

在利用gsoap进行文件传输时，发现有不少的bug,其实这些bug并不是它官方给的库有问题，而是咱们在使用的时候不当会导致一些无法预知的bug。

这里引用一个下载文件的例子。在下载文件时，如果文件不存在在服务器上，或者在服务器侧fopen一个文件时出错了，就会导致gsoap库里面引用时指针异常退出。在一个空指针里面去fread肯定会出错了。

还有一个问题，当客户端向服务器下载文件时，我不知道设备的ID号等信息，所以我想利用一个平台不存在的文件，让设备来请求，靠这种方式得到其设备的ID号。在平台上形成记录的作用。

先看看我修改后的代码吧：


    int m__GetData(struct soap *soap, struct x__Keys *keys, struct m__GetDataResponse *response)
	{ 
		struct m__GetDataResponse *t = NULL;

	    char files[10][256];
	    memset(files, '\0', sizeof(files));

    	int i, k;
        char *file = (char *)soap_malloc(soap, 256);
	    memset(file, '\0', 256);
        if ((soap->omode & SOAP_IO) == SOAP_IO_STORE)
          soap->omode = (soap->omode & ~SOAP_IO) | SOAP_IO_BUFFER;
        if (!keys)
			return soap_sender_fault(soap, "No keys", NULL);

	    for (i = 0, k = 0; i < keys->__size; ++i)
        { 
			if ((strstr(keys->key[i], "ly_codec_dictionary.inf")))
			{
				memset(file, '\0', 256);
				snprintf(file, 256, "/www/ly_codec_dictionary.inf");
				
				if (!access(file, F_OK))
				{
					memcpy(files[k], file, strlen(file));
					k++;
				}
			}
			else
				write_app_log("[%s] keys->key[%d] = %s. drop it. maybe this is message from client.", __func__, i, keys->key[i]);
		}

	/* Set up array of attachments to return */
	response->x__data.__size = k;
	response->x__data.item = (struct x__Data *)soap_malloc(soap, k*sizeof(struct x__Data));

	for (i = 0; i < k; i++)
		open_data(soap, files[i], &response->x__data.item[i]);

	return SOAP_OK;
	}

    
