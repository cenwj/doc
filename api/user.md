# 老虎外汇文档

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html) 

## 接口分类 
### 开户、个人中心

#### <span id = "signup">1.开户</span>
* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/signup_v2
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/signup_v2
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:signup_v2|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方user_id|
|phone|int|是|第三方用户手机号码|
|id_no|string|是|第三方用户身份证号码|
|username|string|是|第三方用户真实姓名|


返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0||获取成功|
|101| |传递参数错误|
|102| |手机号码不正确|
|104| |生成mt4失败|
|105| |获取不到第三方用户信息|
|109| |第三方user_id已经绑定过老虎账户|
|303| |验证失败|
|117| |身份证号码第三方用户名称不能为空|
|mt4_id|string|第三方用户开户成功后的返回老虎帐号mt4_id|
|password|string|第三方用户开户成功后的返回用户设置登录mt4密码|

```
{
    "is_succ":true,
    "error_msg":"",
    "error_code":0,
    "mt4_id":"500792"
}
```


#### <span id = "signup_v3">1.1.开户</span>
* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/signup_v3
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/signup_v3
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:signup_v3|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方user_id|
|phone|int|是|第三方用户手机号码|
|id_no|string|是|第三方身份证号码|
|username|string|是|第三方用户真实姓名|
|password|string|是|第三方用户用户登录mt4密码|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0||获取成功|
|101| |传递参数错误|
|102| |手机号码不正确|
|104| |生成mt4失败|
|105| |获取不到第三方用户信息|
|109| |第三方user_id已经绑定过老虎账户|
|303| |验证失败|
|117| |身份证号码第三方用户名称不能为空|
|210| |密码不能少于6位，必须由数字和字母组成|
|mt4_id|string|第三方用户开户成功后的返回老虎帐号mt4_id|
|password|string|第三方用户开户成功后的返回用户设置登录mt4密码|

```
{
    "is_succ":true,
    "error_msg":"",
    "error_code":0,
    "mt4_id":"500792",
    "password":"xxxx"
}
```



#### <span id = "get_master_group">2.获取跟随高手当前订单分组</span> 

* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/get_master_group
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_master_group
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_master_group|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方user_id|
|mt4_id|int|是|老虎开户mt4_id|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |请求成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息或者老虎账户信息|
|303| |签名验证失败|
|data|array|返回的详细信息|
|username|string|高手名称|
|usercode|string|高手usercode|
|occupy_asset|string|占用保证金|
|profit|string|收益|
|profit_rate|string|收益率(百分比)|
|copy_asset|double|复制金额|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":[
        {
            "usercode":"10207",
            "username":"高手菊二",
            "occupy_asset":"0.00",
            "profit":"0.00",
            "copy_asset":0,
            "profit_rate":"0.00"
        }
    ]
}
```

#### <span id = "get_master_order_info">3.获取用户跟随单个高手持仓明细</span> 

* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/get_master_order_info
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_master_order_info
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_master_order_info|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|from_id|int|是|老虎高手user_code|
|page|int|是|分页|
|pagesize|int|是|取多少条|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true/false|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |请求成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息或者老虎账户信息|
|303| |安全验证失败|
|num|int|总条数|
|data|array|返回的详细信息|
|order_id|int|订单id|
|occupy_asset|string|占用保证金|
|profit|string|收益|
|profit_rate|string|收益率(百分比)|
|symbol|string|品种名称|
|username|string|高手名称|
|usercode|string|高手usercode|
|open_price|double|开仓价格|
|close_price|double|平仓价格|
|volume|float|交易手数，不需要前端再做乘以0.01转换|
|action|int|交易类型 0做多 1做空|
|open_time|date|开仓时间|

返回成功json:
```
{
    "is_succ":true,
    "error_msg":"",
    "error_code":0,
    "num":1218,
    "data":[
        {
            "username":"Sandy",
            "usercode":"3303",
            "action":0,
            "open_price":1.12623,
            "close_price":1.12376,
            "symbol":"EURUSD",
            "volume":0.02,
            "profit":"-4.40",
            "order_id":997768,
            "open_time":"2015-06-04 09:09:00",
            "occupy_asset":"20.00",
            "profit_rate":"-22.00"
        }
    ]
}
```

#### <span id = "get_master_history_group"> 4.获取跟随高手历史订单分组</span>

* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/get_master_history_group
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_master_history_group
```
* 类型:HTTPS post 
* 参数:JSON String 
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_master_history_group|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|number|是|第三方user_id|
|mt4_id|number|是|老虎mt4_id|

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
|amount|string|跟随金额|
|username|string|高手名称|
|usercode|string|高手usercode|
|profit|string|收益|
|volume|float|交易手数，不需要前端再做乘以0.01转换|
|avatar_path|string|高手图片|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":[
        {
            "amount":"0",
            "username":"高手菊二",
            "usercode":"10207",
            "profit":"-270.01",
            "volume":4.85,
            "avatar_path":"https://demo.tigerwit.com/avatar/10207_150.jpg"
        }
    ]
}
```


#### <span id = "get_master_history_info">5.获取用户跟随单个高手持仓明细</span> 

* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/get_master_history_info
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_master_history_info
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_master_history_info|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|from_id|int|是|跟随高手usercode|
|page|int|是|分页|
|pagesize|int|是|取多少条|

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
|num|int|总条数|
|data|array|返回的详细信息|
|order_id|int|订单id|
|profit|string|收益|
|symbol|string|品种名称|
|symbol_cn|string|交易品种中文名称|
|username|string|高手名称|
|usercode|string|高手usercode|
|open_price|double|开仓价格|
|close_price|double|平仓价格|
|volume|float|交易手数，不需要前端再做乘以0.01转换|
|action|int|交易类型 0做多 1做空|
|profit_rate|string|每单收益率|
|close_type|int|平仓类型 手动平仓：0，止损：1，止盈：2，强制：3，复制跟单：4|
|close_time|date|平仓时间|

返回成功json:
```
{
    "is_succ":true,
    "error_msg":"",
    "error_code":0,
    "num":2,
    "data":[
        {
            "close_type":0,
            "profit_rate":"-21.40",
            "username":"Sandy",
            "usercode":"3303",
            "action":1,
            "open_price":2.02384,
            "close_price":2.02526,
            "symbol":"GBPCAD",
            "volume":0.01,
            "profit":"-1.07",
            "order_id":337277,
            "close_time":"2015-11-17 18:40:13"
        },
        {
            "close_type":0,
            "profit_rate":"35.20",
            "username":"Sandy",
            "usercode":"3303",
            "action":1,
            "open_price":2.14105,
            "close_price":2.13858,
            "symbol":"GBPAUD",
            "volume":0.01,
            "profit":"1.76",
            "order_id":337267,
            "close_time":"2015-11-17 15:30:36"
        }
    ]
}
```

#### <span id = "documentary_order"> 6.获取跟单的持仓订单</span>
接口说明:
如果用户有跟随高手，他跟高手的订单关系不会马上生成，会有10到30秒的延迟时间。需用到该接口的ticket（订单）参数去跟  【[外汇持仓接口](#foreign_order)】 匹配找到它们的跟单关系。

* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/documentary_order
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/documentary_order
```
* 类型:HTTPS post 
* 参数:JSON String 
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:documentary_order|
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
| ticket |int|订单号 |
| usercode |string|高手码|
| username | string |高手名称|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":[
        {
            "ticket":2330,
            "usercode":"1655",
            "username":"wumo"
        }
    ]
}
```


#### <span id = "foreign_order"> 7.外汇持仓接口</span>
接口说明:
外汇持仓接口是获取用户开仓后所有的实时订单接口，不包括跟单关系，需要用到该接口的ticket（订单）参数去跟【[获取跟单的持仓订单](#documentary_order)】 匹配找到它们的跟单关系。
比如：
该接口的ticket=850037和【获取跟单的持仓订单】接口里面的ticket=850037则表示该订单是跟单订单。

* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/foreign_order
```
* 线上请求URL:
``` 
https://api.tigerwit.com/action/public/api/foreign_order
```
* 类型:HTTPS post 
* 参数:JSON String 
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:foreign_order|
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
|400| |MT4系统问题|
|data|array|返回的详细信息|
| ticket |int|订单号 |
| open_price | string |开仓价|
| close_price | string |开仓时候的平仓价格|
| symbol_en |string|交易品种英文|
| symbol_cn | string |交易品种中文|
| action |int|交易类型 [0=>'买', 1=>'卖', 2=>'挂单买入', 3=>'挂单卖出', 4=>'挂单追涨', 5=>'挂单追空']|
| occupy_asset | double |占用保证金,不需要转换成美元，已经是美元|
| sl | string |止损|
| tp | string |止盈|
| profit | float |收益|
| volume | float |交易手数，不需要前端再做乘以0.01转换|
| open_time | string |开仓时间|
|swaps|float|过夜费|
|commission|float|手续费|
|margin_rate|double|预付款 与 存款货币 的比率|
|stops_level|double|止盈止损水平|
|multiply|int|10^digits|
|profit_currency|string|盈利公式结果单位|
|profit_rate|float|汇率（不是实时汇率）|

