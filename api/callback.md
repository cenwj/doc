# <span id = "liucheng">老虎外汇文档</span>

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html)

## 接口分类 
### 老虎回调第三方接口(需提供第三方回调地址)
|||
|:--:|:--:|
|请求类型|post|
|请求地址|需第三方提供|
|请求说明|入金\出金结束后回调的接口|

请求第三方地址接收参数:

|参数名称|描述|类型|必填|
|:--|:--|:--|:--|
|order_no|第三方入库订单号|varchar(32)|是|
|order_amount|出金\入金金额（美元）|varchar(32)|是|
|trade_status|SUCCESS：成功；FAIL：失败|varchar(16)|是|
|function|WITHDRAW：出金；DEPOSIT：入金|varchar(16)|是|
|private_key|第三方私有key|varchar(32)|是|
|partner_key|第三方的合作伙伴Key|varchar(32)|是|
|partner_secret|第三方的合作伙伴Secret|varchar(64)|是|
|signature|签名|varchar(64)|是|

返回参数:

|参数名称|说明|类型|必需|
|:--|:--|:--|:--|
|code|是否成功 [成功:success,失败:fail]|string|yes|
|message|返回信息|string|yes|


json:
```
{
   "code": "success",
   "message": "回调成功",
 
}
```

说明：
>该接口是老虎外汇回调第三方合作伙伴的接口，接口地址需第三方提供给老虎外汇。`signature`参数生产同老虎外汇接口生成签名一样。

回调作用:
>当第三方用户成功入金和出金通知第三方入金、出金成功与否。

