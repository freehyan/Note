# HTTP

HTTP, 超文本传输层协议（HyperText Transfer Protocol），用于从**www服务器传输超文本到本地浏览器的网络层**传输协议，使浏览器更加高效和使网络传输
减少。保证计算机快速传输超文本文档，和确定传输文档哪部分，以及哪部分数据的先显示。

### HTTP请求响应模型

HTTP由请求和响应组成，标准的客户端服务器模型。HTTP客户端发起请求，服务端回送响应。

![][1]

HTTP是无状态协议，无状态指客户端和服务端不需要建立持久连接，意味着服务端回送响应之后，连接就关闭了，服务端不保留连接的有关信息。
HTTP遵循请求(Request)/响应(Reponse)模型，客户端发送请求，服务端响应请求和返回应答内容。

---
### HTTP工作过程

### HTTP 请求

HTTP请求报文由 **请求行（request line），请求头部（request head），空行和请求数据**四个部分组成。

![][2]

* 请求行以方法符号开头，后面跟着请求的URI和协议版本，中间以空格隔开：

> Method SP Request-URI SP HTTP-Version CRLF

	1. Method：由Request-URI标识的资源上所执行的方法
	2. Request-URI：统一资源标识符(通过简单的格式化字符串，通过名称、位置、或其他任何特性标识某个资源)
	3. HTTP-Version 请求的HTTP协议版本
	4. CRLF表示回车和换行
---
    GET /index.html HTTP/1.1
    POST http://192.168.2.217:8080/index.jsp HTTP/1.1

### HTTP 请求方法

|方法名称          |含义             |
|-----------------|----------------| 
|GET|获取由Request-URI所标识的资源的信息|
|POST|向服务器发送请求，要求服务器接收附在请求后面的数据|
|HEAD|HEAD方法只是请求消息报头，而不是完整的内容。通常用于测试超链接的有效性，是否可以访问，以及最近是否更新等。|
|PUT              |以提供的Request-URI存储封装的实体。 |
|DELETE           |请求原始服务器删除Request-URI标识的资源。 |

## HTTP 响应

服务端接收和解释消息后，返回HTTP响应消息，包含状态行，响应抱头，响应正文。

* 状态行：HTTP版本号，3位数字的状态码，描述状态的短语

> HTTP-Version Status-Code Reason-Phrase CRLF

* 响应报头： 响应消息报头包含了**普通报头、响应报头、实体报头**，普通报头和实体报头和请求消息报头中的普通报头、实体报头相同。
响应报头允许服务器传递不能放在状态行中的附加响应信息，以及关于服务器的信息和 对 Request-URI 所标识的资源进行下一步访问的信息

* 响应正文：HTTP请求的消息正文。

#### HTTP 状态码

HTTP状态码Web服务器告诉客户端发生了什么，状态码第一个数字代表当前响应的类型：

* 1xx：指示信息——表示请求已接收，继续处理
* 2xx：成功——表示请求已经被成功接收，理解，接受
* 3xx：重定向——要完成请求必须进行更进一步的操作
* 4xx：客户端错误——请求有语法错误或请求无法实现
* 5xx：服务器端错误——服务器未能实现合法的请求
---
* 200 **OK** 服务器成功处理了请求；
* 206 Partial Content（部分内容）代表服务器已经成功处理了部分GET请求（只有发送GET 方法的request, web服务器才可能返回206）
* 301 Moved Permanently（永久重定向）请求的URL已移走。Response中应该包含一个Location URL, 说明资源现在所处的位置
* 302 Moved Temporarily（临时重定向） 
* 304 Not Modified（未修改）客户的缓存资源是最新的，要客户端使用缓存
* 400 Bad Request（坏请求）告诉客户端，它发送了一个错误的请求。
* 401 Unauthorized（未授权）需要客户端对自己认证
* 404 **Not Found** 未找到资源
* 500 **Internal Server Error** 服务器遇到一个错误，使其无法对请求提供服务

---
### HTTPS

