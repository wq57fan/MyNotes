# oh-my-zsh主题与插件安装配置
---

#### 1.安装zsh

	sudo yum install zsh

#### 2.切换到zsh

	sudo chsh -s /bin/

#### 3、安装oh-my-zsh

	sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

#### 4、主题更换

打开.zshrc文件：

	vim ~/.zshrc


修改XAH_THEME的值：

	ZSH_THEME="ys"

#### 5、加入插件

	plugins=(git last-working-dir)

#### 6、更新配置文件，使得插件生效

	source ~/.zhsrc
