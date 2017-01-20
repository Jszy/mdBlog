解压文件到指定位置
```
tar xvJf 下载/node-v7.4.0-linux-x64.tar.xz -C software/node2
```
创建目录并把`压缩包里面的内容`，解压到此位置，
```
mkdir software/node2 && 
tar xvJf 下载/node-v7.4.0-linux-x64.tar.xz 
-C software/node2 
--strip-components 1
```
