- [Git教程](#git教程)
	- [Git简介](#git简介)
	- [创建版本库](#创建版本库)
	- [把文件添加到版本库](#把文件添加到版本库)
	- [删除文件](#删除文件)
	- [添加远程库](#添加远程库)
	- [删除远程库](#删除远程库)
	- [从远程库克隆](#从远程库克隆)
	- [分支管理](#分支管理)
	- [分支策略](#分支策略)
# Git教程
## Git简介  

- **Git是目前世界上最先进的分布式版本控制系统。**    

- **版本库**：版本库又名仓库(repository)，我们可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能追踪。
## 创建版本库
1. 首先，选择一个合适的地方，创建一个空目录（不一定必须在空目录下创建Git仓库）。  

    	mkdir learngit  
		cd learngit  
		pwd  
	pwd命令用于显示当前目录。     
2. 通过git init命令把这个目录变成Git可以管理的仓库。

    	git init
如此Git就已经新建好仓库，并且提示这是一个空的仓库。可以发现目录底下多了一个.git的目录，这个目录是Git用来跟踪管理版本库的(.git目录默认隐藏，利用ls -ah命令可以看见) 。 
## 把文件添加到版本库
![](https://img-blog.csdnimg.cn/96021e64e9b244aeb50ce145db72970c.png)
- **所有版本控制系统，只能跟踪文本文件的改动（比如txt文件，网页，程序代码等等）。无法跟踪图片，视频等二进制文件的具体变化。**   
- **如果要真正使用版本控制系统，就要以纯文本方式编写文件，因为文本是有编码的（建议使用标准的UTF-8编码）。**  
- **不要使用windows自带的记事本编辑任何文本文件。最好使用Vscode代替记事本。**  

首先我们编写一个readme.txt文件饭在learngit目录下（子目录也行）。放在其他地方git找不到。

1. git add告诉Git，把文件添加到仓库。  

   		git add redeme.txt
2. git commit告诉Git，把文件提交到仓库。

    	git commit -m"wrote a readme file"

**commit可以一次提交多个文件。**  
    
	git add file1.txt
	git add file2.txt file3.txt
	git commit -m "add 3 files."  
**commit可以一次提交该文件夹下所有文件**

	git add .
	git commit -m "add all files in this folder"
修改reademe.txt文件后可以使用git status命令掌握仓库当前状态。

    git status  
后续再使用git add,git -commit提交修改。

- git diff命令可以查看具体修改内容。（查看工作区和暂存区差异）

    	git diff readme.txt
- git diff -cached（查看暂存区和分支差异）
- git diff HEAD（查看工作区和分支差异）  
- 我们可以随时用git status命令查看仓库当前状态。  
- git log命令查看每次修改的历史纪录，显示从最近到最远的提交日志。**（查看提交历史）**
- git reset命令将当前版本回退。在Git中，用HEAD表示当前版本，上一个版本就是HEAD^,上上一个版本就是HEAD^^，往上100个版本写成HEAD~100。可以直接head 版本号来更改当前版本。

    	git reset --head HEAD^
- cat命令查看redeme.txt内容。

    	cat readme.txt   
- git reflog命令用来记录你的每一次命令。**（查看命令历史）**
- git checkout -- file丢弃工作区的修改（不能丢弃暂存区的修改，想要丢弃暂存区的修改需要使用git reset或者git restore。**只适用于丢弃工作区的修改**）   
	存在两种情况：
	- redeme.txt修改后还没有被放到暂存区，这时撤销修改就回到和版本库一模一样的状态。
	- 一种是readme.txt已经添加到暂存区后，又做了修改。现在撤销修改就回到添加到暂存区后的状态。   
- git reset HEAD file既可以表示回退版本，也可以把暂存区的修改回退到工作区中。
![](https://img-blog.csdnimg.cn/6f90964ff50848b3a4344bb895220d1a.png)  
## 删除文件
一般情况下，我们通常直接在文件管理器中把没用的文件删了，或者用rm命令删了。  

    rm test.txt
此时，Git知道我们删除了文件。工作区和版本库就不一致了。现在有两个选择。  
  
- 确实从版本库中删除该文件，用命令git rm删除掉，并且git commit。

    	git rm test.txt
		git commit -m "remove test.txt"  
- 另一种情况是删除错了，因为版本库里还有，所以可以很轻松的把误删的文件恢复到最新版本。  

		git checkout -- test.txt

**从来没有被添加到版本库就被删除的文件是无法恢复的。** 
## 添加远程库
**分支不一定叫master,也可以叫别的名字，命令随之改变。**  
1. 在Github上创建learngit仓库。此时在Github上这个learngit仓库还是空的，Github告诉我们，可以从这个仓库克隆出新的仓库,也可以**把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到Github仓库。**  
在本地learngit仓库下运行命令：

    	git remote add origin git@github.com:ohmpawatt/learngit.git
添加后，远程库的名字就是origin，这是Git默认的叫法。
2. 把本地库的所有内容推送到远程库上。(实际上是把当前分支推送到远程）

    	git push -u origin master
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支推送给远程的新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后 的推送或者拉取时就可以简化命令。
3. 从现在起，只要本地作了提交，就可以通过命令把本地master分支的最新修改推送至Github。

    	git push origin master
## 删除远程库
1. 建议先使用git remote -v查看远程库信息。

    	git remote -v
2. 根据名字删除，比如删除origin。

    	git remote rm origin

**此时的删除其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登陆到Github，在后台页面找到删除按钮在删除。**
## 从远程库克隆
假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。  

1. 登录Github，创建一个新的仓库，名字叫gitskills。勾选Initialize this repository with a README，这样Github会自动为我们创建一个README.md文件。  
2. 用命令git clone克隆一个本地库。

    	git clone git@github.com:ohmpawatt/gitskills.git
3. 编辑项目。
4. git add（将改动添加到暂存区）。
5. git commit -m“提交说明”。
6. git push origin 将本地更改推送到远程分支，如果远程分支名称为main，就是：

    	git push origin main
## 分支管理
**分支作用：我们可以创建一个属于自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。**

- 每次提交，Git把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。
- master指向提交，HEAD指向当前分支。
![](https://img-blog.csdnimg.cn/db5277eeb27e4b0a8abdf6c74a2d4eb8.png)
- 当我们创建新的分支，例如dev,Git新建了一个指针叫dev,指向master相同的提交，再把HEAD指向dev,就表示当前分支在dev上。Git创建分支速度非常快，因为除了增加一个dev指针，改变HEAD指向，工作区的文件都没有任何变化。此后工作区的修改和提交就是针对dev分支。  
git checkout表创建并切换：

		git checkout -b dev
也可以用以下两条命令替代：
		
		git branch dev
		git checkout dev
使用git branch命令查看当前分支(git branch命令会列出所有分支，在当前分支前面标注*)：

		git branch
![](https://img-blog.csdnimg.cn/c4df57fec8354af1a8d488a76b2a0ca0.png)
![](https://img-blog.csdnimg.cn/ee56fae7cec8413d96e9106d94acec45.png)
- 当我们在dev上的工作完成了，就可以把dev合并到master上。最简单的方法就是直接把master指向dev的当前提交。所以Git合并分支也非常快，只要更改指针，工作区内容也不变。  
git merge命令用于合并指定分支到当前分支。
		
		gut merge dev
合并后，再查看readme.txt的内容可以看到和dev分支的最新提交是完全一样的。
![](https://img-blog.csdnimg.cn/7971867b93324b3b959529a2766f9d7d.png)
- 合并完后可以删除分支，即把dev指针给删掉。

		git branch -d dev
![](https://img-blog.csdnimg.cn/d950d07e55664ad085edcab21ad53182.png)

- **合并后再删除分支，和直接在master分支上工作效果是一样的，但过程更安全。**  
- **切换分支也可以用git switch。**  
创建并切换到新的dev分支：

		git switch -c dev
直接切换到已有的master分支：

		git switch master
## 分支策略
- master分支应该非常稳定，仅仅用来发布新版本，平时不能在上面干活。干活都在dev分支上。dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本。  
团队协作分支示意图：
![](https://img-blog.csdnimg.cn/887798a070c0403b8b17ee0d945d8152.png)


