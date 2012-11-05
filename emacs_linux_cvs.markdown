cvs常用命令笔记
==========

公司用的cvs，命令常记不住，所以记录一下。
----------

### 1.创建一个新的仓库 ###

    mkdir -p /home/cvsroot/wj_module #创建仓库
	useradd qzt_wj #创建用户
	passwd qzt_wj
	chown -R qzt_wj:cvs wj_module #修改仓库的权限
	cvs -d /home/cvsroot/wj_module/ init #初始化仓库
	vi /etc/xinetd.d/cvspserver; server_args = -f --allow-root=/home/cvsroot/wj_module #增加远程访问权限
	/etc/rc.d/init.d/xinetd restart #重启服务

### 2.导入模块 ###

    export CVSROOT=:pserver:qzt_wj@192.168.0.5:/home/cvsroot/wj_module
	cvs login
	input the passwd
	cd beap_app_wj
	find . -type d -name 'CVS' | xargs rm -rf#
	cvs import -m "beap_app_wj init" beap_app_wj B3V4R7D4_MTB tag_20121105
	
	
### 3.checkout模块 ###

    export CVSROOT=:pserver:qzt3473@192.168.0.5:/home/cvsroot/3.4.7.3
	cvs login
	input the passwd
	cvs co beap_app_stat
	cd beap_app_stat
	cvs status -v | more
	cd ..
	rm -rf beap_app_stat
	cvs co -r B3V4R7D3 beap_app_stat
	

* * * * *

