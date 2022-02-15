
## 开打指定端口
```console
firewall-cmd --zone=public --add-port=6001/tcp --permanent
firewall-cmd --reload
```
## close
```console
firewall-cmd --zone=public --remove-port=6001/tcp --permanent
firewall-cmd --reload
```
## check open port
```console
$ firewall-cmd --list-all
```



---
[参考1](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7)