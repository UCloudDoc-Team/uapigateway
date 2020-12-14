# IP 信息服务
## 服务介绍
* **简介**
    * 全球IP地址信息查询，信息字段包含：国家/地区名称、省份/州名称、城市名称、中国行政区划代码、经度、纬度、时区ID、时区偏移、大洲代码、国家代码二位、国际电话代码、所有者域名、运营商
    * 国内精确到“城市”， 国外部分地区精确到“国家”
    * 数据每日更新

* **服务提供商**
  * IPIP.NET

* **产品优势**
  * 专业团队支撑，数据 24 小时准实时更新
  * 使用全球 500 个以上的自有网络监测点进行辅助测量
  * 与全球网络服务商进行 IP 地理位置方面的合作，保证数据持续准确

## 计费及限制
* 请求限制：2万次/小时
* 计费： 0.25元/千次， 不足1000次的按实际次数计算，精确到 0.01 元
* 结算：后付费，每日结算，按实际用量计费
* 异常调用：因服务端故障导致请求出错（HTTP 状态码 >=400）时，请求不计入计费次数
    
## 接口调用说明

* **调用地址：**
  * http(s)://ip-info.ucloud365.com/v1/ipip/:ip (外网调用)
  * http://ip-info.service.ucloudapi.com/v1/ipip/:ip (客户VPC内调用)


   **注:** 
    * *查询指定IP时，“:ip" 传指定的IP*
    * *查询当前请求的IP信息时，“ip" 传定值 ”current“*
    * *客户VPC内调用时，只能调用同 region 的地址，不能跨 region 调用* 
    * *接口返回部分字段目前只支持“中文”，需要其它语言版本请联系: 4000188113*
  
* **请求方式：** GET
  
* **返回类型：** JSON
  
* **API 调用：** [API 签名认证调用方法（AppKey & AppSecret）](/uapigateway/operation_guide/use_api/signature)

* **请求参数（Headers）**

    | header 名称 | 必填 | 描述 |
    | ---- | ----| -----|
    | X-Gw-Signature-Method | 是 | 加密算法，目前只支持 hmac-sha256 |
    | X-Gw-Signature-Headers | 是 | 签名所需要的请求头，填写 X-Gw-Timestamp,X-Gw-App-Key |
    | X-Gw-App-Key | 是 | 签名 AppKey，在控制台 App 详情页中获取 |
    | X-Gw-Timestamp | 是 | 签名时间戳, UNIX 类型 |
    | X-Gw-SignedString | 是 | 被签名字符串，格式为 "X-Gw-Timestamp:"+签名时间戳+",X-Gw-App-Key:"+AppKey |
    | X-Gw-Signature | 是 | 签名值 |
    | X-Gw-Stage | 否 | 如调用环境为 RELEASE 环境可不填，API 市场中订阅的 API调用 可不填 |

* **请求参数（Path)**

    |名称|类型|是否必选|描述|
    |---|----|---|---|
    |ip|String|是|IPV4地址|

* **请求参数（Body）**
  
  无

* **返回参数**
    * Meta字段：
        |字段名|字段类型|字段描述|
        |----|----|----|
        |code|int|错误码|
        |error|string|错误信息|

    * Data字段
        |字段名|字段类型|字段描述|
        |----|----|----|
        |addr|string|所查询的 IP 地址|
        |country_name|string|国家名称|
        |region_name|string|省份/州|名称|
        |city_name|string|城市名称|
        |china_admin_code|string|中国行政区划代码|
        |longitude|float|经度|
        |latitude|float|纬度|
        |timezone|string|时区ID|
        |utc_offset|string|时区偏移|
        |continent_code|string|大洲代码|
        |country_code|string|国家代码二位|
        |idd_code|string|国际电话代码|
        |isp_domain|string|运营商域名；如：chinaunicom.com|

