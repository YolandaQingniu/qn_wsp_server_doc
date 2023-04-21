### 在线测试
接口地址: `GET /yolanda/test`

在线示例: http://wsp-sdk.yolanda.hk/yolanda/test

### 秤端与docker交互
接口地址: `GET /yolanda/wsp?code=`

在线示例: http://wsp-sdk.yolanda.hk/yolanda/wsp?code=ERROR

### 健康检查
接口地址: `GET /yolanda/healthcheck`

在线示例: http://wsp-sdk.yolanda.hk/yolanda/healthcheck

### 生成新的Hmac
接口地址: `POST /yolanda/generate_new_hmac`
参数: 
```sh
curl --request POST \
  --url http://your-docker-domain/yolanda/generate_new_hmac \
  --header 'Content-Type: application/json' \
  --data '{
  "old_hmac": "6EB5B207EB762FE1AED6B3C40D12E1ED5345AF7D6518A59B360C9860C07D2E9990E13E861404026D2413275F124CE0E37E9CA4E1AED6B3C488EDEEED6233EE92F29F0864515B5AB7FA29322C366EB5B29B23F753027B815F914E78A1DCA13FCBF887A03C1C7DFD890098884C81E78C025D27A0C84426B67BE9D2E4889B2E2CE3B6515A13853FCDB2F074D645F5DA4E7DAB01A1424D024F36C9BEAC40000",
  "model_id": "0204"
}'
```

返回值
```json
{
	"code": "200",
	"new_hmac": "3F828A0207EB762F6518A59B360C9860C07D2E9990E13E8614046EB5B275F124CE0E37E9CA4A2B08DCD613E1E1AED6B3C488EDEEE864515B5AB7FA29322C366EB5B29B23F753027B815F914E78A10D12E1ED5345AF7DDCA13FCBF887A03C1C7DFD890098884C81E78C025D27A0C84426B67BE9D2E4889B24C8DCD2737996308B28F38C6D211FDD5A4E7DAB01A1424D024F36C9BEAC40000"
}
```

注, 以上为假数据.

### 计算指标数据

请求地址: POST /yolanda/calculate

请求参数:

|字段|类型|是否必填|备注|其他信息|
|-|-|-|-|-|
|height|Float|必填|身高(cm)|mock: 180|
|birthday|String|必填|生日|mock: 1995-08-08|
|gender|Integer|必填|性别，0女，1男|mock: 1|
|algorithm|Integer|必填|算法|mock: 2|
|hmac|Integer|必填|Hmac	|mock: 21C422176CA1C23AA843984B1A363D00A315E2D3092BC0B5425F446CB17EC4CA3B5C270718D9A674FC9F70D498378E8A6F4FB43294A59997CEA1B3A443D1AE595333CEA5A359A9A8DC3AF50D14194566D4DE43C7AAB2D0ED2CFE9ACCFA951B42C17986190E03FD93F27F89474E1A4834D7D89C36A4A8F8BA319CE4A699841437DA2913598D510E3D7C74F16B0B64FD9D|

返回参数:

|字段|类型|是否必填|备注|
|-|-|-|-|
|code|String|必填|错误码|
|msg|String|必填|错误信息|
|calc_result|Object|必填|计算结果，为空对象表示计算出错|
|- score|Float|必填|分数|
|- weight|Float|必填|体重|
|- bodyfat|Float|必填|体脂率|
|- subfat|Float|必填|皮下脂肪|
|- visfat|Float|必填|内脏脂肪等级|
|- water|Float|必填|体水分|
|- bmr|Integer|必填|基础代谢|
|- bodyage|FloIntegerat|必填|体年龄|
|- muscle|Float|必填|骨骼肌率|
|- bone|Float|必填|骨量|
|- bmi|Float|必填|BMI|
|- sinew|Float|必填|肌肉量|
|- protein|Float|必填|蛋白质|
|- body_shape|Integer|必填|体型|
|- fat_free_weight|Float|必填|去脂体重|
|- heart_rate|Float|必填|心率|
|- cardiac_index|Float|必填|心脏指数|

参数示例:

```json
{
  "height": 180.0,
  "birthday": "1995-08-08",
  "gender": 1,
  "algorithm": 2,
  "hmac": "21C422176CA1C23AA843984B1A363D00A315E2D3092BC0B5425F446CB17EC4CA3B5C270718D9A674FC9F70D498378E8A6F4FB43294A59997CEA1B3A443D1AE595333CEA5A359A9A8DC3AF50D14194566D4DE43C7AAB2D0ED2CFE9ACCFA951B42C17986190E03FD93F27F89474E1A4834D7D89C36A4A8F8BA319CE4A699841437DA2913598D510E3D7C74F16B0B64FD9D"
}
```

返回值示例:

```json
{
  "code": "200",
  "msg": "ok",
  "calc_result": {
    "score": 86.5,
    "weight": 62.9,
    "bodyfat": 13,
    "subfat": 11.9,
    "visfat": 2.874408641975309,
    "water": 62.8,
    "bmr": 1552,
    "bodyage": 22,
    "muscle": 56.2,
    "bone": 2.74,
    "bmi": 19.4,
    "sinew": 52,
    "protein": 19.9,
    "body_shape": 4,
    "fat_free_weight": 54.7,
    "heart_rate": 93,
    "cardiac_index": 3.7
  }
}
```
