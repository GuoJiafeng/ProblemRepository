## Git

### Git是什么?

​	Git是目前世界上最先进的分布式版本控制系统.

### 为什么需要版本控制系统?

​	保存历史版本的文件,方便协同开发

### 分布式VS集中式

​	什么是分布式版本控制系统 : git

![1541593092109](C:\Users\R\AppData\Local\Temp\1541593092109.png)

​	什么是集中式版本控制系统 : SVN  CVS

![1541592805240](C:\Users\R\AppData\Local\Temp\1541592805240.png)

分布式版本控制系统的优势

```markdown
	断网时 : SVN 无法继续进行工作
		    Git 可以正常进行文件交换,正常工作
	服务器损坏时 : SVN 原始文件+版本库丢失
				 Git 可以恢复完整的版本库
	程序员: SVN 网速影响工作效率  本机无法通过SVN进行代码备份 
		   Git 网速影响较小      本机可以进行版本控制
	Git拥有强大的分支管理
```

### Git的安装

```markdown
	打开 git-bash.exe
	输入指令  为git提供一个访问的用户名和Email
	$ git config --global user.name "Your Name"
	$ git config --global user.email "email@example.com"
```

###  Git的常用指令

```markdown
1. $ git init  创建版本库 Tips:需要在制定文件夹下
2. $ git add Rx.txt 添加文件至版本库
3. $ git commit /$ git commit -m"信息" 提交添加的文件
4. $ git status 查看版本库状态
5. $ git log 查看历史提交日志
 	$ git log --pretty=oneline
```

### Git的时光机
```markdown
1. $ git reset --hard 版本号  返回之前的版本
2. $ git relog                查看回退前版本
3. Git的工作区 暂存区 主干 head指针
4. vi add vi commit
5. git checkout             撤销工作区的修改
6. $ git reset head XXX     撤销暂存区的修改
7. rm XXX                 删除文件
8. $ git rm XXX           删除文件
```

### Git的分支

```markdown
`1. 分支是什么 如何实现
2. $ git checkout -b dev 创建分支
3. $ git checkout 分支名称 切换分支
4. $ git merge 分支名称   合并分支  tip:先切换至主分支
5. $ git branch -d 分支名称 删除分支
6. 解决分支冲突
    master add commit    git merge dev  修改冲突  git add  git commit
    dev    add commit  
```

### Git的远程仓库

> ```markdown
> 1. GitHub 注册登录
> 2. GitHub 新建仓库 tip: init初始化
> 3. 添加远程仓库  $ git remote add origin XXX  本地git添加远程仓库
> 4. 将本地master分支推向远程仓库
>   git push -u origin master
> 5. 删除原有的远程仓库地址 git remote remove origin
> 6. git clone XXXX
> 
> 码云
> 1. HTTP
> 2. SSH  免密推送	
> 3. git push   推送
> 4. git pull   接收
> 5. 解决远程仓库分支冲突
> 6. git push origin dev 推送分支
> 7. git push -d 删除远程分支
> ```

### Git与IDEA的集成

