The first thing we need to do after we installed git.

You can view all of your settings and where they are coming from using:
```console
$ git config --list --show-origin
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
如果不用 --global , 就是默认 --local , 只针对当前库
+ --local 当前库
+ --global 当前用户
+ --system 全用户

set vscode as text edito
```console 
$ git config --global core.editor '"${FullPathToVscode}/bin/code" --wait'
```
我没试 , 但是感觉可以 , 因为一般安装 git 的时候 , 就设置好了

set default init branch (不设置默认也是 master)
```console 
$ git config --global init.defaultBranch master
```
Checking Your Settings
```console
$ git config --list --show-origin
```
or
```console
$ git config --list
```
使用 明确的 `key` 去看 git 到底使用的哪个值
```console
$ git config user.name
$ git config init.defaultBranch
$ git config core.editor
$ git config --show-origin user.name
$ git config --show-origin init.defaultBranch
$ git config --show-origin core.editor
```

get help
```console
$ git help <verb>
$ git <verb> --help # # 完整的 手册页
$ man git-<verb> # windows 也有 man 命令 , 但是没有 get-<verb> 的相关文件

$ git <verb> -h # 简短的 手册页
```

clone
```shell
$ git clone <url> [directory]
```

`git add` 是支持简单正则的

`git add` is a multipurpose command — you use it to begin tracking new files, to stage files, and to do other things like marking `merge-conflicted` files as resolved.

### Short Status
```shell
$ git status -s
$ git status --short
```
There are two columns to the output — the left-hand column indicates the status of the staging area and the right-hand column indicates the status of the working tree.

### The rules for the patterns you can put in the .gitignore file are as follows:
+ Blank lines or lines starting with # are ignored.
+ Standard glob patterns work, and will be applied recursively throughout the entire working tree.
+ You can start patterns with a forward slash (/) to avoid recursivity.
+ You can end patterns with a forward slash (/) to specify a directory.
+ You can negate a pattern by starting it with an exclamation point (!).

## git diff
To see what you’ve changed but not yet staged, type git diff with no other arguments:
```shell
$ git diff
```
If you want to see what you’ve staged that will go into your next commit, you can use:
```shell
$ git diff --staged
```
this command compares your staged changes to your last commit.

`git diff --cached` to see what you’ve staged so far (`--staged` and `--cached` are synonyms):
```shell
$ git diff --cached
```
see what difftool is available on the system.
```shell
git difftool --tool-help
```

### git rm <file>
就是 rm <file> + git add <file>  
rename 是因为 









