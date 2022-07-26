# 接口规范

<aside class="success">
API 通信统一采用 HTTPS 的 POST 方式，POST 请求类型为 application/json ，UTF-8 编码
</aside>

## 公共参数

> 请求示例：

```json
{
  "appKey": "8038241718026163404840",
  "charset": "UTF-8",
  "signType": "RSA2",
  "sign": "",
  "time": "2022-01-12 13:14:15",
  "version": "1.0",
  "data": {
    "outTradeNo": "TEST-00001",
    "outTradeTime": "2022-01-12 13:14:15",
    "paymentAmount": 200,
    "cur": "THB",
    "subject": "这是个测试商户订单",
    "body": "แฟลชโฮมสแกนเติมเงิน",
    "notifyUrl": "https://test.com",
    "outUserId": "999999"
  }
}
```

> 响应示例：

```json
{
  "sign": "",
  "code": 0,
  "message": "Request Succeeded",
  "data": {
    "outTradeNo": "TEST-00001",
    "tradeNo": "220725040365063952",
    "tradeTime": "2022-07-25 20:37:29",
    "paymentAmount": 200,
    "cur": "THB",
    "billerId": "096072849481994",
    "qrImage": "",
    "qrRawData": "0002010102123057011509607284948199402182207253964830116520312103438218752520470115303764540125802TH5922TestMerchant16086435296007BANGKOK62340523202207250837298230000000703TPC63048CE0",
    "qrExpireTime": "2022-07-26 19:37:29"
  }
}
```

### HTTP HEADER

Field     | Required | Type | Example value    | Description
--------- | -------- | ---- | ---------------- | -----------
Content-Type | Y | string(32) | application/json | 商户订单号，32个字符以内、只能包含字母、数字、下划线、横线；需保证在商户端不重复
Accept-Language | N | string(2) | th | 语言，支持th、en、zh-CN，默认英文：en

### 公共请求参数

Field     | Required | Type | Example value    | Description
--------- | -------- | ---- | ---------------- | -----------
appKey | Y | string(32) | 1234567890ABCD1234567890 | FlashPay颁发的APP_KEY
charset | Y | string(10) | UTF-8 | 请求使用的编码格式，默认且只支持UTF-8
signType | Y | string(16) | RSA2 | 签名类型，默认且只支持RSA2(SHA256withRSA)
sign | Y | string | C380BEC2BFD727A4B6845133519F3AD6 | 签名，不参与签名
time | Y | string(19) | 2020-07-10 12:07:07 | 时间字符串，格式：yyyy-MM-dd HH:mm:ss
version | Y | string(10) | 1.0 | 调用的接口版本，目前固定为：1.0
data | Y | object |  | 数据体(具体参见每个接口的请求参数)

### 公共响应参数

Field     | Required | Type | Example value    | Description
--------- | -------- | ---- | ---------------- | -----------
code | Y | int(6) | 0 | 网关码(0：成功，只表达请求成功，非业务成功)
message | Y | string(64) | 成功 | 网关返回码描述
sign | Y | string(64) | C380BEC2BFD727A4B6845133519F3AD6 | 签名，不参与签名
data | N | object |  | 数据体(具体参见每个接口的响应参数)

## 签名算法

<aside class="success">
本文涉及到的接口，均需要对请求内容进行签名，并对FlashPay平台返回的内容进行验签！
</aside>

### 访问方式：

#### 商户访问平台

【商户请求】：商户应当用【商户私钥】对请求内容“签名“，平台收到请求后用【商户公钥】"验签"

【平台响应】：平台应当用【平台私钥】对响应内容“签名“，商户收到响应后用【平台公钥】"验签"

#### 平台访问商户

【平台请求】：平台应当用【平台私钥】对请求内容“签名“，商户收到请求后用【平台公钥】"验签"

【商户响应】：商户应当用【商户私钥】对响应内容“签名“，平台收到响应后用【商户公钥】"验签"

### 签名：

> Java 示例，具体可参考以下 jackson 的实现:

```java
 // 针对data字段的json序列化设置
// 去掉空值  
objectMapper.setSerializationInclusion(JsonInclude.Include.NON_EMPTY);
// 设置字母升序         
  objectMapper.configure(MapperFeature.SORT_PROPERTIES_ALPHABETICALLY,true);
  objectMapper.configure(SerializationFeature.ORDER_MAP_ENTRIES_BY_KEYS,true);   
```

> 签名原文示例：

```text
appKey=8045636385012971212808&charset=UTF-8&data={"body":"แฟลชโฮมสแกนเติมเงิน","cur":"THB","goodsCategory":"生活用品","goodsDetails":[{"body":"生活用品描述","goodsCategory":"生活用品","goodsId":"G0001","goodsName":"Goods0001","price":100,"quantity":2},{"body":"生活用品描述","goodsCategory":"生活用品","goodsId":"G0002","goodsName":"Goods0002","price":200,"quantity":4}],"notifyUrl":"https://test.com","operatorNo":"Y0001","outTradeNo":"PAT-00001","outTradeTime":"2022-01-12 13:14:15","outUserId":"999999","paymentAmount":200,"subject":"这是个测试商户订单"}&time=2022-01-12 13:14:15&version=1.0
```

#### Step1.1： 生成签名原文

- 首先将【公共请求参数】或【公共响应参数】中的字段按字母升序排好
- 剔除sign、signType以及空值字段（包括null和空字符串''）
- 对于data字段，如果为空（包括null和空字符串''）则不参与签名；如果不为空，则对该字段以字母序升序排列后进行json序列化
- 用&拼接上述字段，生成待签名字符串

#### Step1.2：签名

- 用私钥对【签名原文】进行RSA2（SHA256WithRSA）签名。
- 注意：【签名原文】String需要转化为UTF-8编码的byte[]，然后去签名，上述签名数据byte[]需要采用Base64编码转为String，并设置在sign字段上。

### 验签

#### Step2.1： 生成签名原文

按【Step1.1】方式一致的方式，生成签名原文

#### Step2.2： 验签

- 用对应公钥，与上述【Step2.1】生成的签名原文，对sign字段传入的签名进行RSA2（SHA256WithRSA）验签，验证结果为 true 则验证成功，否则验证未通过。
- 注意：【签名原文】String需要转化为UTF-8编码的byte[]。
- 注意：签名数据sign（String）需要采用Base64编码转为byte[]。
