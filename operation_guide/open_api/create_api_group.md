# API分组管理

API分组是控制管理API的基本管理单元，需先创建API分组，然后再API分组下创建API

*   分组有Region和Project属性，创建的分组归于选定的Region和Project下，不可更改。
*   创建分组后，会给API分组分配一个二级域名，你可以使用该二级域名访问API分组下的API。
*   API分组下可自定义域名。需将自定义域名CNAME到二级域名后使用。
*   如果自定义域名需要使用HTTPS协议，需为自定义域名上传SSL证书以及密。

> 注意，分配的二级域名仅供调试使用，服务正式上线之后请绑定自定义域名进行访问。


## 创建API分组
在UAPIGateway产品中切换至“开放API”，点击“创建API分组”，输入API分组名称及API分组描述。点击“确定”。
![创建API分组](/images/open_api/create_api_group.png)  

<br/>
<br/>

## 编辑API分组
在API分组详情中或者列表页中点击"详情"，然后点击基本信息下方的编辑按钮。和创建API分组类似，输入分组名称与分组描述。
![修改API分组](/images/open_api/modify_api_group.png)






