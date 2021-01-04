# IP 信息服务
## 服务介绍
* **简介**
    * 全球IP地址信息查询，信息字段包含：国家/地区名称、省份/州名称、城市名称、中国行政区划代码、经度、纬度、时区ID、时区偏移、大洲代码、国家代码二位、国际电话代码、所有者域名、运营商
    * 国内精确到“城市”， 海外部分地区精确到“国家”

* **服务提供商**
  * [IPIP.NET](https://www.ipip.net)

* **产品优势**
  * 专业团队支撑，数据 24 小时准实时更新
  * 使用全球 600 个以上的自有网络监测点进行辅助测量
  * 与全球网络服务商进行 IP 信息方面的合作，保证数据持续准确

## 计费及使用限制
* 请求上限：2万次/小时（单VPC）
* 计费： 0.25元/千次，<font color=blue>每天100次免费</font> 不足1000次的按实际次数计算，精确到 0.01 元
* 结算：后付费，每日结算，按实际用量计费
* 异常调用：因服务端故障导致请求出错（HTTP 状态码 >=400）时，请求不计入计费次数
   
## 购买操作说明
* [购买操作说明](/uapigateway/operation_guide/thirdparty_api/ipip/ipinfo-manual)
  
## 接口调用说明

* **调用方式：**
   * vpc 中直接调用, 无需处理鉴权，系统会自动鉴权和计费

* **调用地址：**
  * http://ucloud.ipip.net/ip/:ip 
  * **注:** 
    * *":ip" 是要查询的目标 IP,查询当前请求的 client IP 时，传定值 ”current“（VPC 内调用时，client ip 是内网 IP，无实际意义）*
    * *VPC内调用时，只能在“购买时授权过的VPC”使用* 
    * *接口返回部分字段目前只支持“中文”，需要其它语言版本请联系: 4000188113*
  
* **请求方式：** GET
  
* **返回类型：** JSON

* **请求参数（Path)**

    |名称|类型|是否必选|描述|
    |---|----|---|---|
    |ip|String|是|IPV4地址|

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
        |country_name|string|国家/地区名称|
        |region_name|string|省份/州|名称|
        |city_name|string|城市名称|
        |china_admin_code|string|中国行政区划代码|
        |longitude|float|经度|
        |latitude|float|纬度|
        |timezone|string|时区ID|
        |utc_offset|string|时区偏移|
        |continent_code|string|大洲代码|
        |country_code|string|国家/地区代码二位|
        |idd_code|string|国际电话代码|
        |isp_domain|string|运营商域名；如：chinaunicom.com|

* **请求示例**
  
  curl 示例：

    ```
        curl http://ucloud.ipip.net/ip/43.227.197.201
    ```

    nodejs 示例：

    ```javascript
        var axios = require("axios")
        var url = "http://ucloud.ipip.net/ip/43.227.197.201"
        axios({
            method : "GET",
            url : url,
        }).then(function(response){
            console.log(response.data)
        })
    ```

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
            "country_code": "CN",
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
            "error": "Not globalunicast ip address"
        },
        "data": null
    }

    ```

* **错误码**
    
    |错误码	|错误信息|描述|
    |---|---|---|
    |0|Success|成功|
    |1001|Not globalunicast ip address|非公共IP地址|
    |1002|Not legal ipv4 address|IP地址不合法|
