# Git教程
# Git简介  

- **Git是目前世界上最先进的分布式版本控制系统。**    

- **版本库**：版本库又名仓库(repository)，我们可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能追踪。
# 创建版本库
1. 首先，选择一个合适的地方，创建一个空目录（不一定必须在空目录下创建Git仓库）。  

    	mkdir learngit  
		cd learngit  
		pwd  
	pwd命令用于显示当前目录。     
2. 通过git init命令把这个目录变成Git可以管理的仓库。

    	git init
如此Git就已经新建好仓库，并且提示这是一个空的仓库。可以发现目录底下多了一个.git的目录，这个目录是Git用来跟踪管理版本库的(.git目录默认隐藏，利用ls -ah命令可以看见) 。 
# 把文件添加到版本库
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
# 删除文件
一般情况下，我们通常直接在文件管理器中把没用的文件删了，或者用rm命令删了。  

    rm test.txt
此时，Git知道我们删除了文件。工作区和版本库就不一致了。现在有两个选择。  
  
- 确实从版本库中删除该文件，用命令git rm删除掉，并且git commit。

    	git rm test.txt
		git commit -m "remove test.txt"  
- 另一种情况是删除错了，因为版本库里还有，所以可以很轻松的把误删的文件恢复到最新版本。  

		git checkout -- test.txt

**从来没有被添加到版本库就被删除的文件是无法恢复的。** 
# 添加远程库
1. 在Github上创建learngit仓库。此时在Github上这个learngit仓库还是空的，Github告诉我们，可以从这个仓库克隆出新的仓库





