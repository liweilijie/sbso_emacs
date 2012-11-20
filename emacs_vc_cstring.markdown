vc下CString一些方法记录
==========

*最近在搞windows，我知道无论如何都避免不了有一天做windows的开发的，于是我慢慢地接受的世界上让我最讨厌的windows。在这里记录一些windows的开发笔记吧！*

* * * * *

#### 1. 处理字符串的一些方法 ####

- '`CString Mid(int nFirst) const;`':
- '`CString Mid(int nFirst, int nCount) const;`': 
    * nCount代表要提取的字符数，nFirst代表要提取的开始索引位置。
	
- '`CString Left(int nCount) const;`' : 返回的字符串是前nCount个字符。

- '`CString::Find; `':
- '`int Find(TCHAR ch)const;`':
- '`int Find(LPCTSTR s) const;`':
- '`int Find(TCHAR ch, int nStart) const;`':
- '`int Find(LPCTSTR s, int nStart) cont;`' : 
  * 返回值：不匹配的话返回-1;索引以0开始。nStart代码以索引值nStart的字符开始搜索。返回此CString对象中与需要的子字符串或字符匹配的第一个字符的从零开始的索引；如果没有找到子字符串或字符则返回-1。

* * * * *

#### 2.数据库处理 ####

- **Access多个表join查询问题**: 
    * 在Access中如果利用join多表连接时，会出现问题，提示不支持。但是还是有办法的。办法就是加括号。例如'`select a.*, b.* from (a left join b on a.id = b.id) left join c on c.a = b.a;`' 但是当我要加多个条件且还要进行order by时，则还是叠加括号即可：'`select a.*, b.* from (a left join b on (a.id = b.id and a.id > 0)) order by a.id`'.



* * * * *

#### 3.CMarkup xml库 ####

在vc中，需要用到xml库来缓存一些信息。只是首先地写xml与读xml操作，于是挑了一个可以得到源码且很轻量的xml库来操作-CMarkup库。

在使用中遇到编码问题，因为我需要解释编码出来。

我的app环境是gb2312的，而在往服务器侧发送数据是utf-8格式的。想要将utf-8的数据以utf-8的格式存放在xml文件中这一点比较困难，我还是绕道行之，将utf-8首先转为gb2312的，然后再做存储。存储之后加载时遇到问题。后来发现无论是在写还是读都要有如下代码才可以正常工作：
    
	CMarkup xml;
	
	/* whatever read or write and must add this function to set encoding */
	xml.SetDoc("<?xml version=\"1.0\" encoding=\"GB2312\"?>\r\n");
	
	if (xml.Load(path))
	{
	    /* to do */
	}

这个问题整整花了我一天时间啊。
