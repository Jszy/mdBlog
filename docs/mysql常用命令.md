## 安装 mysql 

</br>

下载 `Yum Repository`，获取 `mysql` [下载地址](https://dev.mysql.com/downloads/repo/yum/)

```shell
wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
```

</br>

安装 `Yum Repository`

```shell
yum localinstall mysql57-community-release-el7-11.noarch.rpm
```

</br>

安装 `mysql`

```shell
yum install mysql-community-server
```

</br>

验证数据库：启动

```shell
systemctl start  mysqld.service
```

</br>

查看生成的临时账号root和密码

```shell
grep 'temporary password' /var/log/mysqld.log
```

</br>

完成安全设置及密码重置

```shell
mysql_secure_installation
```

</br>

## 常用命令

</br>

查看端口号

```shell
mysql> show global variables like 'port'
```

</br>

创建数据库 

```mysql
create database tutorial
```

<br/> 

创建用户和密码 

```mysql
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
``` 

<br/>

为用户分配权限 

```mysql 
GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
``` 

<br> 

权限生效 

```mysql
FLUSH PRIVILEGES;
```

<br/>

重启服务器 

```mysql
systemctl restart mysqld.service
``` 

<br/> 

更新数据库密码 

```mysql
// 版本 5.7 字段不再是password 变更为 authentication_string
update mysql.user set authentication_string=password('123456') where user='root'
```
