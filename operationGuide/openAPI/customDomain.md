{{indexmenu_n>3}}

# 自定义域名

UAPI Gateway会为每个创建的API分组单独分配一个二级域名，您可以使用该域名来访问该分组下的API。Protocol + Domain + Path + HTTPMethod 用来确认API唯一性。注意分配的二级域名仅供开发和调试使用，开发API后请使用自定义域名访问。  
自定义域名，请确保您的域名满足以下条件：

*   自定义域名需要在ucloud备案系统中备案，请登录ucloud备案系统查询您域名的[备案情况](https://www.ucloud.cn/site/beian/index.html)
*   确保您的自定义域名已经CNAME至API分组的二级域名下。在控制台绑定域名时并无校验，如未解析则可能导致访问出错。
*   若您需要修改自定域名绑定的API分组，需先解绑，重新解析，再绑定到新的API分组
*   若您的API分组下的API使用HTTPS协议，还需上传SSL证书和私钥。


操作步骤：进入API分组详情，在右侧的自定义域名中栏中点击“绑定域名”，输入“自定义域名”，“SSL证书”，”密钥”。点击“确定”  

![自定义域名](/images/openAPI/customDomain.png)


