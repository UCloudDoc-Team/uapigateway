

# 使用 Postman 签名

Postman 是常用调试后端 HTTP 服务，我们可以使用 POST 的 Pre-request Script 功能构建 HTTP 请求头完成签名。

![设置header](/images/use_api/postman1.png)

如图现在Headers 中填写签名的必要信息，变量参数定义在 {{}} 修饰符中，POSTMAN 中 {{}} 内的参数为全局变量。案例中我们所需两个全局变量：X-Gw-Timestamp和X-Gw-Signatured的参数值。

切换到 Pre-request Script 菜单下，Pre-request Script 内建了 javascript 解释器，结合 POSTMAN API 可以对 HTTP 请求参数进行修改。由于 POSTMAN 版本不同，造成 POSTMAN API 会有差别。具体 API [请参考](https://learning.getpostman.com/docs/postman/scripts/intro_to_scripts)

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
