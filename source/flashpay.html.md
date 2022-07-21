---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
- json

toc_footers:
- <a href='#'>Sign Up for a Developer Key</a>
- <a href='https://flashpay.co.th/'>Documentation Powered by FlashPay</a>

includes:
- flashpay_access
- flashpay_appendix
- flashpay_notice

search: true

code_clipboard: true

meta:
- name: description
  content: Documentation for the FlashPay API
---

# 文档说明

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

# 接口规范

# 相关接口

## 创建二维码订单

> The request parameter example like this:

```json
{
  "appKey": "8045636385012971212808",
  "charset": "UTF-8",
  "signType": "RSA2",
  "sign": "",
  "time": "2022-01-12 13:14:15",
  "version": "1.0",
  "data": {
    "outTradeNo": "PAT-00001",
    "outTradeTime": "2022-01-12 13:14:15",
    "paymentAmount": 200,
    "cur": "THB",
    "subject": "这是个测试商户订单",
    "body": "แฟลชโฮมสแกนเติมเงิน",
    "expireTime": "",
    "notifyUrl": "https://test.com",
    "outUserId": "999999"
  }
}
```

对此接口的一个描述。

### HTTP Request

`GET /upay/create-qrcode-payment`

### Request Parameters

Parameter | Required | Type | The sample value | Description
--------- | -------- | ---- | ---------------- | -----------
outTradeNo | Y | string(32) | 2014072300007148 | 商户订单号，32个字符以内、只能包含字母、数字、下划线、横线；需保证在商户端不重复
outTradeTime | Y | string(19) | 2020-07-10 12:07:07 | 商户订单时间，时间字符串，格式：yyyy-MM-dd HH:mm:ss

<aside class="success">
API 通信统一采用 HTTPS 的 POST 方式，POST 请求类型为 application/json ，UTF-8 编码
</aside>

