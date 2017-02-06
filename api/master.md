# 老虎外汇文档

#### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html)

============================高手============================

#### <span id = "get_master_group">1.获取高手列表</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/get_master_list_v2
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_master_list_v2
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_master_list_v2|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|order|string|no| 排序 收益率传空就是默认收益率排序, min_follow=>最低跟随金额, maxRetract=>最大跌幅, copyHistorySum=>历史复制人数 |
|page|int|yes|页数|
|pagesize|int|yes|条数|

返回参数说明:

|名称|类型|说明|
|:-------------:|:-------------:|:-------------:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码 0 成功 其他失败|
|sum|int|总条数|
|page|int|当前页数|
|data|array|返回信息|
|username|string|高手用户名|
|user_code|string|高手码|
|max_retract|double|最大回撤|
|profit_rate|float|收益率|
|last_week_copy_rate|float|7日变化率|
|history_sum|int|历史复制人数|
|min_copy_amount|float|最少复制金额|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"操作成功",
    "is_succ":true,
    "data":[
        {
            "username":"Jamestock",
            "user_code":"1239872",
            "max_retract":-0.7766,
            "profit_rate":-54.28,
            "last_week_copy_rate":-74.59,
            "history_sum":244,
            "min_copy_amount":500
        },
        {
            "username":"彭泽",
            "user_code":"1220307",
            "max_retract":0,
            "profit_rate":-64.19,
            "last_week_copy_rate":-67.23,
            "history_sum":238,
            "min_copy_amount":1500
        }
    ],
    "sum":68,
    "page":1
}
```

#### <span id = "get_master_info_v2">2.高手的基本信息</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/get_master_info_v2
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/get_master_info_v2
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_master_info_v2|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_code|number|no|高手码|

返回参数说明:

|名称|类型|说明|
|:-------------:|:-------------:|:-------------:|
|is_succ|bool | true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|number|返回码 0 成功 其他失败|
|data| Object |返回信息|
|user_code| string |高手码|
|username| string |高手昵称|
|min_copy_amount| double |最少复制金额|
|history_sum| int |历史复制人数|
|total_profit| float |总收益|
|max_retract| double |最大回撤|
|split_ratio| int |分成比例|
|last_profit_close_rate| float |准确率|
|last_max_volume| float |最大开仓|
|last_total_close| int |总平仓|
|win_count| int |总盈利订单|
|lose_count| int |总亏损订单|
|avg_position_time| string |平均持仓时间|
|win_sell_count| int |成功的做空交易|
|win_buy_count| int |成功的做多交易|
|last_profit_rate| float |上一交易日收益率|
|last_week_profit_rate| float |近7日收益率|
|avg_month_close| int |月平均交易笔数|
|avatar_path| string |高手图片|
|region_cn| Object |返回的地区信息|
|city_name|string|城市名称|
|world_code|string|国家代码|
|world_name|string|国家名称|
|state_name|string|城市名称|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":{
        "user_code":"1320771",
        "username":"虎虎虎虎",
        "min_copy_amount":3000,
        "history_sum":50,
        "total_profit":676.47,
        "max_retract":-0.1023,
        "split_ratio":20,
        "last_profit_close_rate":95.58,
        "last_max_volume":0.5,
        "last_total_close":294,
        "win_count":281,
        "lose_count":13,
        "avg_position_time":"19时07分",
        "win_sell_count":169,
        "win_buy_count":112,
        "last_profit_rate":0,
        "last_week_profit_rate":7.44,
        "avg_month_close":147,
        "avatar_path":"https://www.tigerwit.com/avatar/1320771_150.jpg",
        "region_cn":{
            "city_name":"",
            "world_code":"CN",
            "world_name":"中国",
            "state_name":"北京市"
        }
    }
}
```


#### <span id = "historical_rate">3.高手历史月收益率表现图标</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/historical_rate
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/historical_rate
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:historical_rate|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_code|int|no|高手码|


返回参数说明:

|名称|类型|说明|
|:-------------:|:-------------:|:-------------:|
|is_succ|bool | true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码 0 成功 其他失败|
|data|array|key=>value|
|t|string|日期（年-月）|
|v|float|收益率|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":[
        {
            "t":"2015-10",
            "v":-11.22
        },
        {
            "t":"2015-11",
            "v":37.4
        }
    ]
}
```


#### <span id = "copy_change">4.高手复制者变化图标</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/copy_change
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/copy_change
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:copy_change|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_code|int|是|高手码|

返回参数说明:

|名称|类型|说明|
|:-------------:|:-------------:|:-------------:|
|is_succ|bool | true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码 0 成功 其他失败|
|Last_week_copy_rate|float|近七日复制变化率(百分百)|
|last_max_balance|float|管理资金|
|data|array|key=>value|
|t|string|复制日期|
|v|int|复制人数|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "Last_week_copy_rate":0,
    "last_max_balance":15430.68,
    "data":[
        {
            "t":"2016-01-13",
            "v":1
        },
        {
            "t":"2016-01-21",
            "v":1
        }
    ]
}
```

#### <span id = "monthly_symbols">5.高手月交易品种图标</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/monthly_symbols
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/monthly_symbols
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:monthly_symbols|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_code|int|no|高手码|
|date|string|yes|传递月份 传空为默认为当月 　如2016-09|

返回参数说明:

|名称|类型|说明|
|:-------------:|:-------------:|:-------------:|
|is_succ|bool | true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码 0 成功 其他失败|
|time| string |返回改高手第一次做单时间或者注册时间|
|now_date| string |当前数据时间|
|data| Object |返回信息|
| symbol| string |产品名称|
| ratio| float |产品百分比|
| symbol_cmd_one| int |做空数量|
| symbol_cmd_zore| int |做多数量|
| symbol_cmd_zore_time| int |做多时间秒数|
| symbol_cmd_one_time| int |做空时间秒数|

说明:
**time 参数:**
   >是给第三方对接的时候计算开始月份到当前月份的集合，比如 time为2017-01，当前月份为2017-02，筛选列表为 2017-01，2017-02。

**now_date 参数:**
   >如果传了date参数就是这个date，如果没有传就是当前月份的date。


返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "time":"2015-01",
    "now_date":"2016-08",
    "data":[
        {
            "symbol":"XAUUSD",
            "ratio":86.43,
            "symbol_cmd_one":121,
            "symbol_cmd_zore":102,
            "symbol_cmd_zore_time":11423630,
            "symbol_cmd_one_time":6942930
        },
        {
            "symbol":"GBPUSD",
            "ratio":9.3,
            "symbol_cmd_one":21,
            "symbol_cmd_zore":3,
            "symbol_cmd_zore_time":37226,
            "symbol_cmd_one_time":2009167
        },
        {
            "symbol":"AUDUSD",
            "ratio":3.49,
            "symbol_cmd_one":7,
            "symbol_cmd_zore":2,
            "symbol_cmd_zore_time":215741,
            "symbol_cmd_one_time":1012170
        },
        {
            "symbol":"USDJPY",
            "ratio":0.78,
            "symbol_cmd_one":0,
            "symbol_cmd_zore":2,
            "symbol_cmd_zore_time":99282,
            "symbol_cmd_one_time":0
        }
    ]
}
```