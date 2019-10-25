

# 使用POSTMAN签名

POSTMAN常用调试后端HTTP服务，我们可以使用POST的Pre-request Script功能构建HTTP header 完成签名。

![设置header](/images/use_api/postman1.png)

如图现在Headers 中填写签名的必要信息，变量参数可以应{{}}符号把参数包裹，POSTMAN中{{}}内的参数为全局变量。案例中我们所需两个全局变量：X-Gw-Timestamp和X-Gw-Signatured的参数值。  

切换到Pre-request Script菜单下，Pre-request Script内建了javascript解释器，结合POSTMAN API可以对HTTP请求参数进行修改。由于POSTMAN版本不同，造成POSTMAN API会有差别。具体API[请参考](https://learning.getpostman.com/docs/postman/scripts/intro_to_scripts)

![pre-script](/images/use_api/postman2.png)

代码如下：

``` 
var stage = "user_prd_stage";
var appKey = "76976226127534999";
var appSecret = "d1bb0aead0fd4f36b7e58eb55de46543";
var timeStamp = Math.ceil(Date.now() / 1000)
var signedString = "X-Gw-Timestamp:"+timeStamp+",X-Gw-App-Key:"+appKey;
var signature = CryptoJS.HmacSHA256(signedString , appSecret).toString(CryptoJS.enc.Base64);
postman.setGlobalVariable("timeStamp" , timeStamp);
postman.setGlobalVariable("X-Gw-SignedString",signedString);
postman.setGlobalVariable("X-Gw-Signature",signature);
```
