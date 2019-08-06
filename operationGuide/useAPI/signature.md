#加密签名
访问API的签名算法  
需要添加的Header：  
`   X-Gw-Signature-Method : hmac-sha256  
	X-Gw-Signature-Headers : X-Gw-Timestamp, X-Gw-App-key
	X-Gw-App-Key : APP KEY
	X-Gw-Timestamp: 时间戳
	X-Gw-Signature：签名
`

签名的计算 
`SignedString：“X-Gw-Timestamp:<时间戳>,X-Gw-App-Key:<AppKey>`  
使用APP SECRET对 SignedString进行签名(使用hmac-sha256算法)，并将签名结果添加到Header X-Gw-Signature中

