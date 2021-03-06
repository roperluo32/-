- HTTP和HTTPS的区别
  - TCP后增加了SSL四次握手过程

- SSL的过程
  - client-hello, 请求证书
  - server回复证书和一个随机数
  - client从证书中得到公钥，根据公钥，以及随机数算出一个加密秘钥，并把加密秘钥发送给server
  - server回复ok

- 证书有效性的验证？
  - 采用根证书验证server端的证书

- HTTP1.0到HTTP1.1到HTTP2.0的演进，有什么区别，体现在请求消息的哪些字段中？有没有实际用过？
  - HTTP1.0。 keepalive；content-length
  - HTTP1.1。默认长连接，请求流水线；分块chunked(解决需要携带content-length的问题)；断点续传
  - HTTP2.0。采用二进制分帧，解决pipeline对头阻塞的问题；头部压缩

- HTTP长连接和短连接，区别，长连接有什么好处
  - 短连接。一个请求建立一次tcp连接
  - 长连接。多个请求复用一条tcp连接，好处是减少了tcp连接的开销，同时提高了服务端的并发数

- HTTP常用状态码
  - 1开头
    - 1xx(临时响应)表示临时响应并需要请求者继续执行操作的状态代码。代码 说明
    - 100 (继续) 请求者应当继续提出请求。 服务器返回此代码表示已收到请求的第一部分，正在等待其余部分。
    - 101 (切换协议) 请求者已要求服务器切换协议，服务器已确认并准备切换。
  - 2开头
    - 2xx (成功)表示成功处理了请求的状态代码。代码 说明
    - 200 (成功) 服务器已成功处理了请求。 通常，这表示服务器提供了请求的网页。
    - 201 (已创建) 请求成功并且服务器创建了新的资源。
    - 202 (已接受) 服务器已接受请求，但尚未处理。
    - 203 (非授权信息) 服务器已成功处理了请求，但返回的信息可能来自另一来源。
    - 204 (无内容) 服务器成功处理了请求，但没有返回任何内容。
    - 205 (重置内容) 服务器成功处理了请求，但没有返回任何内容。
    - 206 (部分内容) 服务器成功处理了部分 GET 请求。
  - 3开头
    - 3xx (重定向) 表示要完成请求，需要进一步操作。 通常，这些状态代码用来重定向。代码 说明
    - 300 (多种选择) 针对请求，服务器可执行多种操作。 服务器可根据请求者(user agent) 选择一项操作，或提供操作列表供请求者选择。
    - 301 (永久移动) 请求的网页已永久移动到新位置。 服务器返回此响应(对 GET或 HEAD 请求的响应)时，会自动将请求者转到新位置。
    - 302(临时移动) 服务器目前从不同位置的网页响应请求，但请求者应继续使用原有位置来进行以后的请求。
    - 303 (查看其他位置) 请求者应当对不同的位置使用单独的 GET 请求来检索响应时，服务器返回此代码。
    - 304 (未修改) 自从上次请求后，请求的网页未修改过。 服务器返回此响应时，不会返回网页内容。
    - 305 (使用代理) 请求者只能使用代理访问请求的网页。 如果服务器返回此响应，还表示请求者应使用代理。
    - 307 (临时重定向) 服务器目前从不同位置的网页响应请求，但请求者应继续使用原有位置来进行以后的请求。
  - 4开头
    - 4xx(请求错误) 这些状态代码表示请求可能出错，妨碍了服务器的处理。代码 说明
    - 400 (错误请求) 服务器不理解请求的语法。
    - 401 (未授权) 请求要求身份验证。 对于需要登录的网页，服务器可能返回此响应。
    - 403 (禁止) 服务器拒绝请求。
    - 404 (未找到) 服务器找不到请求的网页。
    - 405 (方法禁用) 禁用请求中指定的方法。
    - 406 (不接受) 无法使用请求的内容特性响应请求的网页。
    - 407 (需要代理授权) 此状态代码与 401(未授权)类似，但指定请求者应当授权使用代理。
    - 408 (请求超时) 服务器等候请求时发生超时。
    - 409 (冲突) 服务器在完成请求时发生冲突。 服务器必须在响应中包含有关冲突的信息。
    - 410 (已删除) 如果请求的资源已永久删除，服务器就会返回此响应。
    - 411 (需要有效长度) 服务器不接受不含有效内容长度标头字段的请求。
    - 412 (未满足前提条件) 服务器未满足请求者在请求中设置的其中一个前提条件。
    - 413 (请求实体过大) 服务器无法处理请求，因为请求实体过大，超出服务器的处理能力。
    - 414 (请求的 URI 过长) 请求的 URI(通常为网址)过长，服务器无法处理。
    - 415 (不支持的媒体类型) 请求的格式不受请求页面的支持。
    - 416 (请求范围不符合要求) 如果页面无法提供请求的范围，则服务器会返回此状态代码。
    - 417 (未满足期望值) 服务器未满足"期望"请求标头字段的要求。
  - 5开头
    - 5xx(服务器错误)这些状态代码表示服务器在尝试处理请求时发生内部错误。这些错误可能是服务器本身的错误，而不是请求出错。代码 说明
    - 500 (服务器内部错误) 服务器遇到错误，无法完成请求。
    - 501 (尚未实施) 服务器不具备完成请求的功能。 例如，服务器无法识别请求方法时可能会返回此代码。
    - 502 (错误网关) 服务器作为网关或代理，从上游服务器收到无效响应。
    - 503 (服务不可用) 服务器目前无法使用(由于超载或停机维护)。 通常，这只是暂时状态。
    - 504 (网关超时) 服务器作为网关或代理，但是没有及时从上游服务器收到请求。
    - 505 (HTTP 版本不受支持) 服务器不支持请求中所用的 HTTP 协议版本

- HTTP状态码301与302的区别
  - 301，永久移动
  - 302，临时移动

- 206代表啥
  - 服务器成功处理了部分请求

- 浏览器打开网站的过程
  - DNS 解析:将域名解析成 IP 地址
  - TCP 连接：TCP 三次握手
  - 发送 HTTP 请求
  - 服务器处理请求并返回 HTTP 报文
  - 浏览器解析渲染页面
  - 断开连接：TCP 四次挥手
  - [《经典面试题：从 URL 输入到页面展现到底发生什么？》](https://blog.fundebug.com/2019/02/28/what-happens-from-url-to-webpage/)


- HTTP报文格式，深入的说一下，比如大文件怎么分块编码传输
  - HTTP1.1的新特性， 请求头增加了Transfer-Encoding: chunked属性
  - 目的是告诉客户端，响应body是分成了一块块的，块与块之间有间隔符，块的结尾有特殊标记