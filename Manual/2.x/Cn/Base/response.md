# Response对象
## 生命周期
Response对象在系统中以单例模式存在，自收到客户端HTTP请求时自动创建，直至请求结束自动销毁。Response对象完全符合[PSR7](psr-7.md)中的所有规范。

## 方法列表
### write
该方法用于向客户响应数据。
```
$response->write('hello world');
```

### redirect
该方法用于将请求重定向至指定的URL
```
$response()->redirect("/newURL/index.html");
```
### setCookie
向客户端设置一个Cookie，用法与原生的setCookie一致。

### getSwooleResponse
用于获取原始的swoole_http_response实例。
### end
结束对该次HTTP请求响应
### isEndResponse
判断该次HTTP请求是否结束响应。
## PSR-7规范Response对象中常用方法
### withStatus
向客户端发送HTTP状态码。
```
$response()->withStatus($statusCode);
```
> 注意：$statusCode必须为标准的HTTP允许状态码，具体请见Http Message中的Status对象。

### withHeader
用于向HTTP客户端发送一个header。
```
$response()->withHeader('Content-type','application/json;charset=utf-8');
```