

# 加密签名
## 访问API的签名算法需要添加的Header：

| 请求头 | 必填 | 描述 |
| ---- | ----| -----|
| X-Gw-Signature-Method | 是 | 加密算法，目前只支持 hmac-sha256 |
| X-Gw-Signature-Headers | 是 | 签名所需要的请求头，填写 X-Gw-Timestamp,X-Gw-App-Key |
| X-Gw-App-Key | 是 | 签名 AppKey，在控制台 App 详情页中获取 |
| X-Gw-Timestamp | 是 | UNIX 签名时间戳, |
| X-Gw-SignedString | 是 | 被签名字符串，格式为 "X-Gw-Timestamp:"+签名时间戳+",X-Gw-App-Key:"+AppKey |
| X-Gw-Signature | 是 | 签名值 |
| X-Gw-Stage | 否 | 如调用环境为 RELEASE 环境可不填，API 市场中订阅的 API调用 可不填 |

## NodeJs 版本签名代码
```js
var axios = require("axios")
var CryptoJS = require("crypto-js");


var signHeaders = "X-Gw-Timestamp,X-Gw-App-Key"
var appKey = "xxxxxxxxxxxxxxxxxxxx"
var appSecret = "yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy"


var timeStamp = Math.ceil(Date.now() / 1000)
var signedString = "X-Gw-Timestamp:"+timeStamp+",X-Gw-App-Key:"+appKey;
var signature = CryptoJS.HmacSHA256(signedString , appSecret).toString(CryptoJS.enc.Base64);

var url = "http://demo.ucloudapi.com/getUserInfo/v1"

axios({
	method : "GET",
	url : url,
	headers : {
		"X-Gw-Signature-Method"  : "hmac-sha256",
		"X-Gw-Signature-Headers" : "X-Gw-Timestamp,X-Gw-App-Key",
		"X-Gw-App-Key"           : appKey,
		"X-Gw-Timestamp"         : timeStamp,
		"X-Gw-Signature"         : signature,
		"X-Gw-SignedString"      : signedString,
		"X-Gw-Stage"             : "RELEASE"
	}
}).then(function(response){
	console.log(response.data)
})

```

