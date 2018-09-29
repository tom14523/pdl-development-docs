# <center><span id="ocr身份证识别">ocr身份证识别</span></center>
---

## 1. 接口地址
 > /api/ocr_id_card

## 2. 请求参数

| 参数名 | 类型 | 说明 | 是否必需 | 备注 |
| --| -- | -- | -- | -- |
| id_card_front_image   | string | 身份证正面图像           | Y | base64编码，要求base64编码后大小不超过4M，最短边至少15px，最长边最大4096px，支持jpg/png/bmp格式 |
| id_card_back_image    | string | 身份证背面图像            | Y | base64编码，要求base64编码后大小不超过4M，最短边至少15px，最长边最大4096px，支持jpg/png/bmp格式 |

## 3. 响应参数

| 参数名 | 类型 | 说明 | 是否必需 | 备注 |
| --| -- | -- | -- | -- |
| expiry_date       | string | 失效日期(背面信息)   | Y |格式：yyyy-mm-dd  |
| issuing_authority | string | 签发机关(背面信息)   | Y |  |
| id_no             | string | 公民身份号码(正面信息) | Y |  |
| address           | string | 住址(正面信息)      | Y |  |
| gender            | string | 性别(正面信息)      | Y | 男；女 |
| nation            | string | 民族(正面信息)      | Y | 如：汉 |
| issuing_date      | string | 签发日期(背面信息)   | Y |  |
| birth             | string | 生日(正面信息)      | Y | 格式：yyyy-mm-dd |
| id_name           | string | 姓名(正面信息)      | Y |  ||



## 4. 请求示例

```json
{
  "app_id":"abc",
  "sign":"DITCb3hZl2MKbtB9IAQGG7xN8f01la3kClVAoAJ93MMBRyJCy2kCb8TNd/Ctrfg1E5uRJqJdzqYzOWwqDEA4amMs0PNSm9LqDY9YAukF9aoKThZPQzxqMI8UapTZesfs5Os0wY6qE/GGRmrdgrEUmqYLf3wpEhazIQwsjdqCWBk=",
  "biz_data":{
    "id_card_front_image":"base64",
    "id_card_back_image":"base64"
  },
  "sign_type":"RSA",
  "timestamp":"1234567890"
}
```
## 5. 响应示例

* 正常响应示例 

```json
{
    "status": 200,
    "message": "OK",
    "data": {
        "expiry_date": "2023-05-16",
        "issuing_authority": "xxx公安局",
        "id_no": "xxx",
        "address": "xxx",
        "gender": "男",
        "nation": "汉",
        "issuing_date": "2013-05-16",
        "birth": "1996-10-17",
        "id_name": "xxx"
    },
    "timestamp": 1538188146722,
    "sign_type": "RSA"
}
```
