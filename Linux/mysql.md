### 默认就是MariaDB

### install
我看 appstream 里还是很新的,不安装客户端,就直接安装了
```console
dnf install mysql-server
```
### boot
```console
systemctl start mysqld.service
```
### mysql_secure_installation
删除一个临时账号,设置root密码
```console
mysql_secure_installation
```
### 生成用户
root 登录
```console
mysql -u root -p
```
生成数据库 nightowl
```sql
create database nightowl;
```
创建用户 meteor , 注意给密码
```sql
CREATE USER 'meteor'@'%' IDENTIFIED BY '';
```
授权给 meteor 读写 nightowl 的权限
```sql
GRANT ALL PRIVILEGES ON nightowl.* TO 'meteor'@'%';
FLUSH PRIVILEGES;
```
修改用记密码
```sql
ALTER USER 'meteor'@'%' IDENTIFIED BY '';
FLUSH PRIVILEGES;
```