* **请求示例**
  
    <details>
        <summary>postman</summary>

    ```js
        var stage = "RELEASE";  //授权的API所在的环境，默认是 RELEASE 
        var appKey = "xxxxxxxxx"; //被目标API授权过的 APP 的 appKey
        var appSecret = "xxxxxxxxxxxxx"; //被目标 API 授权过的 APP 的 appSrecet
        var timeStamp = Math.ceil(Date.now() / 1000)
        var signedString = "X-Gw-Timestamp:"+timeStamp+",X-Gw-App-Key:"+appKey;
        var signature = CryptoJS.HmacSHA256(signedString , appSecret).toString(CryptoJS.enc.Base64);
        postman.setGlobalVariable("timeStamp" , timeStamp);
        postman.setGlobalVariable("X-Gw-SignedString",signedString);
        postman.setGlobalVariable("X-Gw-Signature",signature);
        postman.setGlobalVariable("X-Gw-Stage", stage);
    ```
    </details>

    <details>
        <summary>nodejs</summary>

    ```js
        var axios = require("axios")
        var CryptoJS = require("crypto-js");

        var signHeaders = "X-Gw-Timestamp,X-Gw-App-Key"
        var appKey = "kkkkkkkkkkkkk" //AppKey
        var appSecret = "xxxxxxxxxx" //AppSecret

        var timeStamp = Math.ceil(Date.now() / 1000)
        var signedString = "X-Gw-Timestamp:"+timeStamp+",X-Gw-App-Key:"+appKey;
        var signature = CryptoJS.HmacSHA256(signedString , appSecret).toString(CryptoJS.enc.Base64);

        var url = "https://ip-info.ucloud365.com/v1/ipip/current"
        axios({
            method : "GET",
            url : url,
            headers : {
                "X-Gw-Signature-Method"  : "hmac-sha256",
                "X-Gw-Signature-Headers" : signHeaders,
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
    </details>

    <details>
        <summary>Golang</summary>

    ```golang
    package main

    import (
        "crypto/hmac"
        "crypto/sha256"
        "encoding/base64"
        "fmt"
        "io/ioutil"
        "net/http"
        "strings"
        "time"
    )

    /*
    X-Gw-SignatureMethod
    X-Gw-SignatureHeaders
    X-Gw-Signature
    X-Gw-AppKey
    X-Gw-Timestamp
    */

    // return (signature, signatureString)
    func GetSignature(secret string, signatureHeaders []string, headers map[string]string) (string, string) {

        hash := hmac.New(sha256.New, []byte(secret))
        signatureString := ""
        for idx, signatureHeader := range signatureHeaders {
            signatureString = signatureString + signatureHeader + ":" + headers[signatureHeader]
            if idx > 0 {
                signatureString = "," + signatureString
            }
        }
        hash.Write([]byte(signatureString))
        md := hash.Sum(nil)
        signature := base64.StdEncoding.EncodeToString(md)
        return signature, signatureString
    }

    func DoRequest(method string, url string, body string, headers map[string]string) {
        client := &http.Client{}
        req, _ := http.NewRequest(method, url, strings.NewReader(body))
        for k, v := range headers {
            req.Header.Set(k, v)
        }
        resp, _ := client.Do(req)
        respContent, errRead := ioutil.ReadAll(resp.Body)
        if errRead != nil {
            fmt.Println(errRead)
        } else {
            fmt.Println(respContent)
            resp.Body.Close()
        }
    }

    func main() {
        key := "kkkkkkkkk"  //appKey
        secret := "xxxxxxxx"  //appSecret

        var headers map[string]string
        headers = make(map[string]string)
        headers["X-Gw-SignatureMethod"] = "hmac-sha256"
        headers["X-Gw-SignatureHeaders"] = "X-Gw-Timestamp,X-Gw-AppKey"
        headers["X-Gw-Signature"] = ""
        headers["X-Gw-AppKey"] = key
        headers["X-Gw-Timestamp"] = fmt.Sprintf("%d", time.Now().Unix())
        signatureHeaders := []string{"X-Gw-Timestamp", "X-Gw-AppKey"}
        signature, signatureString := GetSignature(secret, signatureHeaders, headers)
        headers["X-Gw-Signature"] = signature

        fmt.Println(signature)
        fmt.Println(signatureString)
        DoRequest("GET", "https://ip-info.ucloud365.com/v1/ipip/43.227.197.201", "", headers)
    }

    ```
    </details>

* **正常返回**

```json
{
    "meta": {
        "code": 0,
        "error": ""
    },
    "data": {
        "addr": "43.227.197.201",
        "city_name": "杭州",
        "country_name": "中国",
        "isp_domain": "电信",
        "continent_code": "AP",
        "country_ce": "",
        "idd_code": "86",
        "latitude": "30.252501",
        "longitude": "120.165024",
        "owner_domain": "",
        "region_name": "浙江",
        "timezone": "Asia/Shanghai",
        "utc_offset": "UTC+8"
    }
}
```

* **失败返回**
```json
{
    "meta": {
        "code": 1001,
        "error": "Not global unicast ip address"
    },
    "data": null
}

```

* **错误码**
    
    |错误码	|错误信息|描述|
    |---|---|---|
    |0|Success|成功|
    |1001|Not global unicast ip address|非公共IP地址|
    |1002|Not legal ipv4 address|IP地址不合法|
