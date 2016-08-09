# 设置默认shell
1. 查看当前shell`echo $SHELL`
2. 安装zsh`sudo apt-get install zsh`[zsh的优势](http://www.zhihu.com/question/21418449)
2. 设置默认shell`chsh -s /bin/zsh`
3. 安装oh-my-zsh`sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`

# 切换用户
1. `sudo xxx`(可以设置/etc/sudoers对应允许命令)
2. `su -` 或者 `su xxx`

# 给root设置密码
1. `sudo passwd root`


# 源安装软件
1. 根据[软件仓库](https://help.ubuntu.com/community/Repositories/CommandLine)
2. 软件源位置 ` /etc/apt/sources.list`和`/etc/apt/sources.list.d/`目录下后缀为`.list`的文件
3. 修改源文件先备份`cp xxx xxx-backup`
4. `deb: `这行代表编译好的二进制文件，适合大部分用户
5. `deb-src:`这行代表源文件地址，适合开发者，`saucy`:发布名称，`main & restricted`:名称或组件
6. 添加源`sudo add-apt-repository "deb http://us.archixxxx`

# ppa安装软件
1. ppa(Personal Package Archive),一个软件包发散渠道[网址](https://launchpad.net/)
2. 设置ppa方式[链接](http://blog.csdn.net/david_xtd/article/details/9713643)
3. 添加ppa，`sudo add-apt-repository ppa:<repository-name>`
4. 移除ppa，`sudo add-apt-repository -r ppa:<repository-name>`

# 20件安装ubuntu要做的事
1. 根据[链接](http://blog.csdn.net/skykingf/article/details/45267517)
2. 卸载libreoffice`sudo apt-get remove libreoffice-common`
3. 删除amazon链接`sudo apt-get remove unity-webapps-common`
4. 删除基本不用自带软件
	```
	sudo apt-get remove thunderbird totem rhythmbox empathy brasero simple-scan gnome-mahjongg aisleriot gnome-mines cheese transmission-common gnome-orca webbrowser-app gnome-sudoku  landscape-client-ui-install
	sudo apt-get remove onboard deja-dup
	```
5. 安装vim`sudo apt-get install vim`
6. 安装sublime
	```
	sudo add-apt-repository ppa:webupd8team/sublime-text-3
	sudo apt-get update
	sudo apt-get install sublime-text
	```
7. 安装git`sudo apt-get install git`

# 安装chrome
1. 根据[链接](http://www.cnblogs.com/iamhenanese/p/5514129.html)
2. 添加source list`sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/`
3. 添加公钥`wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -`
4. 更新source列表 `sudo apt-get update`
5. 安装chrome`sudo apt-get install google-chrome-stable`

# 提示系统更新
1. 提示系统跟新，提示又点不了
2. 根据[链接](http://jingyan.baidu.com/article/a17d5285113afc8098c8f2e3.html?qq-pf-to=pcqq.group)
3. 运行`sudo update-manager`
4. 后来发下这东西就是`设置-软件和更新-更新`

# 卸载firefox
1. 根据[链接](http://blog.sina.com.cn/s/blog_49f914ab0100hfss.html)
2. 根据[彻底删除软件](http://zhidao.baidu.com/link?url=QKtU1H8mwCioXZLRHPGJuzk4SCeatzDY7MxfB7keT-P_NGtyWM7N-hiqqIPvYcXmiv45IKDfPxeRpUhAdS6oYK)
	>sudo apt-get purge
	>sudo apt-get autoremove,sudo apt-get clean
	>dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
	>sudo apt-get remove --purge softname1
3. 选出firefox程序`dpkg --get-selections |grep firefox`
4. 依次卸载`sudo apt-get purge firefox...`
5. 删除配置文件`rm -rvf ~/.mozilla`

# 安装shadowsocks
1. 根据[链接](https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97)
2. 运行
	```
	sudo add-apt-repository ppa:hzwhuang/ss-qt5
	sudo apt-get update
	sudo apt-get install shadowsocks-t5
	```

# 安装nvida驱动
1. 因为是双显卡，所以想安装闭源驱动用来切换显卡
2. 去官网搜了文件，xxx.run
3. 在tty环境下运行(tty环境，Teletype，控制终端，ubuntu下ctrl+alt+F1...F7控制)
4. 按照[链接](http://ubuntuhandbook.org/index.php/2015/01/install-nvidia-346-35-ubuntu-1404/)安装
5. 卸载nvidia驱动`sudo apt-get remove nvidia* && sudo apt-get autoremove`
6. 黑名单开源显卡驱动
	```
	gedit /etc/modprobe.d/blacklist-nouveau.conf
	添加如下
	blacklist nouveau
	blacklist lbm-nouveau
	options nouveau modeset=0
	alias nouveau off
	alias lbm-nouveau off
	```
7. 关闭开源驱动
	```
	echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/nouveau-kms.conf
	sudo update-initramfs -u
	```
8. 关闭图形会话，`sudo stop lightdm`，失败，使用`service lightdm stop`，成功
9. 运行`chmod +x NVIDIA-Linux-*-346.35.run && sudo sh NVIDIA-Linux-*-346.35.run`，成功
10. 重启,失败

# 循环登陆界面，登陆不了
1. 查看 ~/.Xauthority权限，正确，还是运行`chown lee:lee .Xauthority`,登陆失败
2. 运行`chmod 777 /tmp -R`,登陆失败
3. 卸载nvidia驱动
4. 运行
	```
	sudo sh NVIDIA-Linux-*-346.35.run --uninstall
	sudo apt-get purge nvidia*
	```
5. 登陆成功

# 重装nvidia驱动
1. 按照[链接](https://www.v2ex.com/t/275534)
2. 运行
	```
	sudo apt-add-repository ppa:graphics-drivers/ppa -y
	sudo apt update
	sudo apt install nvidia-364
	```
3. 成功
4. alt+f2,查找nvidia-settings，Thermal Settings下查看显卡温度，在PRIME Profiles下进行显卡切换

# 安装搜狗输入法
1. 了解到搜狗输入法基于fcitx输入框架
2. 卸载fcitx框架，其他多余输入法
3. 添加ppa`ppa:fcitx-team/nightly`，更新失败
4. 下载deb包，`dpkg install sougouxx.deb`，失败
5. 依赖问题，下载gdebi，解决依赖问题`apt-get install gdebi`
6. 安装deb包，`sudo gdebi sogoupinyin.deb`
7. 完成

# 登陆启动会话失败
1. 卸载ibus原因
2. 安装ubuntu-session
3. 重启，成功登陆

# 显示不了侧边栏
1. 卸载ibus引起，unity也被卸载掉了
2. 安装unity`apt-get install unity`
3. 重设compiz`dconf reset -f /org/compiz/`
4. 重启unity`setsid unity`
5. 如果想重置侧边栏图标，`unity --reset-icons`

# 系统设置显示不全
1. 因为之前卸载ibus，会把unity-control-center也卸载掉
2. 重新安装即可
