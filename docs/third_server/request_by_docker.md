# 公共分类

### 通用命令

#### 读取秤端密钥

接口地址: `POST /wsp/read_secret_key`

请求参数:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|mac|string|必须|Mac地址|mock: 12:34:56:78:9A:BC|

返回数据:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|secret_key|string|必须|秤端密钥(16位字符串, 空串表示读取不到)|mock: 123456789ABCDEFG|

#### 读取内部型号

接口地址: `POST /wsp/read_model_id`

请求参数:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|mac|string|必须|Mac地址|mock: 12:34:56:78:9A:BC|

返回数据:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|model_id|string|必须|内部型号(4位字符串, 空串表示读取不到)|mock: 067E|

### 20命令(获取用户信息和配置信息)

#### 读取秤端用户

接口地址: `POST /wsp/read_scale_users`

请求参数:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|mac|string|必须|Mac地址|mock: 12:34:56:78:9A:BC|

返回数据:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|scale_users|object []|必须|秤端用户数组(数组可为空数组)|item 类型: object|
|├─ user_index|integer|必须|用户索引(1-8)|mock: 2|
|├─ gender|integer|必须|性别(0为女 1为男)|mock: 1|
|├─ height|number|必须|身高(单位厘米, 保留一位小数)|mock: 180.5|
|├─ birthday|string|必须|生日(YYYY-mm-dd格式)|mock: 1990-01-01|
|├─ user_key|integer|必须|用户密钥(1000-9999)|mock: 1234|
|unit|integer|必须|单位 1 kg 2 lb 4 斤|mock: 1|

#### (客户定制)读取BOW秤端用户

接口地址: `POST /wsp/read_bow_scale_users`

请求参数:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|mac|string|必须|Mac地址|mock: 12:34:56:78:9A:BC|
|battery_level|integer|必须|电量 0-不支持电量 1-低电量 2-工作电量 4-满电量|mock: 1|

返回数据:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|scale_users|object []|必须|秤端用户数组(数组可为空数组)|item 类型: object|
|├─ user_index|integer|必须|用户索引(1-8)|mock: 2|
|├─ gender|integer|必须|性别(0为女 1为男)|mock: 1|
|├─ height|number|必须|身高(单位厘米, 保留一位小数)|mock: 180.5|
|├─ birthday|string|必须|生日(YYYY-mm-dd格式)|mock: 1990-01-01|
|├─ user_key|integer|必须|用户密钥(1000-9999)|mock: 1234|
|unit|integer|必须|单位 1 kg 2 lb 4 斤|mock: 1|
|ctrl|integer|必须|为1显示指标, 为0不显示 # Bit0->用户名 Bit1->BMI Bit2->骨量 Bit3->体脂率 Bit4->肌肉量 Bit5->体水分 Bit6->心率 Bit7->天气 Bit8->重量趋势|mock: 511|

#### 读取Ota版本

接口地址: `POST /wsp/read_ota_versions`

请求参数

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|mac|string|必须|Mac地址|mock: 12:34:56:78:9A:BC|

返回数据

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|ota_versions|object []|必须|固件版本列表|item 类型: object|
|├─ internal_model|string|必须|内部型号|mock: 029A|
|├─ hardware_model|string|必须|硬件型号|mock: 0001|
|├─ version|integer|必须|固件版本号|mock: 6|
|├─ crc|string|必须|文件校验和(8位)|mock: AABBCCDD|

### 21命令(上传数据)

#### 创建未知测量数据

接口地址: `POST /wsp/create_unknown_measurement`

请求参数:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|mac|string|必须|Mac地址|mock: 12:34:56:78:9A:BC|
|model_id|string|必须|型号ID(4位)|mock: 0E2B|
|weight|number|必须|体重|mock: 50.0|
|timestamp|integer|必须|测量时间戳(秒级)|mock: 1582698882|
|heart_rate|integer|必须|心率|mock: 93|
|resistance|integer|必须|50k电阻|mock: 500|
|sec_resistance|integer|必须|500k电阻|mock: 500|
|hmac|string|必须|签名(Hmac)|mock: Hmac|

返回数据:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|is_success|boolean|必须|是否成功|mock: true|


#### 创建测量数据

接口地址: `POST /wsp/create_measurement`

请求参数:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|mac|string|必须|Mac地址|mock: 12:34:56:78:9A:BC|
|model _id|string|必须|型号|mock: 00EA|
|user_index|integer|必须|用户索引|mock: 1|
|weight|number|必须|体重|mock: 50.0|
|timestamp|integer|必须|测量时间戳(秒级)|mock: 1582698882|
|heart_rate|integer|必须|心率|mock: 93|
|resistance|integer|必须|50k电阻|mock: 500|
|sec_resistance|integer|必须|500k电阻|mock: 500|
|bmi|integer|必须|BMI|mock: 21.1|
|bodyfat|number|必须|体脂率|mock: 27.6|
|body_shape|integer|必须|体型|mock: 4|
|fat_free_weight|number|必须|去脂体重|mock: 39.11|
|subfat|number|必须|皮下脂肪|mock: 25.8|
|visfat|integer|必须|内脏脂肪等级|mock: 4|
|water|number|必须|体水分|mock: 49.7|
|muscle|number|必须|骨骼肌率|mock: 42.2|
|sinew|number|必须|肌肉量|mock: 36.75|
|bone|number|必须|骨量(无机盐)|mock: 2.35|
|protein|number|必须|蛋白质|mock: 16.98|
|bmr|integer|必须|基础代谢|mock: 1214|
|bodyage|integer|必须|体年龄|mock: 27|
|score|number|必须|分数|mock: 91.9|
|cardiac_index|number|必须|心脏指数|mock: 2.7|
|hmac|string|必须|签名(Hmac)|mock: sfsfsffdsvsdvsd|

返回数据:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|is_success|boolean|必须|是否成功|mock: true|

### 22命令(20命令的信息确认)

#### 完成信息同步

接口地址: `POST /wsp/finish_info_sync`

请求参数:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|mac|string|必须|Mac地址|mock: 12:34:56:78:9A:BC|

返回数据:

|名称|类型|是否必须|备注|其他信息|
|--- |--- |--- |--- |--- |
|is_success|boolean|必须|是否成功|mock: true|
