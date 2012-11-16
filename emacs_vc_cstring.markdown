vc下CString一些方法记录
==========

*最近在搞windows，我知道无论如何都避免不了有一天做windows的开发的，于是我慢慢地接受的世界上让我最讨厌的windows。在这里记录一些windows的开发笔记吧！*


#### 1. 处理字符串的一些方法 ####

- '`CString Mid(int nFirst) const;`':
- '`CString Mid(int nFirst, int nCount) const;`': 
    * nCount代表要提取的字符数，nFirst代表要提取的开始索引位置。
	
	
==========

- '`CString Left(int nCount) const;`' : 返回的字符串是前nCount个字符。

==========

- '`CString::Find; `':
- '`int Find(TCHAR ch)const;`':
- '`int Find(LPCTSTR s) const;`':
- '`int Find(TCHAR ch, int nStart) const;`':
- '`int Find(LPCTSTR s, int nStart) cont;`' : 
  * 返回值：不匹配的话返回-1;索引以0开始。nStart代码以索引值nStart的字符开始搜索。返回此CString对象中与需要的子字符串或字符匹配的第一个字符的从零开始的索引；如果没有找到子字符串或字符则返回-1。


#### 2.数据库处理 ####

- **Access多个表join查询问题**: 
    * 在Access中如果利用join多表连接时，会出现问题，提示不支持。但是还是有办法的。办法就是加括号。例如'`select a.*, b.* from (a left join b on a.id = b.id) left join c on c.a = b.a;`' 但是当我要加多个条件且还要进行order by时，则还是叠加括号即可：'`select a.*, b.* from (a left join b on (a.id = b.id and a.id > 0)) order by a.id`'.
