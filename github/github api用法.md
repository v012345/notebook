https://api.github.com/repos/solomonxie/gists/contents

git pull <远程主机名> <远程分支名>:<本地分支名>

如何进行pr!!!!

### 清理没stage的文件和文件夹
```console
git clean -f -d
```

删除当前目录下没有被track过的文件和文件夹
```console
git clean -df
```

新建分支,并切换分支
```console
git checkout -b dev
```

### 拉一个远程分支
本地没有这个远程分支的情况
```console
git fetch origin branch-name
```
新建分支track,这个分支
```console
git checkout -b branch-name origin/branch-name
```

