---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
- json

toc_footers:
- <a href='#'>Sign Up for a Developer Key</a>
- <a href='https://flashpay.co.th/'>Documentation Powered by FlashPay</a>

includes:
- flashpay_reference
- flashpay_api
- flashpay_appendix
- flashpay_notice

search: true

code_clipboard: true

meta:
- name: description
  content: Documentation for the FlashPay API
---

# 文档说明

    在过去的几年中，无现金支付已成为泰国金融基础设施的重要组成部分，QR支付是其主要媒介之一。 FlashPay的开放API平台通过为合作伙伴和初创企业提供在其上进行开发的付款界面，使公众能够利用无现金支付趋势。

    本文档用来介绍QR 30支付产品。Thai QR Code Tag 30（QR 30）：支持商户出示QR码模式（C扫描B），在此模式下，用户扫描商户的QR码并使用活期账户或储蓄账户作为资金来源进行付款；大多数主要的泰国银行都支持这种QR支付方式。

# 接入准备

申请AppKey、RSA2签名的公钥私钥(FlashPay的密钥对，商户的密钥对)
- 泰国：
  - 生产环境域名：https://pay-openapi.flashfin.com
  - 测试环境域名：https://test-pay-openapi.flashfin.com
  
- 马来
  - 生产环境域名：https://pay-openapi.flashpayment.my
  - 测试环境域名：https://test-pay-openapi.flashpayment.my

