{{indexmenu_n>5}}

# 创建API

API分组创建完成后您就可以创建API了，一个完成的API定义分为“基本信息”，“API请求定义”，“API后端定义”以及“API返回定义”。API具Region和Project属性。定义完成后皆不可更改。

*   基本信息包含API分组，API名称，API描述。API只能归属于同Region，同Project中的API分组下，定义后不可更改。
*   API请求定义，现在支持HTTP / HTTPS / HTTP(S)三种协议。系统根据API定义的protocol + domain + path + HTTPMethod 作为唯一的URI，需确保唯一。
*   后端请求现仅支持VPC一种请求类型，需先创建VPC授权后才可选择。


