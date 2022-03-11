<!-- RHEL 8 Or CentOS 8 Or Rocky 8 -->

## 关闭selinux
## 查看是否有虚拟内存
```console
free
```
### 有
下一步 "查看repo"
### 没有
以后写
## 查看repo
```console
dnf repolist
```
### epel
```console
dnf install epel-release
```
### remi
```console
dnf install http://rpms.remirepo.net/enterprise/remi-release-8.rpm
```

## NodeJs
先看版本
```console
dnf module list nodejs
```
比如安装16
```console
dnf module install nodejs:16
```

## Redis



