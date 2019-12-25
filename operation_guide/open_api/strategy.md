# 策略描述

* 策略是针对API的限制与开放条件，创建策略时需按照对应的策略模版制定策略。策略内容现支持YAML和JSON两个格式的文本，下面是CORS跨域策略的示例
* 策略生成后，可绑定对应环境上的API，你可以在策略详情中的**已绑定API**列表中查看对应API信息，以及API的发布状态。策略绑定后，即刻生效。
  
YAML示例：  
```yaml
---
allowOrigins: www.ucloud.cn	# 允许的ORIGIN,用逗号分隔, "*"代表所有域
allowMethods: GET,POST,PUT				# 允许的方法,用逗号分隔
allowHeaders: X-Gw-Request-Id			# 允许的请求头部,用逗号分隔
exposeHeaders: X-RC1,X-RC2			# 允许暴露给XMLHttpRequest对象的头,用逗号分隔
allowCredentials: true					# 是否允许Cookie
maxAge: 172800
```
  
JSON示例：  
```json
{
    "allowOrigins" : "www.ucloud.cn",  //允许的ORIGIN,用逗号分隔, "*"代表所有域
    "allowMethods" : "GET,POST,PUT",   //允许的方法,用逗号分隔
    "allowHeaders" : "X-Gw-Request-Id",  //允许的请求头部,用逗号分隔
    "exposeHeaders" : "exposeHeaders",  //允许暴露给XMLHttpRequest对象的头,用逗号分隔
    "allowCredentials" : true,          //是否允许Cookie
    "maxAge" : 172800                   //预检缓存时间，单位为秒
}
```

## 创建策略
为了保证正确识别，同项目下的策略不能重名。对于不同类型的策略，配置可能会不同，具体请参考响应的默认配置以及代码注释。
![创建策略](/images/open_api/create_strategy.png)

## API绑定策略
策略可绑定在API制定的环境上，如果API已在环境下运行，无需发布即刻生效。如你的策略已在使用中，请谨慎修改。
绑定API时，先根据API分组进行筛选，而后选中所要绑定的API，选择所需绑定的环境，点击确定。
![策略绑定API](/images/open_api/strategy_bind_apis.png)
