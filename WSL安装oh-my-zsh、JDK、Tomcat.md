# WSL安装oh-my-zsh/JDK/Tomcat
---

## 一、安装zsh

### 1、更新和升级

```shell
$ sudo apt-get update
$ sudo apt-get upgrade
```

### 2、安装zsh

```shell
$ sudo apt-get install zsh
```

### 3、设置默认 shell 为 zsh

```shell
$ chsh -s $(which zsh)
```

### 4、检查是否成功

```shell
$ echo $SHELL
```

### 5、安装oh-my-zsh

```shell
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
// 或者
$ sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

### 6、上述安装方法报错怎么办？

```shell
$ git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
$ cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
$ ~ chsh -s /bin/zsh  # 切换 zsh
```

再去安装oh-my-zsh即可。

## 二、zsh主题

### 1、主题更换

打开.zshrc文件：

```shell
$ vim ~/.zshrc
```

### 2、修改XAH_THEME的值：

```shell
ZSH_THEME="ys"
```

## 三、zsh插件

### 1、下载语法高亮插件

```shell
$ git clone git://github.com/zsh-users/zsh-syntax-highlighting $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```

### 2、下载自动提示插件

下载该插件到.oh-my-zsh的插件目录

```shell
$ git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

### 3、加入自有插件

```properties
plugins=(git last-working-dir zsh-syntax-highlighting zsh-autosuggestions)
```

### 4、更新配置文件，使得插件生效

```shell
$ source ~/.zshrc
```

### 5、插件权限安全问题？

![image-20200610180915144](C:\Users\49769\AppData\Roaming\Typora\typora-user-images\image-20200610180915144.png)

```shell
$ compaudit | xargs chmod g-w,o-w
```

或者(不推荐)在该配置文件 .zshrc 中添加如下语句即可绕过权限验证：

```properties
ZSH_DISABLE_COMPFIX="true"
```

### 6、遇到"Permission denied"？

授权后再更新配置文件：

```shell
$ sudo chmod -R 777 /home
```

此时就可以在该路径下进行一系列的操作。

`注意：该授权操作不能直接对/usr进行授权，建议对子目录进行授权，不然访问权限会被锁死！`


## 四、JDK

### 1、下载并移动至目录

到 oracle 官网下载 linux-64 位压缩包，并将文件从windows目录移动到linux下：

```shell
$ sudo mv /mnt/c/Users/49769/Downloads/jdk-8u251-linux-x64.tar.gz /usr/local/jdk1.8
```

### 2、解压缩

```shell
$ sudo tar -xvzf jdk-8u251-linux-x64.tar.gz 
```

### 3、删除压缩包

```shell
$ sudo rm -f jdk-8u251-linux-x64.tar.gz
```

### 4、添加以下语句到 .zshrc，配置环境变量

 因为.zshrc控权到用户，更加安全，将JDK配置到该文件内。

进入配置文件：

```shell
$ vi ~/.zshrc
```

添加配置：

```properties
export JAVA_HOME=/usr/local/jdk1.8 
export JRE_HOME=${JAVA_HOME}/jre  
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  
export PATH=${JAVA_HOME}/bin:$PATH 
```

### 5、更新配置文件

```shell
$ source ~/.zshrc
```

### 6、测试

```shell
$ java -version
```

## 五、Tomcat

### 1、下载并移动至目录

到 tomcat 官网下载 tomcat9 的压缩包，并将文件从windows目录移动到linux下：

```shell
$ sudo mv /mnt/c/Users/49769/Downloads/apache-tomcat-9.0.36.tar.gz /usr/tomcat9
```

### 2、解压缩

若进不去bin目录，则先授权

```shell
$ sudo tar -xvzf apache-tomcat-9.0.36.tar.gz
```

### 3、删除压缩包

```shell
$ sudo rm -f apache-tomcat-9.0.36.tar.gz
```

### 4、修改端口

修改tomcat中的conf/server.xml配置文件即可。

### 5、修改配置文件

/usr/tomcat9/apache-tomcat-9.0.36/bin/`startup.sh`最后一行前加入：

/usr/tomcat9/apache-tomcat-9.0.36/bin/`shutdown.sh`最后一行前加入：

```properties
export JAVA_HOME=/usr/local/jdk1.8 
export JRE_HOME=${JAVA_HOME}/jre  
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  
export PATH=${JAVA_HOME}/bin:$PATH
export TOMCAT_HOME=/usr/tomcat9/apache-tomcat-9.0.36
```

### 5、启动

```shell
$ ./startup.sh
```

### 6、环境变量配置

注意：WSL和Windows的环境变量是共享的，导致配置的各种参数不起作用。使用`${PATH}`在wsl中查看path环境变量，默认包含win10的系统变量。

运行regedit进入注册表后，修改注册表可解决：

```properties
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Lxss{GUID}\Flags Flags从更改7为5。
```

若不管用，则管理员运行powershell重启wsl

```shell
net stop LxssManager 
net start LxssManager
```