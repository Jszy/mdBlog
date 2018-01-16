## centos 7 安装 nginx 

</br>

先创建 `yum` 的 `repository`文件：`/etc/yum.repos.d/nginx.repo`

文件内容如下：

```shell
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
```

</br>

安装 `nginx`：

```shell
yum install nginx
```

</br>

启动 `nginx`

```shell
systemctl start nginx.service
```

</br>

引入外部配置文件
```shell
vi /etc/nginx/nginx.conf

include /etc/nginx/conf.d/*.conf;
include /root/home/nginx/conf.d/*.conf;
```
