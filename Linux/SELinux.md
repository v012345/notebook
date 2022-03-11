## 现阶段还是关了吧
如果`/etc/selinux/config`是只读的
```console
lsattr /etc/selinux/config
```
看看是不是有"i(immutable)"权限

给文件加上"i"权限
```conosle
chattr +i fileName
```
去掉"i"权限
```console
chattr -i fileName
```
