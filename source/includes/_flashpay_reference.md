# 接口规范

<aside class="success">
API 通信统一采用 HTTPS 的 POST 方式，POST 请求类型为 application/json ，UTF-8 编码
</aside>

## HTTP HEADER

Parameter | Required | Type | The sample value | Description
--------- | -------- | ---- | ---------------- | -----------
Content-Type | Y | string(32) | application/json | 商户订单号，32个字符以内、只能包含字母、数字、下划线、横线；需保证在商户端不重复
Accept-Language | N | string(2) | th | 语言，支持th、en、zh-CN，默认英文：en

## 公共参数

Parameter | Required | Type | The sample value | Description
--------- | -------- | ---- | ---------------- | -----------
Content-Type | Y | string(32) | application/json | 商户订单号，32个字符以内、只能包含字母、数字、下划线、横线；需保证在商户端不重复
Accept-Language | N | string(2) | th | 语言，支持th、en、zh-CN，默认英文：en

### 公共请求参数

Parameter | Required | Type | The sample value | Description
--------- | -------- | ---- | ---------------- | -----------
Content-Type | Y | string(32) | application/json | 商户订单号，32个字符以内、只能包含字母、数字、下划线、横线；需保证在商户端不重复
Accept-Language | N | string(2) | th | 语言，支持th、en、zh-CN，默认英文：en

### 公共响应参数

Parameter | Required | Type | The sample value | Description
--------- | -------- | ---- | ---------------- | -----------
Content-Type | Y | string(32) | application/json | 商户订单号，32个字符以内、只能包含字母、数字、下划线、横线；需保证在商户端不重复
Accept-Language | N | string(2) | th | 语言，支持th、en、zh-CN，默认英文：en

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
