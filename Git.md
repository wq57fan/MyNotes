**Git 常用指令**
---

代码 | 内容
-|-
git init | 初始化一个空的git本地仓库
git status | 查看工作区代码相对于暂存区的差别
git diff 文件名 | 就是查看文件不同
git clone URL | 就是克隆远程仓库到本地
git pull | 将远程仓库代码拉取到本地并合并（当前分支自动与唯一一个追踪分支进行合并）

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

