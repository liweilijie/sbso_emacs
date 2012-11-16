Bugs的一生与我
==========

*Bugs每天都能遇到，关系越来越好了。这里记录一下Bug的一生与我的邂逅情况！*


### rm remove find  ###

在程序里面有时候需要定期地清理一些临时文件，这些文件可能会比较多.
有时候写程序时会利用remove的方式进行删除单个文件，还有一种方法是批量删除文件。
对于这几种删除方法做如下对比：
    
	> remove(file_path); /* 删除单个文件时用。*/
	> system("rm -rf tmp_*"); /* 当文件过多（上万级）时，会失败。提示参数太多。 */
	> system("find /var/ -type f -name 'tmp*' | xargs rm -rf #"); /* 不存在文件过多的问题，但是有些系统没有xargs命令。*/
	> system("find /var/ -type f -name 'tmp*' -exec rm -rf {} \\;"); /* 这个命令目前比较完美。 */
