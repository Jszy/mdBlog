### 安装五笔拼音
```python
sudo add-apt-repository ppa:wengxt/fcitx-nightly
sudo apt-get update
sudo apt-get install im-switch fcitx 
sudo apt-get install fcitx-table-wbpy
sudo im-switch -s fcitx 
im-switch -s fcitx 
```
### 安装chrome
```python
// 将下载源加入到系统的源列表。命令的反馈结果如图
sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/

//导入谷歌软件的公钥，用于下面步骤中对下载软件进行验证
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -

//用于对当前系统的可用更新列表进行更新
sudo apt-get update

//执行对谷歌 Chrome 浏览器（稳定版）的安装。
sudo apt-get install google-chrome-stable

//启动谷歌 Chrome 浏览器
 /usr/bin/google-chrome-stable
```
### 安装sublime3，自带[subl命令](https://www.sublimetext.com/docs/3/osx_command_line.html)
```txt
1、sublime 官网下载.deb包
2、dpkg -i /sublime.deb
   默认安装在 /opt/sublime-text下
3、查看安装包所在位置
   dpkg -L sublime-text
4、安装package control 需要修改 /opt/sublime-text权限
   chmod –R 777 /opt/sublime-text
```
### 安装nodejs
官网下载最新版，解压到指定目录位置，比如 /sofeware
```python
```
配置参数，profile文件
```
export NODE_HOME=/home/brucecham/software/node
export PATH=$PATH:$NODE_HOME/bin
export NODE_PATH=$NODE_HOME/lib/node_modules
```
在.bashrc文件中加入指定命令，使每次启动后，上面的配置文件都会生效
```txt
source /etc/profile
```
