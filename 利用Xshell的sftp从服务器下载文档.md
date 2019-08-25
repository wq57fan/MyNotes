# 利用Xshell的sftp从服务器下载文档
---

#### 1、打开Xshell连接服务器后进入操作界面；

#### 2、服务器路径转到目标文件夹位置，并查看有哪些文件；

	cd 【目标文件夹】
	ls -lt

#### 3、本机创建sftp文件夹，并转到该路径下；

	lcd d:\Field\sftp

#### 4、查看本地文件夹路径和路径下的内容；

	lpwd
	lls

#### 5、下载远程服务器目录下的A.jpg、B.txt、C.rpm这些文件到本地sftp文件夹下；

	get ./A.jpg ./B.txt ./C.rpm

