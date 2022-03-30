# html面试

## 从浏览器输入url到请求返回发生了什么

### Url:Uniform Resource Locator，统一资源定位符，用于定位互联网上的资源，也称网址。

如有以下网址：

```
scheme: // host.domain:port / path / filename ? abc = 123 # 456789

scheme       - 定义因特网服务的类型。常见的协议有 http、https、ftp、file，
               其中最常见的类型是 http，而 https 则是进行加密的网络传输。
host         - 定义域主机（http 的默认主机是 www）
domain       - 定义因特网域名，比如 baidu.com
port         - 定义主机上的端口号（http 的默认端口号是 80）
path         - 定义服务器上的路径（如果省略，则文档必须位于网站的根目录中）。
filename     - 定义文档/资源的名称
query        - 即查询参数
fragment     - 即 # 后的hash值，一般用来定位到某个位置
```