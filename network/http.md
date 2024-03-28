---
layout: default
title: HTTP
parent: Network
---

## HTTP 协议

HTTP is an application protocol used to communicate between client and server.

## Status Code

| Status Code | Description                                                                                               |
|-------------|-----------------------------------------------------------------------------------------------------------|
| 1xx         | Informational                                                                                            |
| 100         | [Continue](https://tools.ietf.org/html/rfc7231#section-6.2.1) - Only a part of the request has been received by the server, but as long as it has not been rejected, the client should continue with the request. |
| 101         | [Switching Protocols](https://tools.ietf.org/html/rfc7231#section-6.2.2) - The server switches protocol. |
| 102         | [Processing](https://tools.ietf.org/html/rfc2518#section-10.1) - An interim response used to inform the client that the server has accepted the complete request, but has not yet completed it. |
| 2xx         | Success                                                                                                   |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) - The request is OK.                          |
| 201         | [Created](https://tools.ietf.org/html/rfc7231#section-6.3.2) - The request is complete, and a new resource is created. |
| 202         | [Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3) - The request is accepted for processing, but the processing is not complete. |
| 203         | [Non-Authoritative Information](https://tools.ietf.org/html/rfc7231#section-6.3.4) - The information in the entity header is from a local or third-party copy, not from the original server. |
| 204         | [No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5) - A status code and a header are given in the response, but there is no entity-body in the reply. |
| 205         | [Reset Content](https://tools.ietf.org/html/rfc7231#section-6.3.6) - The browser should clear the form used for this transaction for additional input. |
| 206         | [Partial Content](https://tools.ietf.org/html/rfc7233#section-4.1) - The server is returning partial data of the size requested. Used in response to a request specifying a Range header. The server must specify the range included in the response with the Content-Range header. |
| 3xx         | Redirection                                                                                              |
| 300         | [Multiple Choices](https://tools.ietf.org/html/rfc7231#section-6.4.1) - A link list. The user can select a link and go to that location. Maximum five addresses. |
| 301         | [Moved Permanently](https://tools.ietf.org/html/rfc7231#section-6.4.2) - The requested page has moved to a new url. |
| 302         | [Found](https://tools.ietf.org/html/rfc7231#section-6.4.3) - The requested page has moved temporarily to a new url. |
| 303         | [See Other](https://tools.ietf.org/html/rfc7231#section-6.4.4) - The requested page can be found under a different url. |
| 304         | [Not Modified](https://tools.ietf.org/html/rfc7232#section-4.1) - This is the response code to an If-Modified-Since or If-None-Match header, where the URL has not been modified since the specified date. |
| 305         | [Use Proxy](https://tools.ietf.org/html/rfc7231#section-6.4.5) - The requested URL must be accessed through the proxy mentioned in the Location header. |
| 306         | [Unused](https://tools.ietf.org/html/rfc7231#section-6.4.6) - This code was used in a previous version. It is no longer used, but the code is reserved. |
| 307         | [Temporary Redirect](https://tools.ietf.org/html/rfc7231#section-6.4.7) - The requested page has moved temporarily to a new url. |
| 4xx         | Client Error                                                                                             |
| 400         | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) - The server did not understand the request. |
| 401         | [Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1) - The requested page needs a username and a password. |
| 402         | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) - You can not use this code yet. |
| 403         | [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) - Access is forbidden to the requested page. |
| 404         | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) - The server can not find the requested page. |
| 405         | [Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5) - The method specified in the request is not allowed. |
| 406         | [Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6) - The server can only generate a response that is not accepted by the client. |
| 407         | [Proxy Authentication Required](https://tools.ietf.org/html/rfc7235#section-3.2) - You must authenticate with a proxy server before this request can be served. |
| 408         | [Request Timeout](https://tools.ietf.org/html/rfc7231#section-6.5.7) - The request took longer than the server was prepared to wait. |
| 409         | [Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8) - The request could not be completed because of a conflict. |
| 410         | [Gone](https://tools.ietf.org/html/rfc7231#section-6.5.9) - The requested page is no longer available. |
| 411         | [Length Required](https://tools.ietf.org/html/rfc7231#section-6.5.10) - The "Content-Length" is not defined. The server will not accept the request without it. |
| 412         | [Precondition Failed](https://tools.ietf.org/html/rfc7232#section-4.2) - The pre-condition given in the request evaluated to false by the server. |
| 413         | [Payload Too Large](https://tools.ietf.org/html/rfc7231#section-6.5.11) - The server will not accept the request because the request entity is too large. |
| 414         | [URI Too Long](https://tools.ietf.org/html/rfc7231#section-6.5.12) - The server will not accept the request because the URL is too long. Occurs when you convert a "post" request to a "get" request with a long query information. |
| 415         | [Unsupported Media Type](https://tools.ietf.org/html/rfc7231#section-6.5.13) - The server will not accept the request because the media type is not supported. |
| 416         | [Range Not Satisfiable](https://tools.ietf.org/html/rfc7233#section-4.4) - The requested byte range is not available and is out of bounds. |
| 417         | [Expectation Failed](https://tools.ietf.org/html/rfc7231#section-6.5.14) - The expectation given in an Expect request-header field could not be met by this server. |
| 426         | [Upgrade Required](https://tools.ietf.org/html/rfc7231#section-6.5.15) - The server refuses to perform the request using the current protocol but might be willing to do so after the client upgrades to a different protocol. |
| 5xx         | Server Error                                                                                             |
| 500         | [Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1) - The request was not completed. The server met an unexpected condition. |
| 501         | [Not Implemented](https://tools.ietf.org/html/rfc7231#section-6.6.2) - The request was not completed. The server did not support the functionality required. |
| 502         | [Bad Gateway](https://tools.ietf.org/html/rfc7231#section-6.6.3) - The request was not completed. The server received an invalid response from the upstream server. |
| 503         | [Service Unavailable](https://tools.ietf.org/html/rfc7231#section-6.6.4) - The request was not completed. The server is temporarily overloading or down. |
| 504         | [Gateway Timeout](https://tools.ietf.org/html/rfc7231#section-6.6.5) - The gateway has timed out.       |
| 505         | [HTTP Version Not Supported](https://tools.ietf.org/html/rfc7231#section-6.6.6) - The server does not support the "http protocol" version. |


### HTTPS

HTTPS（全称：Hyper Text Transfer Protocol Secure）是一种通过计算机网络进行安全通信的传输协议。HTTPS 通过对数据进行加密，保证了网络传输过程中的安全性。

HTTPS 使用 SSL/TLS 协议为 HTTP 加密，以此提供对数据的完整性、保密性和可验证性的保护。下面是 HTTPS 如何保证加密通信的基本流程：

1. **建立连接**：首先，客户端（如你的浏览器）将尝试与服务器建立一个 SSL/TLS 连接。这是通过在服务器和客户端之间进行一个握手过程来完成的。
2. **握手过程**：在握手过程中，服务器将向客户端发送其公钥和证书。证书包含了服务器的信息，例如服务器的域名、公钥，以及证书颁发机构的签名等。客户端将验证证书的有效性，例如检查证书是否过期，是否被知名的证书颁发机构颁发，证书的域名和服务器的域名是否一致等。
3. **密钥交换**：如果证书验证通过，客户端将使用服务器的公钥来加密一个随机生成的密钥（又叫"预主密钥"），然后将这个密文发送给服务器。服务器收到密文后，用自己的私钥解密，获取到客户端生成的密钥。这样，服务器和客户端就共享了同一个密钥，而且这个密钥在网络传输过程中没有明文的被传递过，保证了密钥的安全性。
4. **数据传输**：此后服务器和客户端就可以用这个共享的密钥来对传输的数据进行加密和解密，确保了数据传输的保密性。同时，TLS 还提供了一种机制来确认数据的完整性，保证了数据在传输过程中不会被篡改。
5. **断开连接**：数据传输完成后，双方可以选择关闭连接。如果稍后再次需要传输数据，就需要再次进行上述的握手过程。

总的来说，HTTPS 通过上述的方式，使得即使有人能够监听到服务器和客户端之间的通信，他们也无法理解通信的内容，因为数据被加密了。此外，他们也无法篡改数据，因为任何篡改都会被检测到。

## HSTS

HTTP Strict Transport Security (HSTS) 是一种网络安全策略机制，它使得网站能告知浏览器只能通过HTTPS进行通信，而不能使用HTTP。这样可以防止一种常见的网络攻击——SSL剥离攻击，它试图将安全的HTTPS连接降级为不安全的HTTP连接。

当一个支持HSTS的网站第一次通过HTTPS与用户的浏览器建立连接时，它会发送一个特殊的HTTP头，叫做`Strict-Transport-Security`。这个头包含两个主要的参数：

1. `max-age`：这个参数告诉浏览器在接下来的多长时间内（单位为秒），都应该只用HTTPS来访问该网站。
2. `includeSubDomains`（可选）：如果这个参数被指定，那么所有的子域名也都应该只用HTTPS来访问。

举个例子，如果一个网站发送了如下的HTTP头：

```
Strict-Transport-Security: max-age=31536000; includeSubDomains
```

这表示在接下来的31536000秒（也就是一年）内，浏览器只应该使用HTTPS来访问该网站和其所有子域名。

这样，即使用户尝试通过输入一个HTTP URL，或者点击一个HTTP链接来访问该网站，浏览器也会自动把这些HTTP请求转换为HTTPS请求。因此，即使有攻击者试图发动SSL剥离攻击，他们也无法成功，因为浏览器不会发送任何非加密的HTTP请求。

然而，需要注意的是，HSTS有一个缺点，那就是它只在浏览器第一次访问网站并接收到HSTS头之后才会生效。也就是说，如果用户第一次访问网站的时候已经被攻击者劫持并降级为HTTP连接，那么HSTS将无法防止这种攻击。这被称为HSTS的"引导问题"。为了解决这个问题，大部分主流浏览器都实现了一个"预加载"的HSTS列表，这个列表中的网站会被浏览器自动认定为只能通过HTTPS进行通信。这需要网站所有者主动将自己的网站提交到这个列表中。
