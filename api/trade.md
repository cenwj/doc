# 老虎外汇文档

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html) 

## 接口分类 
### 开仓、平仓、挂单

#### <span id = "open_trader">1.开仓</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/open_trader
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/open_trader
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:open_trader|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方user_id|
|mt4_id|int|是|绑定老虎的mt4_id|
|cmd|int|是|交易类型 [0=>'买', 1=>'卖'] |
|symbol|string|是|交易品种|
|volume|float|是|开仓手数 这个不需要转换，如果用户下0.01手就传参0.01|
|tp|double|是|止盈价格[没有为0]|
|sl|double|是|止损价格[没有为0]|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |获取成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息|
|144| |定单类型错误|
|303| |验证失败|
|data|Object|返回的信息|
|ticket|int|定单号|
|symbol_en|string|交易品种(英文)|
|symbol_cn|string|交易品种(中文)|
|action|int|交易类型  [0=>'买', 1=>'卖']|
|open_price|double|开仓价格|
|volume|float|交易手数，不需要前端再做乘以0.01转换|
|occupy_asset|float|占用保证金|
|tp|double|止盈价格|
|sl|double|止损价格|
|margin_rate|double|预付款与存款货币的比率|
|open_time|string|开仓时间|

说明:
>开仓的时候可以同时设置止盈、止损，也可以单独设置止盈或止损。止盈和止损价格与当前报价的绝对值必须大于从[【所有交易品种详情】](/api/symbols.html#symbol_list_info)接口获取到的[stops_level]止损水平点。
开仓时设置止盈、止损价格需依据当前品种的实时平仓价来远离。
平仓价格是依据cmd确定。（cmd为0的时候取ask,cmd为1的时候取bid）
具体看[【报价推送】](/quote.html)

margin_rate:预付款与存款货币的比率
occupy_asset:占用保证金
字段返回的【occupy_asset】参数是没有做货币转换的，需要occupy_asset*margin_rate。

返回成功json:
```
{
    "is_succ":true,
    "error_msg":"交易成功",
    "error_code":0,
    "data":{
        "ticket":770814,
        "symbol_en":"AUDCAD",
        "action":0,
        "symbol_cn":"澳元加元",
        "open_price":85.58,
        "volume":0.01,
        "tp":0,
        "sl":0,
        "occupy_asset":10,
        "margin_rate":1,
        "open_time":"2010-11-11 11:11:11"
    }
}
```

#### <span id = "close_trader">2.平仓</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/close_trader
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/close_trader
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:close_trader|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方user_id|
|mt4_id|int|是|绑定老虎的mt4_id|
|ticket|int|是|定单id|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |获取成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息|
|130| |交易类型错误|
|144| |定单类型错误|
|303| |验证失败|
|data|Object|返回的信息|
|ticket|int|定单号|
|symbol_en|string|交易品种(英文)|
|symbol_cn|string|交易品种(中文)|
|action| int |交易类型  [0=>'买', 1=>'卖']|
|profit| float |收益|
|open_price|string|开仓价格|
|close_price|string|平仓价格|
|volume|float|交易手数，不需要前端再做乘以0.01转换|
|close_time|string|平仓时间|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"交易成功",
    "is_succ":true,
    "data":{
        "ticket":476041,
        "symbol_en":"USDCNH",
        "action":0,
        "symbol_cn":"美元人民币",
        "open_price":"6.74615",
        "profit":-0.12,
        "close_price":"6.74534",
        "volume":0.01,
        "close_time":"2011-11-11 11:11:11"
    }
}
```


#### <span id = "update_trader">3.修改订单止盈止损</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/update_trader
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/update_trader
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:update_trader|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方user_id|
|mt4_id|int|是|绑定老虎的mt4_id|
|ticket|int|是|定单id|
|sl|double|是|止损价格|
|tp|double|是|止盈价格|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |修改成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息|
|142| |不能修改别人定单|
|303| |验证失败|
|400| |修改失败|

返回成功json:
```
{
    "is_succ":true,
    "error_msg":"修改成功",
    "error_code":0
}
```

#### <span id = "pending_order">4.挂单交易接口</span>  [【挂单文档】](/pending.html)

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/pending_order
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/pending_order
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:pending_order|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|cmd|int|是|交易类型枚举，OP_BUY_LIMIT=>2, OP_SELL_LIMIT=>3, OP_BUY_STOP=>4, OP_SELL_STOP=>5, 传递数字|
|volume|float|是|交易手数，传0.01则为0.01手|
|symbol|string|是| 产品名称, 携带杠杆, 如EURUSD, XAUUSD200, HK50, 类型string|
|pending_price|double|是| 挂单价格|
|tp|double|是| 止盈价格, 不设置止盈该值为0|
|sl|double|是|  止损价格, 不设置止损该值为0|
|expiration_time|int|是| 过期时间戳, 具体过期时间为开仓时间加该时间戳秒数 永久为0,比如 要1个小时后过期 就传3600|

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
|data|object|返回的详细信息|
| mt4_id |int|下单mt4_id |
| order |int|成功的订单好|
| cmd | int |交易类型|
| volume | float |交易手数，不需要前端再做乘以0.01转换|
| symbol_en | string |下单交易品种 英文|
| symbol_cn| string |下单交易品种 中文|
| open_price | string |挂单价格|
| market_price | string |市场价格|
| tp | string |止盈价格|
| sl | string |止损价格|
| open_time | int |挂单建立时间|
| expiration | string |挂单过期时间|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":{
        "mt4_id":500970,
        "order":462082,
        "cmd":2,
        "volume":1,
        "symbol_cn":"NZDCAD",
        "symbol_en":"新西兰元加元",
        "open_price":"0.1441",
        "market_price":"0.94449",
        "tp":"0",
        "sl":"0",
        "open_time":1472194322,
        "expiration":"2016-11-11 11:11:11"
    }
}
```

