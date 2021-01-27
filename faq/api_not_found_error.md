# API not found error API 未找到

API 网关根据用户指定的 `HTTP 规约` 找到对应的 `注册 API`，其中包括 `HTTP 协议` `HTTP Method` `URI` 等参数。
如您的 API 发布到非 `Release` 环境中，需在 `HTTP 请求头中` 携带 `X-Gw-Stage` 请求头。如发生 `API not found error`，请检查以下清单:

* API 请求协议，Method, URI 等是否与 API 规约相一致
* 检查 API 是否已经发布到所对应 Stage
* 检查 HTTP request header中的 X-Gw-Stage 参数是否设置正确，该值应设为 API 所发布的环境名相对应。

