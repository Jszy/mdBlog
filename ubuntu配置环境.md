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
