# 快速学会使用Git

### git是什么?

Git是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。  
对于开发者的我们来说,没有必要花费太多时间去把git学透,因为可能你学会了,也用不到,我们只需要学会一些常用的指令就可以了.

### git的优势在哪里?

之前主流的管理工具就是Git和Svn,那么Git相比与Svn它的有何优势呢?  

* Git是分布式,而Svn是集中式不是分布式的,那么分布式又是什么?分布式就是好比每个人都是一个独立的系统可以独立运转,然后可以在自己的本地对项目进行有效的控制,而Svn在没有网络的情况下,在本地不能像Git一样灵活.  

* Git没有一个全局版本号，而SVN有：目前为止这是跟SVN相比Git缺少的最大的一个特征。

* (commit)提交的方式也是Git优于Svn的一个地方,Svn在没有网络的情况下是没有办法提交的,Git提交是在提交在本地仓库,而与远程仓库的交互(项目仓库)是进行"推"(Git push),也就是把本地的代码更新到项目仓库里面。

* GIT分支和SVN的分支不同：
分支在SVN中一点不特别，就是版本库中的另外的一个目录。如果你想知道是否合并了一个分支，你需要手工运行像这样的命令svn propget svn:mergeinfo，来确认代码是否被合并。   
然而，处理GIT的分支却是相当的简单和有趣。你可以从同一个工作目录下快速的在几个分支间切换。你很容易发现未被合并的分支，你能简单而快捷的合并这些文件。  
Git鼓励分Branch，而SVN，说实话，我用Branch的次数还挺少的，SVN自带的Branch merge我还真没用过，有merge时用的是Beyond Compare工具合并后再Commit的；   

* GIT的内容完整性要优于SVN：  
GIT的内容存储使用的是SHA-1哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏。
* Git下载下来后，在本地不必联网就可以看到所有的log，很方便学习，SVN却需要联网；


## 开始Git操作

### 配置用户名和邮件  
打开git bash 配置命令
  
 	git config --global user.name "您的用户名"
	
	git config --global user.email "您的邮箱"


### Git创建版本库:
	1. 找到一个放置项目的文件夹
	2. 然后右键点击鼠标Git Bash Here 在命令行里面输入git init    
版本库就创建好了
如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见。
	
	删除远程仓库: git  remote rm test

### 关联/克隆远程仓库
Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

克隆:

	1.使用git clone 加上远程仓库的地址    就可以克隆项目了
(如果出现ssl认证错误输入下面命令)  
git config --global http.sslVerify false

关联:
  
	1. 要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；

	2. 关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

	3.此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

	4.查看修改内容(工作区和仓库的区别): git diff (file)
	
	5.查看版本(参数可以简化版本信息,commit id和备注):
	git log --pretty=oneline


### 创建合并分支:

	查看分支：git branch
	
	创建分支：git branch <name>
	
	切换分支：git checkout <name>
	
	创建+切换分支：git checkout -b <name>
	
	合并某分支到当前分支：git merge <name>
	
	删除分支：git branch -d <name>

	用git log --graph命令可以看到分支合并图

	git cherry-pick  <name>   也可以用来合并分支

 	git cherry-pick <commitid>  合并某一次提交记录的代码

	建立本地分支和远程分支的关联,使用:
	git branch --set-upstream branch-name  origin/branch-name;
	
再合并分支的时候可能有的小伙伴会出现冲突的情况这个时候应该解决冲突然后 通过 git status 查看通途文件解决以后然后在添加提交就可以了  
当工作没有完成时，又有其他事情出现,这个时候可以先把工作现场git stash一下，然后去其他事情，完成后，再git stash pop，回到工作现场.      

### 推送分支 :
就是把该分支上所有本地提交到远程库中，推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：  
首先，可以试图用git push origin branch-name推送自己的修改.  
如果推送失败，则因为远程分支比你的本地更新早，需要先用git pull试图合并。  
如果合并有冲突，则需要解决冲突，并在本地提交。再用git push origin branch-name推送。 


### 多人协作:

　　当你从远程库克隆时候，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且远程库的默认名称是origin。  

	要查看远程库的信息 使用 git remote
	要查看远程库的详细信息 使用 git remote –v

### 标签

Git设置标签很简单

	命令git tag <name>用于新建一个标签，默认为HEAD，也可以指定一个commit id；

	git tag -a <tagname> -m "blablabla..."可以指定标签信息；

	git tag -s <tagname> -m "blablabla..."可以用PGP签名标签；

	命令git tag可以查看所有标签。
	
	命令git push origin <tagname>可以推送一个本地标签；
	
	命令git push origin --tags可以推送全部未推送过的本地标签；
	
	命令git tag -d <tagname>可以删除一个本地标签；
	
	命令git push origin :refs/tags/<tagname>可以删除一个远程标签。


### 项目管理

1. 版本回退  

		HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。

		穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
	
		要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

		


2. 撤销修改删除

		1.当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

		2.当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，，第二步按1操作。

		3.命令git rm用于删除一个文件。

		



Git基本常用命令如下：

　　mkdir：         XX (创建一个空目录 XX指目录名)

　　pwd：          显示当前目录的路径。

　　git init          把当前的目录变成可以管理的git仓库，生成隐藏.git文件。

　　git add XX       把xx文件添加到暂存区去。

　　git commit –m “XX”  提交文件 –m 后面的是注释。

　　git status        查看仓库状态

　　git diff  XX      查看XX文件修改了那些内容

　　git log          查看历史记录

　　git reset  --hard HEAD^ 或者 git reset  --hard HEAD~ 回退到上一个版本

　　(如果想回退到100个版本，使用git reset –hard HEAD~100 )

　　cat XX         查看XX文件内容

　　git reflog       查看历史记录的版本号id

　　git checkout -- XX  把XX文件在工作区的修改全部撤销。

　　git rm XX          删除XX文件

　　git remote add origin <仓库地址> 关联一个远程库

　　git push –u(第一次要用-u 以后不需要) origin master 把当前master分支推送到远程库

　　git clone <仓库地址>  从远程库中克隆

　　git checkout –b dev  创建dev分支 并切换到dev分支上

　　git branch  查看当前所有的分支

　　git checkout master 切换回master分支

　　git merge dev    在当前的分支上合并dev分支

　　git branch –d dev 删除dev分支

　　git branch name  创建分支

　　git stash 把当前的工作隐藏起来 等以后恢复现场后继续工作

　　git stash list 查看所有被隐藏的文件列表

　　git stash apply 恢复被隐藏的文件，但是内容不删除

　　git stash drop 删除文件

　　git stash pop 恢复文件的同时 也删除文件

　　git remote 查看远程库的信息

　　git remote –v 查看远程库的详细信息

　　git push origin master  Git会把master分支推送到远程库对应的远程分支上

　　[如有更好的建议提议,可以发到我的邮箱diosamolee2014@gmail.com](#)