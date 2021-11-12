# 使用WebHooks通知服务器拉取代码

## git
`git -C <path> pull [origin master]`

## 在对应仓库的 settings 中开启webhook
    只发送push事件给api就行,这里说一下laravel中对github签名的校验  
```php
$x_hub_signature_256 = $request->header("x-hub-signature-256");
$signature = "sha256=" . hash_hmac("sha256", $request->getContent(), "github webhook secret");
if (hash_equals($x_hub_signature_256, $signature)) {
    //通过验签
}
```
## 说明一下权限问题
`git pull` 我一直用的root权限  
所以这个比较烦了  
这个随便找个地方,看看下面输出谁,如果没改php.ini的话,应该是*apache*
```php
echo shell_exec("whoami");
```
之后运行下面的,就是在`/etc/sudoers.d/`下面生成`apache`文件,[参考](https://anto.online/code/how-to-run-php-script-root/)
```bash
sudo visudo -f /etc/sudoers.d/apache
```
在`/etc/sudoers.d/apache`中加入,下面的 `apache` 以 `echo shell_exec("whoami");` 返回的为准
```shell
apache ALL=(ALL) NOPASSWD: ALL
```
之后在 laravel 的根目录生成 `/scripts/gitpull.sh`,内容为
```shell
#!/bin/bash
sudo git -C $1 pull origin master
```
最后在`webhooks`的接口调用下面命令,来拉取`master`分支
```php
shell_exec("bash " . base_path() . "/scripts/gitpull.sh " . base_path());
```


