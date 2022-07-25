# 相关接口

## 创建二维码订单

> The request parameter example like this:

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

对此接口的一个描述。

### 流程图

[![二维码支付流程图](https://markdown.com.cn/assets/img/philly-magic-garden.9c0b4415.jpg "二维码支付流程图")](https://markdown.com.cn/assets/img/philly-magic-garden.9c0b4415.jpg)

### HTTP Request

`GET /upay/create-qrcode-payment`

### Request Parameters

Field     | Required | Type | The sample value | Description
--------- | -------- | ---- | ---------------- | -----------
outTradeNo | Y | string(32) | 2014072300007148 | 商户订单号，32个字符以内、只能包含字母、数字、下划线、横线；需保证在商户端不重复
outTradeTime | Y | string(19) | 2020-07-10 12:07:07 | 商户订单时间，时间字符串，格式：yyyy-MM-dd HH:mm:ss