注意：
profit_currency，假设需求是盈利都要转换为美元。若profit_currency为USD，则公式计算结果无需转换；若profit_currency为USDHKD或GBPUSD等等，则需要转换,即为USDHKD或GBPUSD的品种价格算收益。
如果不想通过profit_currency参数转换，可以通过profit_rate参数直接转换 profit = profit_rate * profit 则是最终美元盈利。
第一次拿到持仓单的profit就是美金不用再转换，实时算的时候profit是通过盈利公式算出来后转换美金就要乘以profit_rate。

返回成功json: 以接口返回结果为准。
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":[
        {
            "ticket":850037,
            "symbol_en":"AUDCAD50",
            "symbol_cn":"澳元加元",
            "action":1,
            "occupy_asset":20,
            "sl":"0.00000",
            "tp":"0.00000",
            "open_price":"0.95558",
            "close_price":"0.95594",
            "profit":-0.29,
            "volume":0.01,
            "open_time":"2016-04-28 05:53:33",
            "swaps":0,
            "commission":-10,
            "margin_rate":1,
            "stops_level":10,
            "multiply":100,
            "profit_currency":"USDHKD"
        }
    ]
}
```

#### <span id = "foreign_exchange_account"> 8.外汇账户汇总接口</span>

* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/foreign_exchange_account
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/foreign_exchange_account
```
* 类型:HTTPS post 
* 参数:JSON String 
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法: foreign_exchange_account |
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
|400| |MT4系统问题|
|data|object|返回的详细信息|
| margin |double|已用预付款 |
| margin_free |float|可用预付款|
| margin_level | float |预付款比例|
| equity |float|净值|
| balance | float |余额包括信用|
| balance_not_include_credit | float |余额不包括信用|
| credit | float |信用|

说明：
第一次读取接口数据：
>浮动盈亏 = 净值 - 余额 - 信用（equity-balance_not_include_credit）或（equity-balance-credit)
占用保证金 = 已用预付款(margin)
可用资金 = 可用预付款(margin_free)
净资产 = 净值(equity)

后面自己计算:
>浮动盈亏 = 所有持仓订单浮动盈亏总和
占用保证金 = 所有持仓订单保证总和（保证金是不变的没有新订单不用再自己算）
净值 = 余额（balance_not_include_credit） + 信用 + 浮动盈亏
可用资产 = 余额（balance_not_include_credit） + 信用 + 浮动盈亏 - 占用保证金 


