**Git 常用指令**
---

代码 | 内容
-|-
git init | 初始化一个空的git本地仓库
git status | 查看工作区代码相对于暂存区的差别
git diff 文件名 | 就是查看文件不同
git clone URL | 就是克隆远程仓库到本地
git pull | 将远程仓库代码拉取到本地并合并（当前分支自动与唯一一个追踪分支进行合并）
git log | 显示从最近到最远的提交日志
git reflog | 看命令历史，以便确定要回到未来的哪个版本
git reset --hard HEAD^ | 回退到上一个版本（HEAD指向的版本就是当前版本）
git rm test.txt | 在本地把test.txt文件删了
git remote add origin https://github.com/wq57fan/库名字.git | 在本地关联远程库，远程库的名字是origin（Git默认的）


常用步骤
---
一、把一个已有的本地仓库与远程Github仓库关联：
	
	$ git remote add origin git@github.com:USERNAME/FILENAME.git

二、本地代码修改完后：

	首先将当前目录下修改的所有代码从工作区添加到暂存区：
    $ git add .
	其次“注释”将缓存区内容添加到本地仓库：
    $ git commit -m "COMMENTS"
 

三、可以把本地库的所有内容推送到远程库上: 

	$ git push -u origin master

四、若登陆失败，无法push：

	$ git config --system --unset credential.helper

则执行这个命令之后，你可以重新写入账号密码，这样就可以重新提交代码了。


Github仓库改名后本地同步步骤
---
一、本地仓库路径下执行以下代码，列出每个远程库的简短名字：

	$ git remote -v

二、在本地仓库删除远程仓库：

	$ git remove rm origin

三、修改Github仓库名称和本地路径名称，同时本地文件夹的名称也改一下；

四、在本地添加新的远程仓库，在本地的仓库路径下键入：
		
	$ git remote add origin git@github.com:USERNAME/FILENAME.git


撤销修改
---
场景一：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file

	$ git checkout -- readme.txt	
	把readme.txt文件在工作区的修改全部撤销，让这个文件回到最近一次git commit或git add时的状态

场景二：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。

	$ git reset HEAD readme.txt		
	可以把暂存区的修改撤销掉（unstage），重新放回工作区（用于已add但没commit前，git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区）。
	若要继续删记住再用$ git checkout -- readme.txt丢弃工作区的修改

场景三：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退


创建与合并分支
---
查看分支:

	$ git branch			 列出所有分支，并查看当前分支

创建分支：

	$ git branch <name>
	
切换分支：

	$ git checkout <name>

上面创建、切换的两句可以合并为：
	
	$ git checkout -b dev	创建dev分支，然后切换到dev分支
	
提交作业后切换回主分支再合并：

	$ git checkout master		  切换回master分支
	$ git merge dev				把dev分支的工作成果合并到master分支上
	$ git branch -d dev			删除dev分支


发生冲突
---
当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，完成合并。
用git log --graph命令可以看到分支合并图：

	$ git log --graph --pretty=oneline --abbrev-commit		查看分支的合并情况