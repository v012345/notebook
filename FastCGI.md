## CGI
CGI (Common Gateway Interface)是 Web Server 与后台语言交互的协议，有了这个协议，开发者可以使用任何语言处理 Web Server 发来的请求，动态的生成内容。保证了传递过来的数据是标准格式的（规定了以什么样的格式传哪些数据（URL、查询字符串、POST数据、HTTP header等等）），方便了开发者。

## PHP-CGI
PHP语言对应与服务器交互的CGI程序就是PHP-CGI。  
CGI程序本身只能解析请求、返回结果，不会进程管理，所以有一个致命的缺点，那就是每处理一个请求都需要fork一个全新的进程，随着Web的兴起，高并发越来越成为常态，这样低效的方式明显不能满足需求（每一次web请求都会有启动和退出进程，也就是最为人诟病的fork-and-execute模式，这样一在大规模并发下，就死翘翘了）。就这样，FastCGI诞生了，CGI程序很快就退出了历史的舞台。

## FastCGI
FastCGI，顾名思义为更快的 CGI，它允许在一个进程内处理多个请求，而不是一个请求处理完毕就直接结束进程，性能上有了很大的提高。FastCGI也可以说是一种协议  
那么FastCGI是怎么做的呢  
首先，FastCGI会先启一个master进程，解析配置文件，初始化执行环境，然后再启动多个worker进程。当请求过来时，master会传递给一个worker，然后立即可以接受下一个请求。  
这样就避免了重复的劳动，效率自然是高。  
而且当worker不够用时，master可以根据配置预先启动几个worker等着。  
当然空闲worker太多时，也会停掉一些，这样就提高了性能，也节约了资源。这就是FastCGI的对进程的管理。


---
[参考1](https://cloud.tencent.com/developer/article/1598077)  
[参考2](https://www.jianshu.com/p/95b0d5e9f9d1)  
[参考3](https://www.jianshu.com/p/80e46a80fdbd)  