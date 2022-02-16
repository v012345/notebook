### install
1. [add repo](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/)
2. `dnf module enable nginx:mainline`
3. `dnf install nginx`

### version
```
$ nginx -v
```
### other
```
$ nginx -s stop
$ nginx -s reload
```

### 配置文件
+ 全局块
    > 从配置文件开始events块之间的内容,主要会设置一些影响nginx服务器整体运行的配置指令,主要包括配置运行nginx服务器的用户(组),允许生成的worker process 数,进程PID存放路径,日志存放路径和类型以及配置文件的引入等.  
    > 比如`worker_processes 1;`,这是ngnix服务器并发处理服务的关键配置,worker_processes值越大,可以支持的并发处理量也越多,但是会受到硬件,软件等设备的制约.
+ events块
    > events块涉及的指令主要影响nginx服务器与用户的网络连接,常用的设置包括是否开启对多 work process 下的网络连接进行序列化,是否允许同时接收多个网络连接,选取哪种事件驱动模型来处理连接请求,每个work process可以同时支持的最大连接数等.  
    > 上述例子就表示每个work process支持的最大连接数为1024  
    > 这部分的配置对nginx的性能影响较大,在实际中应该灵活配置.
+ http块
    > 这算是nginx服务器配置中最频繁的部分,代理,缓存和日志定义等绝大多数功能和第三方模块的配置都在这里.  
    > 需要注意的是:http块也可以包括http全局块,server块
    + http全局块
        > http全局块配置的指令包括文件引入,MIME-TYPE定义,日志自定义,连接超时时间,单链接请求数上限等.
    - server块
        > 这块和虚拟主机有密切,虚拟主机从用户角度看,和一台独立的硬件主机是完全一样的,该技术的产生是为了节省互联网服务器硬件成本.  
        > 每个http块可以包括多个server块,而每个server块就相当于一个虚拟主机.  
        > 而每个server块也分为全局server块,以及可以同时包含多个location块.
        1. 全局server块
            > 最常见的配置是本虚拟机主机的监听配置和本虚拟调机的名称或IP配置.
        2. location块
            > 一个server块可以配置多个location块.  
            > 这块的主要作用是基于nginx服务器接收到的请求字符串(例如server_name/uri-string),对虚拟主机名称(也可以是IP别名)之后的字符串(例如前面的/uri-string)进行匹配,对特定的请求进行处理.地址定向,数据缓存和应答控制等功能,还有许多第三方模块的配置也在这里进行.

## 反向代理
就是代理转发了`proxy_pass http://api.nightowl.name;`

## location
```nginx
location [ = | ~ | ~* | ^~ ] uri {

}
```
1. `=` : 用于不含正则表达式的uri前,要求请求字符串与uri严格匹配,如果成功,就停止继续向下搜索并立即处理该请求.
2. `~` : 用于表示uri包含正则表达式,并且区分大小写.
3. `~*` : 表示uri包含正则表达式,但不区分大小写.
4. `^~` : 用于不含正则表达式的uri前,要求nginx服务器找到标识uri和请求字符串匹配度最高的location后,立即使用此location处理请求,而不再使用location块中的正则uri和请求字符串做匹配.




