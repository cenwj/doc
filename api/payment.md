# 老虎外汇文档

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html)

==========================入金、出金、汇率=========================

#### <span id = "deposit_v2">1.申请入金【手机客户端入金(智付入金)】</span>
* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/deposit_v2
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/deposit_v2
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:deposit_v2|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|order_id|string|是|第三发传入的 id唯一标识 第三方入库订单号 ps:最大长度 VARCHAR（50）|
|amount|int|是|入金金额(美金usd)|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |请求成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息或者老虎账户信息|
|303| |安全验证失败|
|data| Object |返回的详细信息|
|usd_amount|string|美金金额|
|rmb_amount|string|人民币金额|
|usd_rate|string|当前入金汇率|
|order_no|string|老虎入库订单id|
|call_back_url|string|智付回调地址|
|order_time|string|申请入金时间|

说明:
>该接口是智付手机端入金接口，需要获取到返回的参数按照智付手机端sdk接收参数传递。
智付文档具体查看 [【智付文档】](http://www.dinpay.com/support.html)

返回成功json:
```
{
    "error_code":0,
    "error_msg":"成功",
    "is_succ":true,
    "data":{
        "usd_amount":"260",
        "rmb_amount":"1630.62",
        "usd_rate":"6.2716",
        "order_no":"952433",
        "call_back_url":"http://demo.tigerwit.com/action/public/v4/zhifupay",
        "order_time":"2016-09-06 15:20:54"
    }
}
```


#### <span id = "withdraw">2.申请出金</span>
* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/withdraw
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/withdraw
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:withdraw|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方user_id|
|mt4_id|int|是|老虎mt4_id|
|amount|float|是|申请出金金额(美金)|
|bank_name|string|是|银行名称|
|bank_addr|string|是|开行地址|
|card|string|是|银行卡号|
|id_no|string(32)|是|第三方用户信息身份证号码|
|username|string|是|第三方用户真实姓名|
|order_id|string(50)|是|第三方入库订单号|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |取消复制成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息|
|303| |验证失败|
|116| |该订单已经提交，不要重复提交|
|112| |出金必须大于20美金|
|113| |你还有复制的高手或者还有交易定单，请取消复制然后再出金。|
|114| |出金余额不足|
|115| |出金失败,系统错误|
|123| |银行卡信息和实名信息不能为空|
|400| |系统错误|
|data|Object|返回信息|
|order_no|int|第三方入库定单id|
|usd_amount|float|出金金额(usd)|
|rmb_amount|float|出金金额(rmb)|
|rate|double|出金汇率|

说明:
>当用户申请出金的时候，需要先调用[【获取银行卡信息】](#check_user_card)接口。无论用户是否已经绑定过银行信息,都需要传递用户的真实姓名和银行卡信息。
 [【获取银行卡信息】](#check_user_card) 接口是给第三方判断用户有没有绑定过银行卡信息。如果没有则需要首选让用户填写一遍银行卡信息。
用户需要修改银行卡信息，则把用户修改后的信息传递过来，下次获取的银行卡信息就是用户修改后的。

返回成功json:
```
{
    "is_succ":true,
    "data":{
        "order_no":951778,
        "usd_amount":20,
        "rmb_amount":123.43,
        "rate":6.1716
    },
    "error_msg":"",
    "error_code":0
}
```

#### <span id = "get_withdraw_rate">3.出金汇率</span>
* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/get_withdraw_rate
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_withdraw_rate
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_withdraw_rate|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |获取成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息|
|303| |验证失败|
|1| |获取汇率失败|
|withdraw_rate|string|返回信息|

返回成功json:
```
{
    "is_succ":true,
    "error_msg":"",
    "error_code":0,
    "withdraw_rate":"6.1716"
}
```

#### <span id = "get_exchange_rate">4.入金汇率</span>
* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/get_exchange_rate
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_exchange_rate
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_exchange_rate|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |获取成功|
|1| |获取失败|
|exchange_rate|string|汇率|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "exchange_rate":"6.9166"
}
```


#### <span id = "check_user_card">5.获取银行卡信息</span>
* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/check_user_card
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/check_user_card
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:check_user_card|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方user_id|
|mt4_id|int|是|绑定老虎的mt4_id|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true/false|
|error_msg|string|返回信息|
|error_code|number|返回码|
|0||获取成功|
|101||传递参数错误|
|105||获取不到第三方用户信息|
|data|Object|返回信息(空则没有绑定)|
|card|string|银行卡号|
|bank_name|string|银行名称|
|bank_addr|string|银行开户地址|

返回成功json:
```
{
    "is_succ":true,
    "error_msg":"成功",
    "error_code":0,
    "data":{
        "card":"18601309735",
        "bank_name":"中国联通",
        "bank_addr":"中国联通"
    }
}
```

#### <span id = "get_withdraw_info">5.获取可出余额，信用值，交易手数</span>
* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/get_withdraw_info
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_withdraw_info
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_withdraw_info|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true/false|
|error_msg|string|返回信息|
|error_code|number|返回码|
|0| |请求成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息或者老虎账户信息|
|303| |安全验证失败|
|7| |系统错误，获取用户余额失败|
|5| |您未满足出金条件，赠金不可提取|
|6| |您还有持仓订单，请平仓后再提现|
|data|object|返回的详细信息|
| payment |boolen|true/真实入金 false/赠金用户 |
| credit |string|信用值|
| volume | float |交易手数|
| balance | string |余额|
| withdraw_balance | string |出金余额|

说明:
>该接口是在用户申请出金的时候用到，给用户展示出金的具体余额信息

返回成功json:
```
{
    "error_code":0,
    "error_msg":"可以提现",
    "is_succ":true,
    "data":{
        "payment":true,
        "credit":"4305.12",
        "volume":0.04,
        "balance":"39780.98",
        "withdraw_balance":"36030.98"
    }
}
```


