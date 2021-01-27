# API 网关错误码定义

发生 API 调用异常时，请根据 HTTP Code 和响应头中的 `X-Gw-Message` 找到对应错误

| Message | HTTP Status Code | 语义 |
| ------ | --------- | --- |
| API not found error | 400 | API 不存在或未发布到制定环境 |
| Parameter error in API request | 400 | 请求入参错误 |
| API authentication error | 400 | API 鉴权错误 |
| Blocked for unpaied order | 400 | 有未支付账单 |
| Too many requests | 400 | API 流量超过限定阀值 |
| Request body is too large | 413 | 请求体体积过大 |
| URI is too Long | 414 | URI 过长 |
| Quota is not enough | 429 |  APP 授权配额不足 |
| Request header is too large | 494 | 请求过大 |
| SSL certificate error | 495 | SSL 证书校验错误 |
| Upstream service unavailable | 502 | 后端服务不可用 |
| Response body is too large | 502 | 响应体体积过大| 
| Response header is too large | 502 |响应头体积过大|

