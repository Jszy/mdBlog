连接远程ip 

```shell
ssh root@127.0.0.1
```

</br>

## node 安装

下载 node 到当前目录

```shell
mkdir download && cd download
wget https://npm.taobao.org/mirrors/node/v8.4.0/node-v8.4.0-linux-x64.tar.xz
```

</br>

解压 node 包

```shell
xz -d node-v8.4.0-linux-x64.tar.xz
tar -xvf node-v8.4.0-linux-x64.tar
```

</br>

解压之后进入到解压目录，运行安装

```shell
./bin/node
```

</br>

配置环境变量

```shell
vi /etc/profile
```

</br>

在文件最后一行增加配置

```shell
export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL

export PATH=$PATH:/root/downloads/node-v8.4.0-linux-x64/bin
```

</br>

配置文件生效

```shell
source /etc/profile
```

