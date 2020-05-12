# 跨域共享

## 什么是跨域共享
跨域资源共享(CORS)是一种机制，它使用额外的HTTP头来告诉浏览器，让运行在一个域名(domain)上的Web应用被准许访问来自不同域名的服务器
上的指定资源，当一个资源从与该资源本身所在的服务器不同的域，协议或端口请求一个资源时，资源会发起一个跨域HTTP请求。
浏览器处于安全考虑，会限制从脚本内发起的跨域HTTP请求。例如XMLHttpRequest和Fetch。
API遵循同源策略，这意味着使用这些API的Web应用程序只能从加载应用程序的同一个域请求HTTP资源，除非响应报文包含了正确的CORS响应头。


## 简单请求与非简单请求
对于跨域HTTP请求，浏览器会根据发送API的结构内，来判断请求是否是一个简单跨域请求。一个非简单跨域请求会在请求前发送一个Method为OPTIONS
的请求进行预检(pre-flight)。包含以下条件的请求可视为简单请求：

* 使用下列方法之一：
    * GET
    * HEAD
    * POST
* 只能包含以下HTTP头
    * Accept
    * Accept-Language
    * Content-Language
    * Content-Type （需要注意额外的限制）
    * DPR
    * Downlink
    * Save-Data
    * Viewport-Width
    * Width 
* Content-Type 的值仅限于下列三者之一：
    * text/plain
    * multipart/form-data
    * application/x-www-form-urlencoded  
* 请求中的任意XMLHttpRequestUpload 对象均没有注册任何事件监听器；XMLHttpRequestUpload 对象可以使用 XMLHttpRequest.upload 属性访问。
* 请求中没有使用 ReadableStream 对象。
 
 
 ## UAPIGateway对于CORS的支持
 对于已经绑定了CORS跨域策略的API，UAPIGateway会根据后端的响应内容来决定是否加上CORS响应头。如后端无任何CORS响应头，UAPIGateway会加上以下响应头
 ```
 Access-Control-Allow-Origin : $http_origin
 Access-Control-Allow-Header : X-Gw-Signature-Method,X-Gw-Signature-Headers,X-Gw-Signature-Headers,X-Gw-Timestamp,X-Gw-Timestamp,X-Gw-SignedString,X-Gw-Stage,Authorization,Content-Type,Accept,Accept-Ranges,Cache-Control,Range
 Access-Control-Allow-Method : POST,GET,DELETE,OPTIONS,HEAD,PUT
 Access-Control-Expose-Header : X-Gw-Signature-Method,X-Gw-Signature-Headers,X-Gw-Signature-Headers,X-Gw-Timestamp,X-Gw-Timestamp,X-Gw-SignedString,X-Gw-Stage,Authorization,Content-Type,Accept,Accept-Ranges,Cache-Control,Range
 Access-Control-Allow-CREDENTIALS: true   
 ```
 <br/>
 对于返回了CORS的Header中的任一响应头的请求，我们视其为用户想要自行进行CORS响应头的处理，UAPIGateway不对CORS响应头做任何处理。
 
 
    

