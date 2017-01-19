[原文地址](http://www.linuxidc.com/Linux/2014-04/100369.htm)  
window系统下，划分出磁盘空间，50G以上吧，然后在电脑-管理-磁盘管理，`格式化`并`删除卷`  
此分区用于安装linux系统及其文件，删除卷后，此分区对window系统不可见，但linux下，全盘可见
#### 准备工具[EasyBCD软件](http://easybcd.soft32.com/free-download/)和[Ubuntu的iso镜像](http://www.linuxidc.com/Linux/2014-04/100352.htm)
下面打开EasyBCD软件，可以看到现在我们的计算机只有一个启动“入口”，我们来给他加一个，第一步选择添加新条目（添加移动入口点）  
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/1.png)  
第2步选NeoGrub，第3步点安装点保存 ，接着是配置（第4步）  
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/2.png)  
然后就会出现一个menu.lst文件  
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/3.png)  
把下面的 英文 复制进去，把原来的全覆盖掉
```txt
title Install Ubuntu
root (hd0,0)
kernel (hd0,0)/vmlinuz boot=casper iso-scan/filename=/ubuntu-14.04-desktop-i386.iso ro quiet splash locale=zh_CN.UTF-8
initrd (hd0,0)/initrd.lz
```
特别注意，ubuntu-14.04-desktop-i386.iso是你的`iso的名字`  
下面把准备好的Ubuntu iso镜像文件用压缩软件或者虚拟光驱打开，找到casper文件夹，把里面的initrd.lz和vmlinuz解压到C盘，把.disk文件夹也解压到C盘，然后在把整个iso文件复制到C盘。  
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/4.png)  
`重启` 你就会看到有2个 启动菜单给你选择 我们选择 `NeoGrub 引导加载器` 这个选项。  
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/5.jpg)  
然后稍等待一段时间 就会见到我们想要安装的 Ubuntu了  
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/6.jpg)  
进入桌面后，按 `Ctrl+Alt+T` 打开终端，输入代码:
```txt
sudo umount -l /isodevice
```
这一命令取消掉对光盘所在 驱动器的挂载（注意，这里的-l是L的小写，-l 与 /isodevice 有一个空格。），否则分区界面找不到分区。  
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/7.png)  
下面就点击 安装Ubuntu 14.04开始安装，选语言不用说  
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/8.png)  
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/9.png)  
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/10.png)  
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/11.png)
