### 开打指定端口
```console
firewall-cmd --zone=public --add-port=6001/tcp --permanent
firewall-cmd --reload
```