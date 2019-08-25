# oh-my-zsh主题与插件安装配置
---

#### 1.安装zsh

	sudo yum install zsh

#### 2.切换到zsh

	sudo chsh -s /bin/

#### 3、安装oh-my-zsh

	sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

##主题
#### 1、主题更换

打开.zshrc文件：

	vim ~/.zshrc


#### 2、修改XAH_THEME的值：

	ZSH_THEME="ys"

## 插件
#### 1、加入自有插件

	plugins=(git last-working-dir)

#### 2、更新配置文件，使得插件生效

	source ~/.zhsrc

#### 3、更新外部插件（比如zsh-autosuggestions）

下载该插件到.oh-my-zsh的插件目录

	git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions

之后步骤同上，加入插件后更新配置文件。
