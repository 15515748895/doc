## Redis协程连接池
demo中有封装好的redis连接池以及redis类，地址: <https://github.com/easy-swoole/demo/blob/3.x/App/Utility/Pool/>，复制demo中的RedisPool.php和RedisObject.php并放入App/Utility/Pool中即可使用

### 添加数据库配置
在env中添加配置信息：
```dotenv
################ REDIS CONFIG ##################

REDIS.host = 127.0.0.1
REDIS.port = 6379
REDIS.auth =
REDIS.POOL_MAX_NUM = 4
REDIS.POOL_TIME_OUT = 0.1
```
在EasySwooleEvent初始化事件initialize注册该连接池
```php
// 注册redis连接池

PoolManager::getInstance()->register(RedisPool::class, Config::getInstance()->getConf('REDIS.POOL_MAX_NUM'));
```

### 注意
连接池不是跨进程的，进程间的连接池连接数是相互独立的，默认最大值是10个；如果开了4个worker，最大连接数可以达到40个。


### 使用

通过redis连接池获取redis操作对象

```php
$redis = PoolManager::getInstance()->getPool(RedisPool::class)->getObj(Config::getInstance()->getConf('REDIS.POOL_TIME_OUT'));
$redis->set('name', 'blank');
$name = $redis->get('name');
var_dump($name);
/*
 * string(5) "blank"
 */
```
用完redis连接池对象之后记得用recycleObj回收

```php
PoolManager::getInstance()->getPool(RedisPool::class)->recycleObj($redis);
```

可通过`invoke`静态方法直接从连接池取出一个连接,直接使用,回调函数结束后自动回收:
```php
<?php
try {
    $result = RedisPool::invoke(function(RedisObject $redis) {
            $name = $redis->get('name');
            return $name;
        });
    $this->writeJson(Status::CODE_OK, $result);
} catch (\Throwable $throwable) {
    $this->writeJson(Status::CODE_BAD_REQUEST, null, $throwable->getMessage());
}
```