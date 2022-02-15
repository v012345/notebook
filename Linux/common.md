## print Linux kernel version
```console
$ uname -r
```
## check OS name and Linux kernel version
```console
$ hostnamectl
```
## view /etc/os-release file
```console
$ cat /etc/os-release
```
## create swap by file
1. 执行
```shell
$ dd if=/dev/zero of=/root/swapfile bs=1M count=2048
$ mkswap /root/swapfile
```
2. 开启与关闭swap
```console
$ swapon /root/swapfile # 使用指定swap
$ swapoff /root/swapfile # 关闭指定swap
```
3. 开启自动开启swap,可以在`/etc/fstab`中加入
```
/root/swapfile swap swap defaults 0 0
```
4. 查看存在和swap
```console
$ free
```
