### Cookie 

HTTP cookie 通常叫做cookie。最初是在客户端用于存储会话信息的。 该标准要求服务器对任意HTTP 请求发送Set-Cookie HTTP头作为响应的一部分。

HTTP/1.1 200 OK

Content-type: text/html

Set-Cookie: name = value

Other-header：Other-header-value



Cookie 大约4KB的长度限制。 



#### 构成

* 名称： 一个唯一确定cookie的名称。 不区分大小写。 最好区分大小写
* 值： 储存在cookie中的字符串值。必须被URL编码
* 域：cookie对于那个域有效的。 所有向该域名发送的请求中都会包含这个cookie信息。 这个值可以包含子域 。
* 路径：对于指定域中的那个路径。应该向服务器发送cookie
* 失效时间 是GMT时间可是的日期（Wdy, DD-Mon-YYYY HH:MM:SS GMT）



### Cookie 操作：读取、写入、删除

详细可见 cookies-js.

```javascript
var CookieUtil = {
  get: function(name) {
  	var cookieName = encodeURIComponent(name) + '=',
        cookieStart = document.cookie.indexOf(cookieName),
        cookieValue = null;
    
    if (cookieStart > -1) {
      var cookieEnd = document.cookie.indexOf(';', cookieStart);
      if (cookieEnd == -1) {
        cookieEnd = document.cookie.length;
      }
    }
  },
};
```





####  Web存储机制  

WebStorage 两个目的 

* 提供一种在cookie之外存储会话数据的途径

* 提供一种存储大量可以夸回话存在的数据机制

  ​

clear()： 删除所有值；Firefox 中没有实现

getItem(name)：根据指定的名字name 获取对应的值。

 key(index)：获得index 位置处的值的名字。

 removeItem(name)：删除由name 指定的名值对儿。

 setItem(name, value)：为指定的name 设置一个对应的值。



#### sessionStorage 

它存储特定于某个会话的数据，也就是该数据只是保持到浏览器关闭。 这个对象就像会话cookie 也会在浏览器关闭后消失。存储在sessionStorage 中的数据可以跨越页面刷新而存在，

存储在localStorage 中的数据和存储在globalStorage 中的数据一样，都遵循相同的规则：数据保留到通过JavaScript 删除或者是用户清除浏览器缓存





























