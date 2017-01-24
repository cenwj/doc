# 老虎外汇文档

#### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html)

============================开户、个人中心============================
* <span id = "signup">开户</span>



#### <span id = "get_master_group">2.获取跟随高手当前订单分组</span> 

* 测试请求URL:http://demo.tigerwit.com/action/public/api/get_master_group
* 线上请求URL:https://api.tigerwit.com/action/public/api/get_master_group
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
|error_msg|string|返回信息|
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

#### <span id = "get_master_history_group"> 3.获取跟随高手历史订单分组</span>

* 测试请求URL:http://demo.tigerwit.com/action/public/api/get_master_history_group
* 线上请求URL:https://api.tigerwit.com/action/public/api/get_master_history_group
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
|error_msg|string|返回信息|
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
|volume|double|交易手数|
|avatar_path|string|高手图片|

json:
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
            "avatar_path":"http://demo.tigerwit.com/avatar/10207_150.jpg"
        }
    ]
}
```

#### <span id = "documentary_order"> 4.获取跟单的持仓订单</span>
接口说明:
如果用户有跟随高手，他跟高手的订单关系不会马上生成，会有10到30秒的延迟时间。需用到该接口的ticket（订单）参数去跟  【[5.外汇持仓接口](#foreign_order)】 匹配找到它们的跟单关系。

* 测试请求URL:http://demo.tigerwit.com/action/public/api/documentary_order
* 线上请求URL:https://api.tigerwit.com/action/public/api/documentary_order
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
|error_msg|string|返回信息|
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


#### <span id = "foreign_order"> 5.外汇持仓接口</span>
接口说明:
外汇持仓接口是获取用户开仓后所有的实时订单接口，不包括跟单关系，需要用到该接口的ticket（订单）参数去跟【[4.获取跟单的持仓订单](#documentary_order)】 匹配找到它们的跟单关系。
比如：
该接口的ticket=850037和【获取跟单的持仓订单】接口里面的ticket=850037则表示该订单是跟单订单。

* 测试请求URL:http://demo.tigerwit.com/action/public/api/foreign_order
* 线上请求URL:https://api.tigerwit.com/action/public/api/foreign_order
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
|error_msg|string|返回信息|
|error_code|int|返回码|
|0| |请求成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息或者老虎账户信息|
|303| |安全验证失败|
|400| |MT4系统问题|
|data|array|返回的详细信息|
| ticket |int|订单号 |
| open_price | string |开仓价|
| close_price | string |平仓价|
| symbol_en |string|交易品种英文|
| symbol_cn | string |交易品种中文|
| action |int|交易类型 [0=>'买', 1=>'卖', 2=>'挂单买入', 3=>'挂单卖出', 4=>'挂单追涨', 5=>'挂单追空']|
| occupy_asset | double |占用保证金|
| sl | string |止损|
| tp | string |止盈|
| profit | float |收益|
| volume | float |交易手数|
| open_time | string |开仓时间|
|swaps|float|过夜费|
|commission|float|手续费|
|margin_rate|double|预付款 与 存款货币 的比率|
|stops_level|double|止盈止损水平|
|multiply|int|10^digits|
|profit_currency|string|盈利公式结果单位|

注意：
profit_currency，假设需求是盈利都要转换为美元。若profit_currency为USD，则公式计算结果无需转换；若profit_currency为USDHKD或GBPUSD等等，则需要转换。

返回成功json:
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

#### <span id = "foreign_exchange_account"> 6.外汇账户汇总接口</span>

* 测试请求URL:http://demo.tigerwit.com/action/public/api/foreign_exchange_account
* 线上请求URL:https://api.tigerwit.com/action/public/api/foreign_exchange_account
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
|error_msg|string|返回信息|
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
| balance | float |结余包括信用|
| balance_not_include_credit | float |结余不包括信用|
| credit | float |信用|

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

#### <span id = "get_trade_record"> 7.获取用户所有交易记录</span>

* 测试请求URL:http://demo.tigerwit.com/action/public/api/get_trade_record
* 线上请求URL:https://api.tigerwit.com/action/public/api/get_trade_record
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
|is_succ|bool|true/false|
|error_msg|string|返回信息|
|error_code|int|返回码|
|0| |请求成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息或者老虎账户信息|
|303| |安全验证失败|
|num|int|总条数|
|data|array|返回的详细信息|
| master_name |string|高手名称 不是跟单 为null|
| is_from |int|是否跟单 0 不是 1跟单|
| action |int|交易类型 [0=>'买', 1=>'卖', 2=>'挂单买入', 3=>'挂单卖出', 4=>'挂单追涨', 5=>'挂单追空']|
| ticket |int|订单号|
| symbol_en |string|交易品种 英文|
| symbol_cn |string|交易品种 中文|
| open_price |string|开仓价格|
| close_price |string|平仓价格|
| profit |string|收益|
| volume |double|交易手数|
| close_type |int|平仓类型 手动平仓：0，止损：1，止盈：2，强制：3，复制跟单：4|
| close_time |string|平仓时间|

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
            "action":0,
            "ticket":817752,
            "symbol_en":"GBPUSD",
            "symbol_cn":"英镑美元",
            "open_price":"1.41390",
            "close_price":"1.41355",
            "profit":"-0.35000",
            "volume":0.01,
            "close_type":0,
            "close_time":"2016-04-15 03:28:03"
        }
    ]
}
```

