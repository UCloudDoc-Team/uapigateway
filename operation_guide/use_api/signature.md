

# 加密签名
访问API的签名算法需要添加的Header：  
``` 
    X-Gw-Signature-Method : hmac-sha256   //必填，制定加密算法，现只支持hmac-sha256
    X-Gw-Signature-Headers : X-Gw-Timestamp, X-Gw-App-key //制定签名所需要的请求头 
    X-Gw-App-Key : APP KEY  // APP KEY
    X-Gw-Timestamp: 时间戳   // 时间戳
    X-Gw-Signature：签名     // 使用APP SECRET的签名字符串
```

签名字符串 
`SignedString：X-Gw-Timestamp:<时间戳>,X-Gw-App-Key:<AppKey>`  
使用APP SECRET对 SignedString进行签名(使用hmac-sha256算法)，并将签名结果添加到Header X-Gw-Signature中

