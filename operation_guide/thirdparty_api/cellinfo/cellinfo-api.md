# 基站信息查询服务

## 简介
  基站信息查询服务

## API 调用
* **调用地址：**
    * http://lbs.ucloud.cn/cellinfo

* **请求方式：** GET

* **返回类型：** JSON

* **请求参数（Path)**

  |名称|类型|参数位置|是否必选|描述|
  |--- |--- |--- |--- |--- |
  |mnc|String|Query|是|Mobile Country Code 移动设备国家代码|
  |mcc|String|Query|是|Mobile Network Code 移动设备网络代码|
  |lac|String|Query|是|LAC（GSM/WCDMA）或TAC（LTE），十进制|
  |ci |String|Query|是|Cell Identifier 十进制|
  

* **返回参数**
    * Meta字段：
      
      |字段名|字段类型|字段描述|
      |----|----|----|
      |code|int|错误码|
      |error|string|错误信息|

    * Data字段
      
      |字段名|字段类型|字段描述|
      |----|----|----|
      |mcc|int|Mobile Country Code 移动设备国家代码|
      |mnc|int|Mobile Network Code 移动设备网络代码|
      |lac|int|LAC（GSM/WCDMA）或TAC（LTE）|
      |ci|int|Cell Identifier|
      |lat|float|经度(WGS 坐标系)|
      |lon|float|经度(WGS 坐标系)|
      |acc|int|覆盖半径（米）|
      |addr|string|地址描述|
      |province|string|省/自治区/直辖市|
      |city|string|地级市/地区/自治州/盟 |
      |district|string|县级市/县/市辖区/自治县/旗|
      |township|string|镇/乡/街道|

* **请求示例**

  curl 示例：

    ```
    curl -i http://lbs.ucloud.cn/cellinfo?mnc=460&mcc=04&lac=4301&ci=20986
    ```


* **正常返回**

    ```json
    {
        "meta": {
            "code": 0,
            "error": ""
        },
        "data": {
            "mcc": 460,
            "mnc": 4,
            "lac": 4301,
            "ci": 20986,
            "lat": 40.008899,
            "lon": 116.483642,
            "acc": 903,
            "addr": "北京市朝阳区望京开发街道望京东路4号;利泽东街与屏翠东路路口东189米",
            "province": "北京市",
            "city": "",
            "district": "朝阳区",
            "township": "望京开发街道"
        }
    }

    ```

* **失败返回**

    ```json
    {
        "meta": {
            "code": 400,
            "error": "Not find cell info"
        },
        "data": null
    }

    ```