返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":{
        "margin":10,
        "margin_free":331259.96,
        "margin_level":3312699.6,
        "equity":331269.96,
        "balance":331272.79,
        "balance_not_include_credit":234234234,
        "credit":12312
    }
}
```

#### <span id = "get_trade_record"> 9.获取用户所有历史交易记录</span>

* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/get_trade_record
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_trade_record
```
* 类型:HTTPS post 
* 参数:JSON String 
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法: get_trade_record |
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|page|int|是|分页|
|pagesize|int|是|取多少条|

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
|num|int|总条数|
|data|array|返回的详细信息|
| master_name |string|高手名称 不是跟单 为null|
| is_from |int|是否跟单 0 不是 1跟单|
| action |int|交易类型 [0=>'买', 1=>'卖']|
| close_type |int|平仓类型 [0=>手动平仓, 1=>止损平仓, 2=>止盈平仓, 3=>强制平仓, 4=>复制跟单]|
| ticket |int|订单号|
| symbol_en |string|交易品种 英文|
| symbol_cn |string|交易品种 中文|
| open_price |string|开仓价格|
| close_price |string|平仓价格|
| profit |string|收益|
| volume |float|交易手数，不需要前端再做乘以0.01转换|
| close_time |string|平仓时间|
| open_time |string|开仓时间|
| commission |float|手续费|
| swaps |float|库存费|
| tp |double|止盈|
| sl |double|止损|
| occupy_asset |float|占用保证金|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "num":198,
    "data":[
        {
            "master_name":null,
            "is_from":0,
            "action":1,
            "ticket":587953,
            "symbol_en":"HK50",
            "symbol_cn":"恒生指数",
            "open_price":"24375.00",
            "close_price":"24390.00",
            "profit":"-19.31",
            "volume":1,
            "close_type":0,
            "close_time":"2017-03-27 05:35:28",
            "open_time":"2017-03-17 07:01:15",
            "commission":-12.88,
            "swaps":-10.03,
            "sl":0,
            "tp":0,
            "occupy_asset":313.96
        }
    ]
}
```


#### <span id = "get_payment_record"> 10.充值记录</span>

* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/get_payment_record
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_payment_record
```
* 类型:HTTPS post 
* 参数:JSON String 
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法: get_payment_record|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|page|int|是|页数|
|pagesize|int|是|条数|

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
|num|int|总条数|
|data|array|返回的详细信息|
| status |int|1 有记录 2 有请求链接生成的记录 3 支付接入商返回失败 4 确认支付成功 5 开户赠金 7信用值 0 无此单 -1 已提交 -2 已撤销 -3 处理中 -4 拒绝出金 -5 出金处理完毕  |
| direction |int|1入金 -1出金|
| rmb_amount | float |出入金[人民币]|
| usd_amount |float|出入金[美元]|
| parity | double |出入金汇率|
| time | string |出入金时间|

注意:
判断出金或者入金根据 direction=1 是入金 direction=-1 是出金。
status为负数则是对应direction=-1出金的状态，入金则反之。

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "num":12,
    "data":[
        {
            "direction":1,
            "time":"2016-03-14 09:49:24",
            "rmb_amount":6660,
            "usd_amount":1061.93,
            "parity":6.2716,
            "status":4
        }
    ]
}
```

#### <span id = "check_mt4"> 11.检查mt4_id、密码是否正确</span>

* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/check_mt4
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/check_mt4
```
* 类型:HTTPS post 
* 参数:JSON String 
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法: check_mt4|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|password|string|是|密码|


返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |验证成功|
|1| |验证失败|
|101| |传递参数错误|
|105| |获取不到第三方用户信息或者老虎账户信息|
|303| |安全验证失败|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"成功",
    "is_succ":true
}
```

#### <span id = "change_password"> 12.修改mt4密码</span>

* 测试请求URL:
```
https://demo.tigerwit.com/action/public/api/change_password
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/change_password
```
* 类型:HTTPS post 
* 参数:JSON String 
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法: change_password|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|password|string|是|密码|


返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |修改成功|
|1| |修改失败|
|101| |传递参数错误|
|105| |获取不到第三方用户信息或者老虎账户信息|
|303| |安全验证失败|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"成功",
    "is_succ":true
}
```

<center> [返回顶部](#top) </center>     
