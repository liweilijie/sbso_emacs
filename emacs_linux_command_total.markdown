linux有趣的命令
==========


#### 删除文件 ####

有次程序出错，导致写了很多临时文件没有及时删除，而将分区占满，且这些文件都不大，但是有几十万个文件。如果用 **rm -rf \*** 来删除，它会报错的，提示你参数太多，无法删除。这样你就麻烦了。后来想起一条命令来。

'`find /var -type f -name 'tmp*' | xargs rm -rf #`'
'`find /var -type f -name 'tmp*' -exec rm -rf {} \;`'

今天有遇到难题了，在一个服务器上由于压力过大，堆积了38G的日志文件，而这些文件不仅多且非常非常大。这下用rm来删除也比较慢的。

那么可以利用 **rsync** 来删除大批文件.

    mkdir -p /www/liwei_blank/
	rsync --delete-before -a -H -v /www/liwei_blank(新建的空目录) /www/wjpt_log(将要被清空的目录)
	# 如果报错'--delete-before:unknow option'的话试试下面这条命令。
	rsync --delete -a -H -v /www/liwei_blank /www/wjpt_log
	
上面是清空目录，如果要删除文件的话方法与目录对应的:

    touch /www/blank.txt
	rsync -a --delete-before --progress --stats /www/blank.txt /var/log/vsftpd.log
	
	

* * * * *




