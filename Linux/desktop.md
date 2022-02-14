第一件事就先关了SElinux，有闭心可以好好研究这个权限管理系统，现在先不管他2021-09-06
vim /etc/selinux/config
直接disable吧,或者
setenforce 0 ＃转成permissive宽容模式

==========================

把v2ray加到systemd启动服务中

vim /etc/systemd/system/v2ray.service
内容
###########
[Unit]
Description=start v2ray

[Service]
Type=simple
ExecStart=/usr/local/v2rayd/v2ray #根据实际变动

[Install]
WantedBy=multi-user.target
###########

systemctl daemon-reload
systemctl start v2ray.service
systemctl enable v2ray.service

========================

安装epel库
dnf search epel-release
dnf info epel-release
dnf install epel-release

#有时centos 7 没有dnf,可以用yum先安装epel库
yum install epel-release
yum install dnf


========================

开启powertools库
dnf config-manager --set-enabled powertools

#nux-dextop可以直接安,也可以从powertools库安
dnf install http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm
安装exfat-utils , fuse , fuse-exfat 来支援exfat文系统
dnf install exfat-utils fuse-exfat



需不需要开机挂载看情况
blkid 查UUID

vim /etc/fstab
############
UUID=9EED-E731                            /home/meteor/Documents     exfat   defaults        0 0
#############
mount -a #测试有没有问题

exfat的权限问题不太好,后来改用ntfs了
#可以支援ntfs文件系统 
dnf install ntfs-3g

UUID=9C64184164182116                     /home/meteor/Public    ntfs-3g  auto,users,permissions 0 0

mount -a #测试有没有问题

========================

如果我现在正使用桌面版，我会安装个五笔输入法
dnf install ibus-table-chinese-wubi-haifeng.noarch
安装好后，可能要reboot一下来读入配置

安装tweaks,让桌好用点
dnf install gnome-tweaks.noarch
dnf install bluecurve-cursor-theme-8.0.2-11.el7.nux.noarch

========================

#安装vscode了
#第一步拿到微软的GPG
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
#之后vscode的库
sudo vim /etc/yum.repos.d/vscode.repo
#################
[vscode]
name=Visual Studio Code
baseurl=https://packages.microsoft.com/yumrepos/vscode
enabled=1
gpgcheck=1
gpgkey=https://packages.microsoft.com/keys/microsoft.asc
##################
dnf update
dnf install code

======================================

#安装chrome
dnf install https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm

========================================

启用rime库来安装php
#[CentOS 8]    
dnf install http://rpms.remirepo.net/enterprise/remi-release-8.rpm
#先列出可用的php模块
dnf module list php
#选择适合的版本安装
sudo dnf module reset php
sudo dnf module enable php:remi-7.4
sudo dnf module install php:remi-7.4
#配不配置没关系
dnf install php-pdo php-mysqlnd



#[CentOS 7]
dnf install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
yum -y install yum-utils
#又要用yum了,不知道为什么centos7的dnf不太好用
yum-config-manager --enable remi-php74
 yum update
yum install php php-fpm

systemctl status php-fpm.service

yum install php-xml php-mysql php-mysqlnd php-mbstring 



========================

#安装composer
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"

sudo mv composer.phar /usr/local/bin/composer

========================

#从官方库安装NGINX，其实epel也可有最新版，看你想怎么安装了
vi /etc/yum.repos.d/nginx.repo
###############
[nginx-stable]
name=nginx stable repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true

[nginx-mainline]
name=nginx mainline repo
baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true
###############
dnf install nginx
#这里有个问题，就是为什么dnf module list 不显示我手动加进入去的库呢


centos7
systemctl start nginx.service


============================

#以上都完装之后，要差mysql没有安装了
dnf install mysql-server
systemctl start mysqld.service
mysql_secure_installation
dnf install mysql #好像是个客户端

#进入mysql
mysql -u root -p
create database nightowl;
CREATE USER 'meteor'@'%' IDENTIFIED BY '';
GRANT ALL PRIVILEGES ON nightowl.* TO 'meteor'@'%';
FLUSH PRIVILEGES;

ALTER USER 'meteor'@'%' IDENTIFIED BY '';
FLUSH PRIVILEGES;


#centos 7 install mysql 8
rpm -Uvh https://repo.mysql.com/mysql80-community-release-el7-3.noarch.rpm
sed -i 's/enabled=1/enabled=0/' /etc/yum.repos.d/mysql-community.repo
yum --enablerepo=mysql80-community install mysql-community-server
systemctl start mysqld.service
systemctl status mysqld.service
#不知道为什么要用下面的命令来看看临时密码
grep "A temporary password" /var/log/mysqld.log

之后就是上面的步骤了


=======================
#先开打指定port，先开80和443吧
firewall-cmd --zone=public --permanent --add-service=http
firewall-cmd --zone=public --permanent --add-service=https
firewall-cmd --zone=public --permanent --add-port 1080/tcp
firewall-cmd --reload
#firewall-cmd --list-all


#如果都配置好，注意SElinux和读写权限问题应该就可以通了

===========================================

#安装nodejs
sudo dnf module list nodejs
sudo dnf module enable nodejs:14
sudo dnf module install nodejs:14

========================

phpMyAdmin

要copy一下config.sample.inc.php

cp config.sample.inc.php config.inc.php
vim 进去,把下面的东西加上,大概在第10行左右吧
$cfg['blowfish_secret'] = 'ifiaeht4399ifaoierHFUERHTUIAHIEIJI' ; /* YOU MUST FILL IN THIS FOR COOKIE AUTH! */

之后就是数据库
create database phpmyadmin;
GRANT ALL PRIVILEGES ON phpmyadmin.* TO 'meteor'@'%';
FLUSH PRIVILEGES;
