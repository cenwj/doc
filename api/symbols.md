# 老虎外汇文档

#### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](pending.html)

============================交易品种============================

#### <span id = "get_symbols">1.获取交易品种汇总</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/get_symbols
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_symbols
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_symbols|
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
|303| |验证失败|
|data|Object|key=>value|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":[
        {
            "AUDCAD":"澳元加元"
        },
        {
            "AUDCAD50":"澳元加元"
        }
    ]
}
```


#### <span id = "symbol_list_info">2.所有交易品种详情</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/symbol_list_info
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/symbol_list_info
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:symbol_list_info|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|symbol|string|是|交易品种　获取全部传递null|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码|
|0| |请求成功|
|101| |传递参数错误|
|151| |没有找到该交易品种|
|303| |验证失败|
|data|Object|返回信息|
|symbol_en|sting|交易品种[英文]|
|symbol_cn|sting|交易品种[中文]|
|digits|int|小数位数|
|stops_level|int|止损水平|
|gtc_pendings|int|直到取消挂单|
|0| |当日有效（包括止损止盈）|
|1| |一直有效（直至客户取消）|
|2| |当日有效（不包括止损止盈）|
|contract_size|double|合约数量|
|profit_mode|int|利润计算|
|0| |外汇|
|1| |差价合约|
|2| |期货|
|swap_type|int|库存费类型|
|3||USD(具体的数据 比如$1.11)|
|2||百分比(具体的百分多少)|
|swap_long|double|买入库存费|
|swap_short|double|卖出库存费|
|margin_mode|int|预付款计算|
|0| |外汇|
|1| |差价合约|
|2| |期货|
|3| |指数差价合约|
|4| |差价合约 - 放大比率|
|margin_hedged|double|预付款对冲|
|margin_initial|double|初始保证金|
|margin_divider|double|百分比 ［保证金计算中的percentage = 100 / margin_divider] |
|currency|string|流通货币|
|margin_currency|string|保证金货币|
 
说明:
>流通货币是Currency - 则盈亏公式计算出来的也是Currency - 盈亏显示需要转换成USD
保证金货币是Margin Currency - 则保证金公式计算出来的也是Margin Currency - 占用保证金显示需要转换成USD

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":[
        {
            "symbol_en":"AUDCAD",
            "symbol_cn":"澳元加元",
            "digits":5,
            "stops_level":100,
            "gtc_pendings":1,
            "contract_size":100000,
            "profit_mode":0,
            "swap_type":3,
            "swap_long":1.4,
            "swap_short":-3.3,
            "margin_mode":0,
            "margin_hedged":100000,
            "margin_initial":0,
            "margin_divider":1,
            "currency":"AUD",
            "margin_currency":"USD"
        },
        {
            "symbol_en":"AUDCAD50",
            "symbol_cn":"澳元加元",
            "digits":5,
            "stops_level":100,
            "gtc_pendings":1,
            "contract_size":100000,
            "profit_mode":0,
            "swap_type":3,
            "swap_long":1.4,
            "swap_short":-3.3,
            "margin_mode":0,
            "margin_hedged":100000,
            "margin_initial":0,
            "margin_divider":0.5,
            "currency":"AUD",
            "margin_currency":"USD"
        }
    ]
}
```


#### <span id = "history_day_info">3.获取单个品种、开收盘信息</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/history_day_info
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/history_day_info
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:history_day_info|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|symbols|string|是|交易品种|

返回参数说明:

|名称|类型|说明|
|:-------------:|:-------------:|:-------------:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码 0 成功 其他失败|
|data| Object |返回信息 key:value|

说明:
```

ctm:类型 int 今天开盘时间
today_open_price:类型 string 今天开盘价
today_low:类型 string 今天开盘最低价
today_high:类型 string 今天开盘最高价
yesterday_close_price:类型 string 昨天收盘价
```

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":{
        "AUDCAD":{
            "ctm":1484611200,
            "today_open_price":"0.98519",
            "today_high":"0.98519",
            "today_low":"0.98519",
            "yesterday_close_price":"0.98528"
        }
    }
}
```


#### <span id = "yesterday_close_price">4.获取多个品种、昨日收盘价格【有缓存】</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/yesterday_close_price
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/yesterday_close_price
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法: yesterday_close_price |
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|symbols|string|是|交易品种，多个品种以逗号分隔 |

返回参数说明:

|名称|类型|说明|
|:-------------:|:-------------:|:-------------:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码 0 成功 其他失败|
|data| Object |返回信息 key:value|

说明:
```

ctm:类型 int 今天开盘时间
yesterday_close_price:类型 string 昨天收盘价
```

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":{
        "AUDCAD":{
            "ctm":1484697600,
            "yesterday_close_price":"0.98720"
        },
        "AUDCHF":{
            "ctm":1484697600,
            "yesterday_close_price":"0.75793"
        }
    }
}
```


#### <span id = "get_symbols_history">5.历史报价</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/get_symbols_history
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_symbols_history
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_symbols_history|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|symbol|string|是|交易品种|
|limit|int|是|取多少条,不能少于2条|
|stop_time|string|是|结束时间|
|type|int|是|1=>1分钟 5=>5分钟 15=>15分钟 30=>30分钟 60=>1个小时 240=>4个小时 1440=>1天 10080=>1个礼拜 43200=>1个月份|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true/false|
|error_msg|string|返回信息|
|error_code|number|返回码|
|0| |获取成功|
|101| |传递参数错误|
|105| |获取不到第三方用户信息|
|127| |传递类型不合法|
|128| |没有该交易品种|
|129| |开始时间和结束时间不能为空|
|303| |验证失败|
|data|Object|返回信息|
|time|string|时间|
|open_price|double|开仓价格|
|high|double|最高价|
|low|double|最低价|
|close|double|收盘价|
|vol|float|交易手数|

返回成功json:
```
{
    "is_succ":true,
    "error_msg":"请求成功",
    "error_code":0,
    "data":[
        {
            "time":"2016-02-22 01:04:00",
            "open_price":1.11127,
            "high":1.11173,
            "low":1.11127,
            "close":1.11171,
            "vol":0.09
        },
        {
            "time":"2016-02-20 00:55:00",
            "open_price":1.11318,
            "high":1.11318,
            "low":1.11308,
            "close":1.11308,
            "vol":0.06
        }
    ]
}
```

