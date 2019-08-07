{{indexmenu_n>2}}

# 创建API分组

API分组是控制管理API的基本管理单元，需先创建API分组，然后再API分组下创建API

*   分组有Region和Project属性，创建的分组归于选定的Region和Project下，不可更改。
*   创建分组后，会给API分组分配一个二级域名，你可以访问该二级域名访问API分组下的API
*   若需自定义域名，可以在API分组下进行域名管理。需将自定义域名CNAME到分配域名后方可使用。
*   若需使用HTTPS协议，需为您的自定义域名上传SSL证书以及密钥。

在UAPI Gateway产品中切换至“开放API”，点击“创建API分组”，输入API分组名称及API分组描述。点击“确定”。

![创建API分组](/images/open_api/create_api_group.png)





