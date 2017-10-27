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
