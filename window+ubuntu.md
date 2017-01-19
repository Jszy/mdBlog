[原文地址](http://www.linuxidc.com/Linux/2014-04/100369.htm)  
window系统下，划分出磁盘空间，50G以上吧，然后在电脑-管理-磁盘管理，`格式化`并`删除卷`  
此分区用于安装linux系统及其文件，删除卷后，此分区对window系统不可见，但linux下，全盘可见
#### 准备工具[EasyBCD软件](http://easybcd.soft32.com/free-download/)和[Ubuntu的iso镜像](http://www.linuxidc.com/Linux/2014-04/100352.htm)
下面打开EasyBCD软件，可以看到现在我们的计算机只有一个启动“入口”，我们来给他加一个，第一步选择添加新条目（添加移动入口点）
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/1.png)
第2步选NeoGrub，第3步点安装点保存 ，接着是配置（第4步）
![img](https://raw.githubusercontent.com/brucecham/images/master/raw/ubuntu/2.png)
