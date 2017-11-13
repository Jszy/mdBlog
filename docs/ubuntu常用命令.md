解压文件到指定位置

```shell
tar xvJf 下载/node-v7.4.0-linux-x64.tar.xz -C software/node2
```

<br/>

创建目录并把`压缩包里面的内容`，解压到此位置，

```shell
mkdir software/node2 && 
tar xvJf 下载/node-v7.4.0-linux-x64.tar.xz 
-C software/node2 
--strip-components 1
```

<br/>

复制文件夹里面的内容到指定的文件夹中，指定的文件夹不存在时候，自动生成

```shell
cp -r software/node2 software/node3
```

<br/>

复制指定文件夹到当前目录

```shell
cp -rf software/node2 .
-f 如果目标位置存在重名的，先删除再复制进去，也就是覆盖
```

<br/>

复制指定文件夹 `ikcamp` 的内容到另外一个文件夹 `test`，并过滤掉指定目录不复制 

```shell
rsync -avP --exclude ./ikcamp/node-modules ikcamp/ test/
```

<br/>

复制指定文件夹 `ikcamp` 的内容到另外一个文件夹 `ikcamp-copy`，并过滤掉指定目录不复制 

```shell
cd ikcamp
cp -r `ls | grep -v node_modules` ../ikcamp-copy
```
