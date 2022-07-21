# 附录

## 交易错误码

Error Code | Meaning | Description
---------- | ------- | -----------
101001 | 买家余额不足
101002 | 银行账户余额不足
101003 | 买家状态非法
101004 | 卖家状态非法
101005 | 账户号不存在
101006 | 产品未开通
101007 | 未开通支付工具
101008 | 未配置算费规则
101009 | 交易已支付
101010 | 交易已关闭
101011 | 交易状态异常
101012 | 交易存在风险
101013 | 交易失败
101014 | 交易不存在
101015 | 交易信息被篡改
101016 | 单笔交易金额超限
101017 | 高风险交易，已被阻断
101018 | 交易处理中
101019 | 日累计金额超限
101020 | 月累计金额超限
101021 | 订单金额低于单笔最小金额
101022 | 币种不支持
101023 | 商户状态异常
101024 | 用户状态异常
101025 | 付款账号状态异常
101026 | 收款账号状态异常
101027 | 账户余额不足
101028 | 没有支付成功的记录
101029 | 未匹配到系统订单
101030 | 不足以支付手续费
101031 | 支付银行不支持当前分期期数付款
101032 | 商户未开通当前支付银行


## 公共错误码

Error Code | Meaning | Description
---------- | ------- | -----------
0   | 成功 | 请求调用成功(不一定是业务成功)
900000 | 业务异常 | 通用业务异常
910001 | 非法的请求参数
910007 | 验签失败
999005 | 关键数据缺失 | 请求未知错误(状态未知)
999999 | 系统错误 | 请求未知错误(状态未知)

### 错误码解释

接口确认成功：http状态码==200并且code==0

接口确认失败：http状态码==200并且code > 0 and code < 999000

接口操作结果未知：不是确认成功、也不是确认失败，则为状态未知(else分支)，此时业务状态无法确定，需要回查或者其他机制确认，绝对不能认为是确认失败！！！

<aside class="notice">
上述判断仅用来判断接口的成功失败，具体交易状态，应该参考具体接口返回的具体错误码进行判断！
</aside>