当引入新包时，有配置项更新
```shell
$ composer dump-autoload 
$ php artisan config:clear
$ php artisan config:cache
```

---

下面的命令现在没用上，之前是内存不足，用文件开了一个swap页搞定的
```shell
$ php -d memory_limit=-1 /usr/local/bin/composer update
```
---

以下用PHP的反射功能拿到类名
```php
class counter
    {
        static $c = 0;
        return $c++;
    }
 
// Create an instance of the Reflection_Function class
    $func = new ReflectionClass('counter');
    echo $func->getFileName();
```
---

下面是用文件做的swap的命令
```shell
$ dd if=/dev/zero of=/root/swapfile bs=1M count=2048
$ mkswap /root/swapfile
$ swapon /root/swapfile
```
把下面的语句加到挂载文件中，文件忘了，用的时候搜一下吧  
`/root/swapfile swap swap defaults 0 0`

---

以下是在Windows上安装horizon时，忽略相关 PHP 扩展，虽然在Windows上用不了吧
```shell
$ composer require "laravel/horizon" --ignore-platform-req=ext-pcntl --ignore-platform-req=ext-posix
$ composer install --ignore-platform-req=ext-pcntl --ignore-platform-req=ext-posix
```

---

之前搞token时用到的，不太会用
```shell
$ composer require tymon/jwt-auth
$ php artisan jwt:secret
//安装horizon可能要
$ dnf install php-process
```

```shell
$ php artisan list
$ php artisan key:generate
$ php artisan jwt:secret
$ php artisan cache:clear
```

---

laravel 定时任务
```shell
$ crontab -e
```
把下面的指令加到的排程表里
`* * * * * php /{$pathToProject}/artisan schedule:run &>> /dev/null`

---





