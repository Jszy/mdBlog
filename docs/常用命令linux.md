连接远程ip 

```
ssh root@127.0.0.1
```

下载 node 到当前目录

```
mkdir download && cd download
wget https://npm.taobao.org/mirrors/node/v8.4.0/node-v8.4.0-linux-x64.tar.xz
```

解压 node 包

```
xz -d node-v8.4.0-linux-x64.tar.xz
tar -xvf node-v8.4.0-linux-x64.tar
```

解压之后进入到解压目录，运行安装

```
./bin/node
```

配置环境变量

```
vi /etc/profile
```

在文件最后一行增加配置

```
export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL

export PATH=$PATH:/root/downloads/node-v8.4.0-linux-x64/bin
```