#### <span id = "pending_modify">5.修改挂单</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/pending_modify
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/pending_modify
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:pending_modify|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|ticket|int|是|订单号|
|pending_price|double|是| 挂单价格|
|tp|double|是|止盈价格, 不修改原止盈为原值, 不使用止盈为0|
|sl|double|是|止损价格, 不修改原止损为原值, 不使用止损为0|
|expiration_time|int|是| 过期时间戳, 不修改为-1, 不使用过期时间为0|

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
|data|object|返回的详细信息|
| mt4_id |int|mt4_id |
| order |int|修改的订单号|
| cmd | int |交易类型|
| volume | float |交易手数，不需要前端再做乘以0.01转换|
| symbol_en | string |下单交易品种 英文|
| symbol_cn| string |下单交易品种 中文|
| open_price | string |挂单价格|
| market_price | double |市场价格|
| tp | string |止盈价格|
| sl | string |止损价格|
| open_time | string |挂单建立时间，本接口该值不会变化|
| expiration | int |挂单过期时间，0为不使用过期时间|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":{
        "mt4_id":500970,
        "order":462343,
        "cmd":2,
        "volume":1,
        "symbol_en":"NZDCAD",
        "symbol_cn":"中文产品",
        "open_price":"0.1441",
        "market_price":0,
        "tp":"0",
        "sl":"0",
        "open_time":"2016-11-11 11:11:11",
        "expiration":1472539005
    }
}
```

#### <span id = "pending_delete">6.删除挂单</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/pending_delete
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/pending_delete
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:pending_delete|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|ticket|int|是|订单号|

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
|data|object|返回的详细信息|
| mt4_id |int|mt4_id |
| order |int|修改的订单号|
| cmd | int |交易类型|
| volume | float |交易手数，不需要前端再做乘以0.01转换|
| symbol_en | string |下单交易品种 英文|
| symbol_cn| string |下单交易品种 中文|
| open_price | string |挂单价格|
| market_price | string |市场价格|
| tp | string |止盈价格|
| sl | string |止损价格|
| open_time | int |挂单建立时间，本接口该值不会变化|
| expiration | int |挂单过期时间，0为不使用过期时间|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":{
        "mt4_id":500970,
        "order":462343,
        "cmd":2,
        "volume":1,
        "symbol_en":"NZDCAD",
        "symbol_cn":"中文产品",
        "open_price":"0.1441",
        "market_price":"0",
        "tp":"0",
        "sl":"0",
        "open_time":1472538305,
        "expiration":1472539005
    }
}
```

#### <span id = "get_pending">7.获取所有挂单</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/get_pending
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_pending
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_pending|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|

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
|data|array|返回的详细信息|
|order|int|订单id|
|open_time|int|挂单建立时间|
|cmd|int|2=>'挂单买涨', 3=>'挂单买跌', 4=>'挂单买涨', 5=>'挂单买跌'|
|volume|float|交易手数，不需要前端再做乘以0.01转换|
|symbol_en|string|交易品种 英文|
|symbol_cn|string|交易品种 中文|
|open_price|string|挂单价格|
|sl|string|止损|
|tp|string|止盈|
|digits|int|小数点位|
|expiration|int|过期时间 时间戳|
|price|string|当前价格|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":[
        {
            "order":462338,
            "open_time":1472537895,
            "cmd":4,
            "volume":0.01,
            "symbol_en":"AUDJPY",
            "symbol_cn":"澳元日元",
            "open_price":"81",
            "sl":"0",
            "tp":"0",
            "digits":3,
            "price":"77.25",
            "expiration":0
        },
        {
            "order":462363,
            "open_time":"2016-11-11 11:11:11",
            "cmd":4,
            "volume":0.01,
            "symbol_en":"AUDCHF50",
            "symbol_cn":"澳元瑞郎",
            "open_price":"1.74001",
            "sl":0,
            "tp":0,
            "digits":5,
            "price":"0.74002",
            "expiration":0
        }
    ]
}
```
