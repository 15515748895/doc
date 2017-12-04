
# easySwoole

EasySwoole 是一款基于Swoole Server 开发的常驻内存型PHP框架，专为API而生，摆脱传统PHP运行模式在进程唤起和文件加载上带来的性能损失。EasySwoole 高度封装了Swoole Server 而依旧维持Swoole Server 原有特性，支持同时混合监听HTTP、自定义TCP、UDP协议，让开发者以最低的学习成本和精力编写出多进程，可异步，高可用的应用服务。 

## 特性:

- 强大的 TCP/UDP Server 框架，多线程，EventLoop，事件驱动，异步，Worker进程组，Task异步任务，毫秒定时器，SSL/TLS隧道加密
- EventLoop API，让用户可以直接操作底层的事件循环，将socket，stream，管道等Linux文件加入到事件循环中。

## 优势:

- 简单易用开发效率高
- 并发百万TCP连接
- TCP/UDP/UnixSock
- 支持异步/同步/协程
- 支持多进程/多线程
- CPU亲和性/守护进程

## 关于ab基准测试:
```
系统: CentOS 7.1(未做系统内核调优)
CPU: 阿里云单核
内存: 1G
php: 5.6.30
Swoole: 1.9.21
测试代码: Index控制器中输出"hello world"
ab -c 100 -n 500000 http://127.0.0.1:9501/ 测试结果如下

Server Software:        swoole-http-server
Server Hostname:        127.0.0.1
Server Port:            9501

Document Path:          /
Document Length:        21 bytes

Concurrency Level:      100
Time taken for tests:   5.808 seconds
Complete requests:      50000
Failed requests:        0
Write errors:           0
Total transferred:      8850000 bytes
HTML transferred:       1050000 bytes
Requests per second:    8608.19 [#/sec] (mean)
Time per request:       11.617 [ms] (mean)
Time per request:       0.116 [ms] (mean, across all concurrent requests)
Transfer rate:          1487.94 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    1   0.4      1       2
Processing:     2   10   2.5     10      81
Waiting:        1   10   2.4      9      80
Total:          3   12   2.5     12      83

Percentage of the requests served within a certain time (ms)
  50%     12
  66%     12
  75%     12
  80%     12
  90%     12
  95%     13
  98%     13
  99%     13
 100%     83 (longest request)
```
## 其他

- [项目官网主页](http://www.easyswoole.com/)
- 官方QQ交流群：633921431
- [文档维护地址](https://github.com/easy-swoole/doc) 
    easySwoole采用gitbook作为文档撰写工具，若您在使用过程中，有发现文档需要纠正/补充。请直接提交在github上。

<script>
    var _hmt = _hmt || [];
    (function() {
        var hm = document.createElement("script");
        hm.src = "https://hm.baidu.com/hm.js?4c8d895ff3b25bddb6fa4185c8651cc3";
        var s = document.getElementsByTagName("script")[0];
        s.parentNode.insertBefore(hm, s);
    })();
</script>    
<script>
(function(){
    var bp = document.createElement('script');
    var curProtocol = window.location.protocol.split(':')[0];
    if (curProtocol === 'https') {
        bp.src = 'https://zz.bdstatic.com/linksubmit/push.js';        
    }
    else {
        bp.src = 'http://push.zhanzhang.baidu.com/push.js';
    }
    var s = document.getElementsByTagName("script")[0];
    s.parentNode.insertBefore(bp, s);
})();
</script>

    
    