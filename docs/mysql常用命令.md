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