HHTPS, 安全套接字层超文本传输协议 (Hyper Text Transfer Protocol over Secure Socket Layer)。HTTPS是以安全为目标的HTTP通道，为了数据的安全，
HHTPS在http基础上加入了SSL协议，SSL依靠证书来验证服务器的身份，并为浏览器和服务器通信加密。

![][3]

* HTTPS 工作原理

	1. 浏览器发送HTTPS请求
	2. 服务端配置：服务端必须有数字证书：(公匙和私匙)。服务端返回公匙（包含证书颁发机构，有效时间等），自己保留私匙，
	3. 传送证书：客户端生成随机值，验证公匙是否有效，无效输出http警告；有效则用随机值加密公匙
	4. 传送加密信息：用证书加密的随机值，目的让服务端获取到这个随机值
	5. 服务端解密信息：利用私匙解密后，得到随机值，利用随机值把响应内容进行**对称加密**（信息和私匙混合在一起，只能通过私匙才能加密）
	6. 传输加密后信息：服务端用私匙加密后的，可在客户端还原
	7. 客户端通过一开始产生的随机值，获取解密内容


* HTTP 和 HTTPS 的区别：

	1. https协议需要到ca申请证书
	2. http是超文本传输协议，信息是明文传输，https则是具有安全性的ssl加密传输协议
	3. http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443
	4. http的连接很简单，是无状态的；HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全

---
### 问题

1. http协议Get和Post的区别？

GET一般用于**获取/查询**资源信息，而POST一般用于**更新**资源信息

	1. GET提交的数据会放在URL之后，以?分割URL和传输数据，参数之间以&相连，如EditPosts.aspx?name=test1&id=123456。POST则是把参数放在Request Body中
	2. 参数的数据类型，GET只接受ASCII字符，而POST没有限制。
	3. GET提交的数据大小有限制（因为浏览器对URL的长度有限制，实际上HTTP协议规范没有对URL长度进行限制），而POST方法提交的数据没有限制。
	4. GET安全和POST不安全，因为浏览器会缓存GET请求
	5. GET在浏览器回退时是无害的，而POST会再次提交请求。GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。
	6. GET方式需要使用Request.QueryString来取得变量的值，而POST方式通过Request.Form来获取变量的值，也就是说Get是通过地址栏来传值，而Post是通过提交表单来传值。
	7. 对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）；而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）。

直观上区别GET会URL在尾部添加访问参数，POST则是把参数放在Request Body中；GET方法url传入参数有长度限制，POST没有；


2. http和https的区别

	HTTPS是HTTP基础上安全加密的网络协议，需要申请证书，相对HTTP传输缓慢一些，但是安全性更高。通常一些银行网站都是使用HTTPS协议，而个人网站使用HTTP
	协议即可。 HTTP和HTTPS的连接方式不一致，目的端口也不一样。（HTTP 是80端口， HTTPS是443端口）。

3. http的状态码有哪些？

	* 200 表示服务端正确处理客户端请求；
	* 404，请求页面不存在；
	* 500，服务器遇到错误，无法对请求做出响应；

4. http的cookie和session

5. http1.0和1.1的区别

	* HTTP 1.0协议： 客户端与服务器建立连接后，只能获取1个web资源，获取资源后断开连接；
	* HHTP 1.1协议：客户端可一次获取web服务器多个资源，并不会断开连接；除非访问出错和手动断开连接


[1]:http_request_reponse.jpg
[2]:http_request.png
[3]:https_theory.png

---

### 资料

1. [HTTP基础：URL格式、 HTTP请求、响应、消息](http://www.cnblogs.com/mengdd/archive/2013/05/26/3099776.html)
2. [HTTP请求和响应格式](http://www.cnblogs.com/yaozhongxiao/archive/2013/03/02/2940252.html)
3. [一次完整的 HTTP 请求过程](http://blog.jobbole.com/106632/)
4. [图解HTTPS](http://www.cnblogs.com/zhuqil/archive/2012/07/23/2604572.html)
5. [http 1.0和1.1 的区别](http://www8.org/w8-papers/5c-protocols/key/key.html)
6. [通俗讲解http,HTTP/1.0和HTTP/1.1的区别](http://www.haowuyun.com/view/78)