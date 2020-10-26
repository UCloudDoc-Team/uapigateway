

# VPC授权管理

VPC是用户专有网络，如何创建VPC请参考[创建VPC授权](https://docs.ucloud.cn/vpc/README)。VPC授权是用户同意将某个ULB / UHOST实例联通VPC, UAPIGateway将通过VPC网络代理到后端实例。注意ULB实例仅支持内网模式，输入的实例端口必须是可访问的。

VPC联通ULB可实现负载均衡的能力。
例如，创建一个内网ULB，在VServer上挂在一系列的服务节点。流量会由API网关，经由VPC通道达到ULB中定义的VServer的端口，再更具您定义的VServer转发配置到达后端服务。
<br/>
![VPC通道ULB](/images/open_api/uapigateway_vpc_access_ulb.png)  
<br/>
> 注意VPC通道仅支持TCP类型的VServer转发

## 创建VPC授权
* 在VPC授权菜单页面，点击“创建VPC授权”，输入“授权名称”，“授权描述”，选择你需要授权的VPC实例，再选择ULB / UHost实例，输入转发的端口。
* 如使用的资源类型为ULB,这里的端口填写的是VServer中的端口号。如果使用的是UHost，需要在host上监听端口，并在防火墙中开放该端口。

![创建VPC授权](/images/open_api/create_vpc_access.png)
> VPC授权一旦创建不可编辑



