<h1><b>MySQL部署</h1></b>

**下载MySQL 8.0的EL9仓库包：**

```
#shell
wget https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm
```

**安装仓库包：**

```
#shell
dnf install -y mysql80-community-release-el9-1.noarch.rpm
```


**安装公钥：**

```
#shell
rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023
```


**安装MySQL服务器：**

```
#shell
dnf install -y mysql-community-server
```


**启动MySQL并设置为开机自启：**

```
#shell
systemctl start mysqld
systemctl enable mysqld
```

**获取临时密码：**

```
#shell
grep 'temporary password' /var/log/mysqld.log
```


**用临时密码登录：**

```
#shell
mysql -u root -p
```


**修改密码：**

```
#mysql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'NEWpassword@123';
```


**查看数据库版本：**

```
#mysql
select version();
```

