

# 创建VPC授权

VPC是用户专有网络，如何创建VPC请参考[如何创建VPC授权]((https://docs.ucloud.cn/network/vpc/index))。VPC授权是用户同意将某个ULB / UHOST实例联通VPC, UAPIGateway将通过VPC网络代理到后端实例。注意ULB实例仅支持内网模式，输入的实例端口必须是可访问的。

在VPC授权菜单页面，点击“创建VPC授权”，输入“授权名称”，“授权描述”，选择你需要授权的VPC实例，再选择ULB / UHOST实例，输入转发的端口。

![创建VPC授权](/images/open_api/create_vpc_access.png)

