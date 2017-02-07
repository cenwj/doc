# 老虎外汇文档

#### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html)

========================开仓、平仓、挂单=========================

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
|volume|float|是|开仓手数|
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
|volume|float|交易手数|
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
|volume|int|平仓手数|
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



