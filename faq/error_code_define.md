

# UAPIGateway错误码定义
| 错误消息 | HTTP状态码 | 语义 | 
| ------ | ---------|
| API not found error | 400 | API不存在或未发布到制定环境 |
| Parameter error in API request | 400 | 请求入参错误 |
| API authentication error | 400 | API鉴权错误 |
| Blocked for unpaied order | 400 | 有未支付账单 |
| Too many requests | 400 | API流量超过限定阀值 |
| Request body is too large | 413 | 请求body size过大 |
| URI is too Long | 414 | URL过长 |
| Quota is not enough | 429 |  APP授权配额不足 |
| Request header is too large | 494 | 请求header size过大 |
| SSL certificate error | 495 | ssl 证书校验错误 |
| Upstream service unavailable | 502 | 后端服务不可用 |
| Response body is too large | 502 | 响应body size 过大| 
| Response header is too large | 502 |响应header size过大|

