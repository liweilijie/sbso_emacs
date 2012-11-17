git常用命令
==========


每天几乎都会用到它，而从来也没有去记录过它的方法。说实话，git真的如所攒的那样好用。
----------

* * * * *

### 1.每天回家都要将远程仓库与本地的进行同步 ###

- '`git pull origin master`' : 相当于从远程获取最新版本并且merge到本地仓库中。git-pull = git-fetch + git-merge.
- '`git fetch and git merge`' : 

* * * * *

    
	git fetch origin master
	git log -p master origin/master
	git merge origin master
	

* * * * *

	
### 2.提交过程 ###

**提交文件时用到的命令：**

    #git add .
	#git commit -m 'comment any words'
	#git push origin master
	
