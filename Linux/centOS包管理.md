虽然 centOS8 已经用了 DNF 来管理, 但是我还是会用到 centOS7, 所以把 yum 和 dnf 都记下来.

### 列出已安装的包
```console
$ dnf list installed
$ yum list installed
```


### [remi](https://blog.remirepo.net/pages/Config-en)
```console
# dnf install http://rpms.remirepo.net/enterprise/remi-release-8.rpm
# dnf module list php
```
<!-- #选择适合的版本安装
sudo dnf module reset php
sudo dnf module enable php:remi-7.4
sudo dnf module install php:remi-7.4
#配不配置没关系
dnf install php-pdo php-mysqlnd -->

### [composer](https://getcomposer.org/download/)

### [git](https://git-scm.com/download/linux)
```console


```
