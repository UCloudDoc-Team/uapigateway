

# API管理

一个完成的API定义分为“基本信息”，“API请求定义”，“API后端定义”以及“API返回定义”。API具Region和Project属性。定义完成后皆不可更改。
*   基本信息包含API分组，API名称，API描述。API只能归属于同Region，同Project中的API分组下，定义后不可更改。
*   API请求定义，现在支持HTTP / HTTPS / HTTP(S)三种协议。系统根据API定义的protocol + domain + path + HTTPMethod 作为唯一的URI，需确保唯一。
*   后端请求现仅支持VPC一种请求类型，需先创建VPC授权后才可选择。


## 创建API
* API基本信息包含API所属分组，API米娜过程，API描述。同Region，同Project下的API定义名称不能相同。
* API请求定义包含支持协议，请求Path，匹配模式，HTTP Method和入参定义。
    * 请求协议：请求协议支持http / https / http(s)三种。
    * 匹配模式：匹配模式是指请求Path的匹配方法，如您的url为/userInfo，匹配模式为绝对匹配，则请求Path必须和定义一致。如匹配模式为前缀匹配，则能
    * 入参定义：入参定义分为两种类型：入参透传和入参映射，入参透传的情况下，会将客户端所有的query / body / header中的参数透传给后端。你也可以在请求Path中添加RestfulAPI推荐的Path Parameter，当使用PathParameter时必须使用入参映射，且需定义Path中的参数，参数类型选择Path,必传。如：定义的请求Path为 /userInfo/[userId]，则比如在参数列表中方式userId参数。匹配请求路径为/userInfo , /userInfo/ , /userInfo/get。

* API后端请求中，需设定后端服务和后端请求Path
    * 后端服务，可从VPC通道中获取VPC授权信息，或手动输入VPC授权ID。手动输入一般用在环境变量定义的情况下，适用于需要同一个程序在不同的主机中运行的情况下。
    * 后端请求Path中可方式环境变量和后端请求参数，后端请求参数仅只用于参数映射的情况下。
   
   
* API返回定义中，可设置ContentType，成功和失败返回示例，以及定义错误码。ContentType会根据设定加在HTTP Response Header中

    
    
    