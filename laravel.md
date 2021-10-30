composer dump-autoload 
php artisan config:clear
php artisan config:cache

php -d memory_limit=-1 /usr/local/bin/composer update

---------------
class counter
    {
        static $c = 0;
        return $c++;
    }
 
// Create an instance of the Reflection_Function class
    $func = new ReflectionClass('counter');
   echo    $func->getFileName();
-------------------


dd if=/dev/zero of=/root/swapfile bs=1M count=2048
mkswap /root/swapfile
swapon /root/swapfile
/root/swapfile swap swap defaults 0 0

----------------------------------

composer require "laravel/horizon" --ignore-platform-req=ext-pcntl --ignore-platform-req=ext-posix
composer install --ignore-platform-req=ext-pcntl --ignore-platform-req=ext-posix


-------------------

composer require tymon/jwt-auth
php artisan jwt:secret
安装horizon可能要
dnf install php-process

-----------
composer require "laravel/horizon" --ignore-platform-req=ext-pcntl --ignore-platform-req=ext-posix 
composer install --ignore-platform-req=ext-pcntl --ignore-platform-req=ext-posix


-----------------------
crontab -e



* * * * * php /{$pathToProject}/artisan schedule:run &>> /dev/null


------------------------------------

php artisan list

php artisan key:generate
php artisan jwt:secret
php artisan cache:clear
php artisan config:clear




