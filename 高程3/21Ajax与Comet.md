### Ajax 与 Comet 

Ajax的核心是XMLHttpRequest对象。那么

* XMLHttpRequest是什么？

  XHR是通过MSXML库中的一个ActiveX对象实现的。因此可能会有三个版本的XHR对象。

  现代浏览器中创建 XHR对象 var xhr = createXHR();

  * XHR的用法

    使用XHR对象时 第一个要调用的方法就是 open(); 接受三个参数： 要发送的请求的类型(get post) 请求的URL和表示是否异步发送的请求布尔值。

    xhr.open('get', 'example.php', false);

    **这里调用open() 方法不会发送真正的请求 只是启动一个请求以备发送。真正的请求必须使用send()如果不需要通过请求主体发送数据则必须传入null。因为这个参数对有些浏览器来说是必须的。调用send之后请求会分派到服务器，这个请求是同步的。** 等到服务器响应之后再继续执行，收到响应之后 响应的数据自动填充XHR对象的数据。相关属性如下：

    * responseText: 作为响应主体被返回的文本。
    * responseXML：text/xml
    * status: 响应的HTTP状态码
    * statusText： HTTP的状态说明

    接收到响应后 第一步检查status属性。确定是否成功返回。 HTTP 的 200状态码作为成功的标志。 **304表示资源没有被修改 重定向。直接使用浏览器中缓存的版本。** 

    ```javascript
    var xhr = null;
    if (window.XMLHttpRequest) {
      xhr = new XMLHttpRequest(); // 生成xhr对象
    }
    xhr.open('GET', 'url', true);
    // 有一个设置表单提交时的内容类型
    xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
    xhr.send(params); // 提交请求的数据

    if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
      alert(xhr.responseText);
    } else {
      alert('request was unsuccessful: ' + xhr.status);
    }
    ```

  *  大多数我们需要发送异步请求 才能让js继续执行而不必等待响应。 检测XHR的readyState属性。 表示请求/响应过程的当前活动阶段。 一般4用的最多

  > 4：完成。已经接收到全部响应数据，而且已经可以在客户端使用了。

* HTTP头部信息 

  虽然不同浏览器实际发送的头部信息会有所不同, 但以上列出的基本上是所有浏览器都会发送的。**setRequestHeader() 方法设置自定义的请求头部信息。** 这个方法接受两个参数：头部字段
  的名称和头部字段的值。要成功发送请求头部信息，必须在调用open()方法之后且调用send()方法
  之前调用setRequestHeader()。

  ​

*  GET 请求

  查询的字符串中每个参数的名称和值都必须使用encodeURIComponent() 进行编码。才能放到URL的末尾

  ```javascript
  xhr.open('get', 'example.php?name1=value1&name2=value2', true);

  function addURLParam(url, name, value) {
    url += (url.indexOf('?') == -1 ? '?' : '&');
    url += encodeURIComponent(name) + '=' + encodeURIComponent(value);
    return url;
  }

  ```

  ​


* 跨资源共享

  通过XHR实现Ajax通信的一个主要限制。来源于跨域安全策略。 默认情况下 XHR对象只能访问与它包含页面位于同一个域中的资源。

  **CORS 跨域资源共享。定义了在必须访问跨域资源是。浏览器和服务器该如何沟通。 背后的基本思想就是使用自定义的HTTP头部让浏览器与服务器通信。从而决定请求或响应是应该成功还是失败**

  如果服务器可以接受请求： 在 Access-Control-Allow-Origin 中发出相同的源信息( 如果是公共资源可以发"*" )。

  ​

* ​

  ​

* Web Sockets API

  ```javascript
  // 创建 Web Socket 先实例化一个WebScoket 对象并传入要连接的URL 
  var scoket = new WebSocket('ws://www.example.com/server.php');

  /**
   * 必须给WebScoket构造函数传入绝对URl。不存在同源策略。是否可以与某个域中的页面通信 取决于服务器
   * (通过握手信息就可以知道请求来自何方)
   **/









  ```

  // 实例化WebSocket对象后 浏览器就会马上尝试创建连接。Web也有一个表示当前状态的 readyState 属性。

  * WebSocket.OPENING (0)：正在建立连接。

  * WebSocket.OPEN (1)：已经建立连接。

  * WebSocket.CLOSING (2)：正在关闭连接。

  * WebSocket.CLOSE (3)：已经关闭连接。

    要关闭连接之后。 可以在任何时候调用close() 方法。 socket.close(); 调用了close()之后，readyState 的值立即变为2（正在关闭），而在关闭连接后就会变成3。

* 发送和接收数据 

  Web Socket 打开之后，就可以通过连接发送和接收数据。要向服务器发送数据，使用send()方法
  并传入任意字符串;

  var socket = new WebSocket('ws://www.example.com/srerver.php') ;

  scoket.send('Hello');

  WebScoket

* ​





































