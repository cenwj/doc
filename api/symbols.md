# 老虎外汇文档

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html) 

## 接口分类 
### 交易品种

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
|min_volume|float|最低交易手数|
|margin_cal_currency|string| 保证金公式结果是否需要汇率转换及需要汇率转换的货币对 |
|profit_cal_currency|string| 盈亏公式结果是否需要汇率转换及需要汇率转换的货币对 |

说明:
>更新：
为了方便货币转换，增加了两个字段：margin_cal_currency，profit_cal_currency,而不用再看currency，margin_currency字段。
如果是返回值是USD则不需要转换汇率，不是USD则拿margin_cal_currency，profit_cal_currency的货币对去获取报价转换汇率具体查看 [【保证金计算】](/ouccupy_asset.html) 【D】货币换算。

返回成功json:
```
{"error_code":0,"error_msg":"","is_succ":true,"data":[{"symbol_en":"AUDCAD","symbol_cn":"澳元加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.4,"swap_short":-3.3,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"AUDCAD50","symbol_cn":"澳元加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.4,"swap_short":-3.3,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"AUDCAD200","symbol_cn":"澳元加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.4,"swap_short":-3.3,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"AUDCHF","symbol_cn":"澳元瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":4.8,"swap_short":-7.2,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"AUDCHF50","symbol_cn":"澳元瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":4.8,"swap_short":-7.2,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"AUDCHF200","symbol_cn":"澳元瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":4.8,"swap_short":-7.2,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"AUDJPY","symbol_cn":"澳元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":3.3,"swap_short":-5.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"AUDJPY50","symbol_cn":"澳元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":3.3,"swap_short":-5.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"AUDJPY200","symbol_cn":"澳元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":3.3,"swap_short":-5.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"AUDNZD","symbol_cn":"澳元新西兰元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-4.4,"swap_short":2.6,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"NZDUSD"},{"symbol_en":"AUDNZD50","symbol_cn":"澳元新西兰元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-4.4,"swap_short":2.6,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"NZDUSD"},{"symbol_en":"AUDNZD200","symbol_cn":"澳元新西兰元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-4.4,"swap_short":2.6,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"NZDUSD"},{"symbol_en":"AUDUSD","symbol_cn":"澳元美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":2.7,"swap_short":-4.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"AUDUSD50","symbol_cn":"澳元美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":2.7,"swap_short":-4.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"AUDUSD200","symbol_cn":"澳元美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":2.7,"swap_short":-4.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"AUD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"CADCHF","symbol_cn":"加元瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":2.6,"swap_short":-5,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"CAD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"CADCHF50","symbol_cn":"加元瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":2.6,"swap_short":-5,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"CAD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"CADCHF200","symbol_cn":"加元瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":2.6,"swap_short":-5,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"CAD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"CADJPY","symbol_cn":"加元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.1,"swap_short":-3.1,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"CAD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"CADJPY50","symbol_cn":"加元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.1,"swap_short":-3.1,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"CAD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"CADJPY200","symbol_cn":"加元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.1,"swap_short":-3.1,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"CAD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"CHFJPY","symbol_cn":"瑞郎日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-3.4,"swap_short":1.2,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"CHF","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"CHFJPY50","symbol_cn":"瑞郎日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-3.4,"swap_short":1.2,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"CHF","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"CHFJPY200","symbol_cn":"瑞郎日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-3.4,"swap_short":1.2,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"CHF","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"EURAUD","symbol_cn":"欧元澳元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-7.8,"swap_short":5.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"AUDUSD"},{"symbol_en":"EURAUD50","symbol_cn":"欧元澳元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-7.8,"swap_short":5.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"AUDUSD"},{"symbol_en":"EURAUD200","symbol_cn":"欧元澳元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-7.8,"swap_short":5.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"AUDUSD"},{"symbol_en":"EURCAD","symbol_cn":"欧元加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-4.3,"swap_short":2.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"EURCAD50","symbol_cn":"欧元加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-4.3,"swap_short":2.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"EURCAD200","symbol_cn":"欧元加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-4.3,"swap_short":2.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"EURCHF","symbol_cn":"欧元瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":0.7,"swap_short":-3.1,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"EURCHF50","symbol_cn":"欧元瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":0.7,"swap_short":-3.1,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"EURCHF200","symbol_cn":"欧元瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":0.7,"swap_short":-3.1,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"EURGBP","symbol_cn":"欧元英镑","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-3.9,"swap_short":0.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"GBPUSD"},{"symbol_en":"EURGBP50","symbol_cn":"欧元英镑","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-3.9,"swap_short":0.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"GBPUSD"},{"symbol_en":"EURGBP200","symbol_cn":"欧元英镑","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-3.9,"swap_short":0.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"GBPUSD"},{"symbol_en":"EURJPY","symbol_cn":"欧元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-1.6,"swap_short":-0.6,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"EURJPY50","symbol_cn":"欧元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-1.6,"swap_short":-0.6,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"EURJPY200","symbol_cn":"欧元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-1.6,"swap_short":-0.6,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"EURNZD","symbol_cn":"欧元新西兰元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-14,"swap_short":11,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"NZDUSD"},{"symbol_en":"EURNZD50","symbol_cn":"欧元新西兰元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-14,"swap_short":11,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"NZDUSD"},{"symbol_en":"EURNZD200","symbol_cn":"欧元新西兰元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-14,"swap_short":11,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"NZDUSD"},{"symbol_en":"EURUSD","symbol_cn":"欧元美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-1.9,"swap_short":0.6,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"EURUSD50","symbol_cn":"欧元美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-1.9,"swap_short":0.6,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"EURUSD200","symbol_cn":"欧元美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-1.9,"swap_short":0.6,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"EUR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"GBPAUD","symbol_cn":"英镑澳元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-7.4,"swap_short":5.5,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"AUDUSD"},{"symbol_en":"GBPAUD50","symbol_cn":"英镑澳元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-7.4,"swap_short":5.5,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"AUDUSD"},{"symbol_en":"GBPAUD200","symbol_cn":"英镑澳元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-7.4,"swap_short":5.5,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"AUDUSD"},{"symbol_en":"GBPCAD","symbol_cn":"英镑加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-2.7,"swap_short":0.7,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"GBPCAD50","symbol_cn":"英镑加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-2.7,"swap_short":0.7,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"GBPCAD200","symbol_cn":"英镑加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-2.7,"swap_short":0.7,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"GBPCHF","symbol_cn":"英镑瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":4.3,"swap_short":-6.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"GBPCHF50","symbol_cn":"英镑瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":4.3,"swap_short":-6.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"GBPCHF200","symbol_cn":"英镑瑞郎","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":4.3,"swap_short":-6.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"GBPJPY","symbol_cn":"英镑日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.1,"swap_short":-3.5,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"GBPJPY50","symbol_cn":"英镑日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.1,"swap_short":-3.5,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"GBPJPY200","symbol_cn":"英镑日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.1,"swap_short":-3.5,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"GBPNZD","symbol_cn":"英镑新西兰元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-14.9,"swap_short":12.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"NZDUSD"},{"symbol_en":"GBPNZD50","symbol_cn":"英镑新西兰元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-14.9,"swap_short":12.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"NZDUSD"},{"symbol_en":"GBPNZD200","symbol_cn":"英镑新西兰元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-14.9,"swap_short":12.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"NZDUSD"},{"symbol_en":"GBPUSD","symbol_cn":"英镑美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":0.6,"swap_short":-1.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"GBPUSD50","symbol_cn":"英镑美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":0.6,"swap_short":-1.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"GBPUSD200","symbol_cn":"英镑美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-0.6,"swap_short":-1.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"GBP","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"NZDCAD","symbol_cn":"新西兰元加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":4.4,"swap_short":-6.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"NZD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"NZDCAD50","symbol_cn":"新西兰元加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":4.3,"swap_short":-6.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"NZD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"NZDCAD200","symbol_cn":"新西兰元加元","digits":5,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":4.3,"swap_short":-6.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"NZD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"NZDJPY","symbol_cn":"新西兰元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":6,"swap_short":-8.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"NZD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"NZDJPY50","symbol_cn":"新西兰元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":6,"swap_short":-8.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"NZD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"NZDJPY200","symbol_cn":"新西兰元日元","digits":3,"stops_level":100,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":6,"swap_short":-8.4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"NZD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"NZDUSD","symbol_cn":"新西兰元美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":5.4,"swap_short":-7.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"NZD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"NZDUSD50","symbol_cn":"新西兰元美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":5.4,"swap_short":-7.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"NZD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"NZDUSD200","symbol_cn":"新西兰元美元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":5.4,"swap_short":-7.9,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"NZD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"USDCAD","symbol_cn":"美元加元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-2.7,"swap_short":0.8,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"USDCAD50","symbol_cn":"美元加元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-2.7,"swap_short":0.8,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"USDCAD200","symbol_cn":"美元加元","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":-2.7,"swap_short":0.8,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCAD"},{"symbol_en":"USDCHF","symbol_cn":"美元瑞郎","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.6,"swap_short":-4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"USDCHF50","symbol_cn":"美元瑞郎","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.6,"swap_short":-4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"USDCHF200","symbol_cn":"美元瑞郎","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":1.6,"swap_short":-4,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCHF"},{"symbol_en":"USDJPY","symbol_cn":"美元日元","digits":3,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":0.1,"swap_short":-1.3,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"USDJPY50","symbol_cn":"美元日元","digits":3,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":0.1,"swap_short":-1.3,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"USDJPY200","symbol_cn":"美元日元","digits":3,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":3,"swap_long":0.1,"swap_short":-1.3,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDJPY"},{"symbol_en":"USDCNH","symbol_cn":"美元人民币","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":0,"swap_long":0,"swap_short":0,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":1,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCNH"},{"symbol_en":"USDCNH50","symbol_cn":"美元人民币","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":0,"swap_long":0,"swap_short":0,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":0.5,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCNH"},{"symbol_en":"USDCNH200","symbol_cn":"美元人民币","digits":5,"stops_level":50,"gtc_pendings":1,"contract_size":100000,"profit_mode":0,"swap_type":0,"swap_long":0,"swap_short":0,"margin_mode":0,"margin_hedged":100000,"margin_initial":0,"margin_divider":2,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USDCNH"},{"symbol_en":"XAGUSD","symbol_cn":"白银","digits":4,"stops_level":150,"gtc_pendings":1,"contract_size":5000,"profit_mode":0,"swap_type":3,"swap_long":-1.4,"swap_short":-1,"margin_mode":2,"margin_hedged":1000,"margin_initial":1000,"margin_divider":1,"currency":"XAG","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"XAGUSD50","symbol_cn":"白银","digits":4,"stops_level":150,"gtc_pendings":1,"contract_size":5000,"profit_mode":0,"swap_type":3,"swap_long":-1.4,"swap_short":-1,"margin_mode":2,"margin_hedged":2000,"margin_initial":2000,"margin_divider":1,"currency":"XAG","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"XAGUSD200","symbol_cn":"白银","digits":4,"stops_level":150,"gtc_pendings":1,"contract_size":5000,"profit_mode":0,"swap_type":3,"swap_long":-1.4,"swap_short":-1,"margin_mode":2,"margin_hedged":500,"margin_initial":500,"margin_divider":1,"currency":"XAG","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"XAUUSD","symbol_cn":"黄金","digits":2,"stops_level":150,"gtc_pendings":1,"contract_size":100,"profit_mode":0,"swap_type":3,"swap_long":-1.7,"swap_short":-0.3,"margin_mode":2,"margin_hedged":1000,"margin_initial":1000,"margin_divider":1,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"XAUUSD50","symbol_cn":"黄金","digits":2,"stops_level":150,"gtc_pendings":1,"contract_size":100,"profit_mode":0,"swap_type":3,"swap_long":-1.7,"swap_short":-0.3,"margin_mode":2,"margin_hedged":2000,"margin_initial":2000,"margin_divider":1,"currency":"USD","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"XAUUSD200","symbol_cn":"黄金","digits":2,"stops_level":150,"gtc_pendings":1,"contract_size":100,"profit_mode":0,"swap_type":3,"swap_long":-1.7,"swap_short":-0.3,"margin_mode":2,"margin_hedged":500,"margin_initial":500,"margin_divider":1,"currency":"XAU","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"XNGUSD","symbol_cn":"天然气","digits":4,"stops_level":15,"gtc_pendings":1,"contract_size":10000,"profit_mode":0,"swap_type":2,"swap_long":-33.3,"swap_short":-10.1,"margin_mode":2,"margin_hedged":1000,"margin_initial":1000,"margin_divider":1,"currency":"XNG","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"XBRUSD","symbol_cn":"布伦特原油","digits":3,"stops_level":15,"gtc_pendings":1,"contract_size":1000,"profit_mode":0,"swap_type":3,"swap_long":-15,"swap_short":5.1,"margin_mode":2,"margin_hedged":1000,"margin_initial":1000,"margin_divider":1,"currency":"XBR","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"XTIUSD","symbol_cn":"西德州原油","digits":3,"stops_level":15,"gtc_pendings":1,"contract_size":1000,"profit_mode":0,"swap_type":3,"swap_long":-33.3,"swap_short":-10.1,"margin_mode":2,"margin_hedged":1000,"margin_initial":1000,"margin_divider":1,"currency":"XTI","margin_currency":"USD","min_volume":0.01,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"AUS200","symbol_cn":"澳洲股指","digits":2,"stops_level":20,"gtc_pendings":1,"contract_size":1,"profit_mode":1,"swap_type":3,"swap_long":-5.85,"swap_short":-1.15,"margin_mode":4,"margin_hedged":1,"margin_initial":0,"margin_divider":1,"currency":"AUD","margin_currency":"USD","min_volume":1,"margin_cal_currency":"USD","profit_cal_currency":"AUDUSD"},{"symbol_en":"EUSTX50","symbol_cn":"欧元区股指","digits":2,"stops_level":20,"gtc_pendings":1,"contract_size":1,"profit_mode":1,"swap_type":3,"swap_long":-5.85,"swap_short":-1.15,"margin_mode":4,"margin_hedged":0,"margin_initial":0,"margin_divider":1,"currency":"EUR","margin_currency":"USD","min_volume":1,"margin_cal_currency":"USD","profit_cal_currency":"EURUSD"},{"symbol_en":"GER30","symbol_cn":"德国股指","digits":2,"stops_level":20,"gtc_pendings":1,"contract_size":1,"profit_mode":1,"swap_type":2,"swap_long":-5.85,"swap_short":-1.15,"margin_mode":4,"margin_hedged":1,"margin_initial":0,"margin_divider":1,"currency":"EUR","margin_currency":"USD","min_volume":1,"margin_cal_currency":"USD","profit_cal_currency":"EURUSD"},{"symbol_en":"JPN225","symbol_cn":"日本股指","digits":2,"stops_level":20,"gtc_pendings":1,"contract_size":100,"profit_mode":1,"swap_type":2,"swap_long":-5.85,"swap_short":-1.15,"margin_mode":4,"margin_hedged":1,"margin_initial":0,"margin_divider":1,"currency":"JPY","margin_currency":"JPY","min_volume":1,"margin_cal_currency":"USDJPY","profit_cal_currency":"USDJPY"},{"symbol_en":"SPA35","symbol_cn":"西班牙股指","digits":2,"stops_level":20,"gtc_pendings":1,"contract_size":1,"profit_mode":1,"swap_type":2,"swap_long":-5.85,"swap_short":-1.15,"margin_mode":4,"margin_hedged":1,"margin_initial":0,"margin_divider":1,"currency":"EUR","margin_currency":"USD","min_volume":1,"margin_cal_currency":"USD","profit_cal_currency":"EURUSD"},{"symbol_en":"NAS100","symbol_cn":"纳斯达克 100","digits":2,"stops_level":20,"gtc_pendings":1,"contract_size":1,"profit_mode":1,"swap_type":2,"swap_long":-5.85,"swap_short":-1.15,"margin_mode":4,"margin_hedged":1,"margin_initial":0,"margin_divider":1,"currency":"USD","margin_currency":"USD","min_volume":1,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"UK100","symbol_cn":"英国富时 100","digits":2,"stops_level":20,"gtc_pendings":1,"contract_size":1,"profit_mode":1,"swap_type":2,"swap_long":-5.85,"swap_short":-1.15,"margin_mode":4,"margin_hedged":1,"margin_initial":0,"margin_divider":1,"currency":"GBP","margin_currency":"USD","min_volume":1,"margin_cal_currency":"USD","profit_cal_currency":"GBPUSD"},{"symbol_en":"US30","symbol_cn":"道琼斯工业指数","digits":2,"stops_level":10,"gtc_pendings":1,"contract_size":1,"profit_mode":1,"swap_type":0,"swap_long":-5.85,"swap_short":-1.15,"margin_mode":4,"margin_hedged":1,"margin_initial":0,"margin_divider":1,"currency":"USD","margin_currency":"USD","min_volume":1,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"FRA40","symbol_cn":"法国股指","digits":2,"stops_level":20,"gtc_pendings":1,"contract_size":1,"profit_mode":1,"swap_type":2,"swap_long":-5.85,"swap_short":-1.15,"margin_mode":4,"margin_hedged":1,"margin_initial":0,"margin_divider":1,"currency":"EUR","margin_currency":"USD","min_volume":1,"margin_cal_currency":"USD","profit_cal_currency":"EURUSD"},{"symbol_en":"USA500","symbol_cn":"标普 500","digits":2,"stops_level":10,"gtc_pendings":1,"contract_size":1,"profit_mode":1,"swap_type":2,"swap_long":-5.85,"swap_short":-1.15,"margin_mode":4,"margin_hedged":1,"margin_initial":0,"margin_divider":1,"currency":"USD","margin_currency":"USD","min_volume":1,"margin_cal_currency":"USD","profit_cal_currency":"USD"},{"symbol_en":"HK50","symbol_cn":"恒生指数","digits":2,"stops_level":10,"gtc_pendings":1,"contract_size":10,"profit_mode":1,"swap_type":2,"swap_long":-5.85,"swap_short":-1.15,"margin_mode":4,"margin_hedged":1,"margin_initial":0,"margin_divider":1,"currency":"HKD","margin_currency":"HKD","min_volume":1,"margin_cal_currency":"USDHKD","profit_cal_currency":"USDHKD"}]}
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
week_high:类型 string 上周最高价 
week_low:类型 string 上周最低价 
month_high:类型 string 上月最高价  
month_low:类型 string 上月最低价   
year_high:类型 string 上年最高价    
year_low:类型 string 上年最低价    
```

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":{
        "AUDCAD":{
            "ctm":1488844800,
            "today_open_price":"1.01650",
            "today_high":"1.02154",
            "today_low":"1.01502",
            "yesterday_close_price":"1.01684",
            "week_high":"1.06391",
            "week_low":"1.04941",
            "month_high":"1.07967",
            "month_low":"1.04929",
            "year_high":"1.16161",
            "year_low":"1.03393"
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
|limit|int|是|取多少条,不能少于2条多于500条|
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

#### <span id = "spread_info">6.获得 组、品种、产品、点差 信息</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/spread_info
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/spread_info
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:spread_info|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|


返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true/false|
|error_msg|string|返回信息|
|error_code|number|返回码|
|0| |获取成功|
|101| |传递参数错误|
|303| |验证失败|
|data|Object|返回信息|
|"security"|string|Json格式的字符串，产品属于品种|
|"spread_common"|string|Json格式的字符串，老虎平台默认点差|
|"spread_special_offset"|string|Json格式的字符串，与老虎不同点差组的、相对老虎的点差|
    
说明：
>相对点差spread_special_offset，该组真实点差spread_special = 老虎公共点差spread_common + 相对点差spread_special_offset

举例：
>假设相对点差为spread_special_offset，则计算量offset = （double）spread_special_offset / 2 
推送过来的买价为ask，卖价为bid 
用户实际的市场价格买价为ASK，卖价为BID 
则ASK=ask + offset, BID = bid - offset 
以后所有用到市场价格均要使用ASK或BID。
notrade：表示只能接受报价不能进行交易。

返回成功json:
```
{"error_code":0,"error_msg":"","is_succ":true,"data":{"security":{"AUDCAD":"Forex-1","AUDCHF":"Forex-1","AUDJPY":"Forex-1","AUDNZD":"Forex-1","AUDUSD":"Forex-1","CADCHF":"Forex-1","CADJPY":"Forex-1","CHFJPY":"Forex-1","EURAUD":"Forex-1","EURCHF":"Forex-1","EURGBP":"Forex-1","EURJPY":"Forex-1","EURNZD":"Forex-1","EURUSD":"Forex-1","EURCAD":"Forex-1","GBPAUD":"Forex-1","GBPCAD":"Forex-1","GBPUSD":"Forex-1","GBPNZD":"Forex-1","GBPJPY":"Forex-1","GBPCHF":"Forex-1","NZDCAD":"Forex-1","NZDCHF":"Forex-1","NZDJPY":"Forex-1","NZDUSD":"Forex-1","USDCNH":"Forex-1","USDCAD":"Forex-1","USDCHF":"Forex-1","USDJPY":"Forex-1","AUDCAD50":"Forex-L","AUDCHF50":"Forex-L","AUDJPY50":"Forex-L","AUDNZD50":"Forex-L","AUDUSD50":"Forex-L","CADCHF50":"Forex-L","CADJPY50":"Forex-L","CHFJPY50":"Forex-L","EURAUD50":"Forex-L","EURCHF50":"Forex-L","EURGBP50":"Forex-L","EURJPY50":"Forex-L","EURNZD50":"Forex-L","EURUSD50":"Forex-L","EURCAD50":"Forex-L","GBPAUD50":"Forex-L","GBPCAD50":"Forex-L","GBPUSD50":"Forex-L","GBPNZD50":"Forex-L","GBPJPY50":"Forex-L","GBPCHF50":"Forex-L","NZDCAD50":"Forex-L","NZDCHF50":"Forex-L","NZDJPY50":"Forex-L","NZDUSD50":"Forex-L","USDCNH50":"Forex-L","USDCAD50":"Forex-L","USDCHF50":"Forex-L","USDJPY50":"Forex-L","AUDCAD200":"Forex-M","AUDCHF200":"Forex-M","AUDJPY200":"Forex-M","AUDNZD200":"Forex-M","AUDUSD200":"Forex-M","CADCHF200":"Forex-M","CADJPY200":"Forex-M","CHFJPY200":"Forex-M","EURAUD200":"Forex-M","EURCHF200":"Forex-M","EURGBP200":"Forex-M","EURJPY200":"Forex-M","EURNZD200":"Forex-M","EURUSD200":"Forex-M","EURCAD200":"Forex-M","GBPAUD200":"Forex-M","GBPCAD200":"Forex-M","GBPUSD200":"Forex-M","GBPNZD200":"Forex-M","GBPJPY200":"Forex-M","GBPCHF200":"Forex-M","NZDCAD200":"Forex-M","NZDCHF200":"Forex-M","NZDJPY200":"Forex-M","NZDUSD200":"Forex-M","USDCNH200":"Forex-M","USDCAD200":"Forex-M","USDCHF200":"Forex-M","USDJPY200":"Forex-M","USDHKD":"NoTrade","XAUUSD":"Gold-USD","XAUUSD50":"Gold-USD-L","XAUUSD200":"Gold-USD-M","XAGUSD":"Silver-USD","XAGUSD50":"Silver-USD-L","XAGUSD200":"Silver-USD-M","XNGUSD":"Oil&Energy-USD","XBRUSD":"Oil&Energy-USD","XTIUSD":"Oil&Energy-USD","AUS200":"CFD","EUSTX50":"CFD","GER30":"CFD","HK50":"CFD","JPN225":"CFD","SPA35":"CFD","NAS100":"CFD","UK100":"CFD","US30":"CFD","USA500":"CFD","FRA40":"CFD"},"spread_common":{"Gold-USD":28,"Silver-USD":280,"Oil&Energy-USD":15,"Index-CFD":0,"Forex-1":16,"Forex-L":16,"Forex-H":16,"Gold-USD-L":28,"Gold-USD-H":28,"Silver-USD-L":280,"Silver-USD-H":280,"cancle":0,"Forex-M":16,"cfd-h":0,"CFD":0,"cfd-special":0,"Gold-USD-M":28,"Silver-USD-M":280,"NoTrade":16},"spread_special_offset":{"TBRD-M00AC-Tech":{"Gold-USD":0,"Silver-USD":220,"Oil&Energy-USD":0,"Forex-1":0,"Forex-L":0,"Gold-USD-L":0,"Silver-USD-L":0,"Forex-M":0,"cfd-h":0,"CFD":0,"cfd-special":0,"Gold-USD-M":-28,"Silver-USD-M":-280,"NoTrade":0},"TRUE-MONEY":{"Gold-USD":-28,"Silver-USD":-280,"Oil&Energy-USD":-15,"Forex-1":-16,"Forex-M":-16,"cfd-h":0,"CFD":0,"cfd-special":0,"Gold-USD-M":0,"Silver-USD-M":0,"NoTrade":0},"TRUE-MONEY_CFH":{"Gold-USD":-28,"Silver-USD":-280,"Oil&Energy-USD":-15,"Forex-1":-16,"Forex-M":-16,"CFD":0,"Gold-USD-M":0,"Silver-USD-M":0,"NoTrade":0},"STPUMAM-HY":{"Gold-USD":20,"Silver-USD":200,"Oil&Energy-USD":20,"Forex-1":20,"Forex-L":20,"Gold-USD-L":20,"Silver-USD-L":200,"CFD":0,"NoTrade":0},"HY-BRD":{"Gold-USD":0,"Silver-USD":0,"Oil&Energy-USD":0,"Forex-1":4,"Forex-L":4,"Gold-USD-L":0,"Silver-USD-L":0,"CFD":0,"NoTrade":0},"BRD_325":{"Gold-USD":0,"Silver-USD":0,"Oil&Energy-USD":0,"Forex-1":6,"Forex-L":6,"Gold-USD-L":0,"Silver-USD-L":0,"Forex-M":6,"CFD":0,"Gold-USD-M":0,"Silver-USD-M":0,"NoTrade":0},"STP_325":{"Gold-USD":0,"Silver-USD":0,"Oil&Energy-USD":0,"Forex-1":6,"Forex-L":6,"Gold-USD-L":0,"Silver-USD-L":0,"Forex-M":6,"CFD":0,"Gold-USD-M":0,"Silver-USD-M":0,"NoTrade":0},"BRD_325_400":{"Gold-USD":0,"Silver-USD":0,"Oil&Energy-USD":0,"Forex-1":6,"Forex-L":6,"Forex-H":6,"Gold-USD-L":0,"Silver-USD-L":0,"Forex-M":6,"CFD":0,"Gold-USD-M":0,"Silver-USD-M":0,"NoTrade":0},"STP_325_400":{"Gold-USD":0,"Silver-USD":0,"Oil&Energy-USD":0,"Forex-1":6,"Forex-L":6,"Forex-H":6,"Gold-USD-L":0,"Silver-USD-L":0,"Forex-M":6,"CFD":0,"Gold-USD-M":0,"Silver-USD-M":0,"NoTrade":0},"PKDS_BRD":{"Gold-USD":3,"Silver-USD":30,"Oil&Energy-USD":3,"Forex-1":10,"Forex-L":10,"Gold-USD-L":3,"Silver-USD-L":30,"Forex-M":10,"CFD":0,"Gold-USD-M":3,"Silver-USD-M":30,"NoTrade":0},"PKDS_TBRD-M00A":{"Gold-USD":3,"Silver-USD":30,"Oil&Energy-USD":3,"Forex-1":10,"Forex-L":10,"Gold-USD-L":3,"Silver-USD-L":30,"Forex-M":10,"CFD":0,"Gold-USD-M":3,"Silver-USD-M":30,"NoTrade":0},"PKDS_STP":{"Gold-USD":3,"Silver-USD":30,"Oil&Energy-USD":3,"Forex-1":10,"Forex-L":10,"Gold-USD-L":3,"Silver-USD-L":30,"CFD":0,"NoTrade":0},"TBRD-PKDS-SUM":{"Gold-USD":3,"Silver-USD":30,"Oil&Energy-USD":3,"Forex-1":10,"Forex-L":10,"Gold-USD-L":3,"Silver-USD-L":30,"CFD":0,"NoTrade":0},"PKDS_STP-CTRL":{"Gold-USD":3,"Silver-USD":30,"Oil&Energy-USD":3,"Forex-1":10,"Forex-L":10,"Gold-USD-L":3,"Silver-USD-L":30,"CFD":0,"NoTrade":0},"STPUMAM-LP":{"Gold-USD":20,"Silver-USD":200,"Oil&Energy-USD":20,"Forex-1":0,"Forex-L":0,"Gold-USD-L":20,"Silver-USD-L":200,"Forex-M":0,"CFD":0,"Gold-USD-M":20,"Silver-USD-M":200,"NoTrade":0},"BRD_315":{"Gold-USD":20,"Silver-USD":200,"Oil&Energy-USD":20,"Forex-1":20,"Forex-L":20,"Gold-USD-L":20,"Silver-USD-L":200,"Forex-M":20,"CFD":0,"Gold-USD-M":20,"Silver-USD-M":200,"NoTrade":0},"STP_315":{"Gold-USD":20,"Silver-USD":200,"Oil&Energy-USD":20,"Forex-1":20,"Forex-L":20,"Gold-USD-L":20,"Silver-USD-L":200,"Forex-M":20,"CFD":0,"Gold-USD-M":20,"Silver-USD-M":200,"NoTrade":0},"BRD_396":{"Gold-USD":10,"Silver-USD":100,"Oil&Energy-USD":10,"Forex-1":10,"Forex-L":10,"Gold-USD-L":10,"Silver-USD-L":100,"Forex-M":10,"CFD":0,"Gold-USD-M":10,"Silver-USD-M":100,"NoTrade":0},"STP_396":{"Gold-USD":10,"Silver-USD":100,"Oil&Energy-USD":10,"Forex-1":10,"Forex-L":10,"Gold-USD-L":10,"Silver-USD-L":100,"Forex-M":10,"CFD":0,"Gold-USD-M":10,"Silver-USD-M":100,"NoTrade":0},"BRD_392":{"Gold-USD":50,"Silver-USD":500,"Oil&Energy-USD":50,"Forex-1":50,"Forex-L":50,"Gold-USD-L":50,"Silver-USD-L":500,"Forex-M":50,"CFD":0,"Gold-USD-M":50,"Silver-USD-M":500,"NoTrade":0},"STP_392":{"Gold-USD":50,"Silver-USD":500,"Oil&Energy-USD":50,"Forex-1":50,"Forex-L":50,"Gold-USD-L":50,"Silver-USD-L":500,"Forex-M":50,"CFD":0,"Gold-USD-M":50,"Silver-USD-M":500,"NoTrade":0},"umam_31000063":{"Gold-USD":0,"Silver-USD":0,"Oil&Energy-USD":0,"Forex-1":7,"Forex-L":7,"Gold-USD-L":0,"Silver-USD-L":0,"Forex-M":7,"CFD":0,"Gold-USD-M":0,"Silver-USD-M":0,"NoTrade":0},"BRD_626":{"Gold-USD":20,"Silver-USD":200,"Oil&Energy-USD":20,"Forex-1":20,"Forex-L":20,"Gold-USD-L":20,"Silver-USD-L":200,"Forex-M":20,"CFD":0,"Gold-USD-M":20,"Silver-USD-M":200,"NoTrade":20},"STP_626":{"Gold-USD":20,"Silver-USD":200,"Oil&Energy-USD":20,"Forex-1":20,"Forex-L":20,"Gold-USD-L":20,"Silver-USD-L":200,"Forex-M":20,"CFD":0,"Gold-USD-M":20,"Silver-USD-M":200,"NoTrade":20},"BRD_631":{"Gold-USD":10,"Silver-USD":100,"Oil&Energy-USD":10,"Forex-1":10,"Forex-L":10,"Gold-USD-L":10,"Silver-USD-L":100,"Forex-M":10,"CFD":10,"Gold-USD-M":10,"Silver-USD-M":100,"NoTrade":10},"STP_631":{"Gold-USD":10,"Silver-USD":100,"Oil&Energy-USD":10,"Forex-1":10,"Forex-L":10,"Gold-USD-L":10,"Silver-USD-L":100,"Forex-M":10,"CFD":10,"Gold-USD-M":10,"Silver-USD-M":100,"NoTrade":10},"BRD_NT":{"Gold-USD":10,"Silver-USD":100,"Oil&Energy-USD":10,"Forex-1":10,"Forex-L":10,"Gold-USD-L":10,"Silver-USD-L":100,"Forex-M":10,"CFD":0,"Gold-USD-M":10,"Silver-USD-M":100,"NoTrade":0},"STP_NT":{"Gold-USD":10,"Silver-USD":100,"Oil&Energy-USD":10,"Forex-1":10,"Forex-L":10,"Gold-USD-L":10,"Silver-USD-L":100,"Forex-M":10,"CFD":0,"Gold-USD-M":10,"Silver-USD-M":100,"NoTrade":0},"PKDS1_BRD":{"Gold-USD":6,"Silver-USD":60,"Oil&Energy-USD":6,"Forex-1":13,"Forex-L":13,"Gold-USD-L":6,"Silver-USD-L":60,"Forex-M":13,"CFD":0,"Gold-USD-M":6,"Silver-USD-M":60,"NoTrade":0},"PKDS1_TBRD-M00A":{"Gold-USD":6,"Silver-USD":60,"Oil&Energy-USD":6,"Forex-1":13,"Forex-L":13,"Gold-USD-L":6,"Silver-USD-L":60,"Forex-M":13,"CFD":0,"Gold-USD-M":6,"Silver-USD-M":60,"NoTrade":0},"PKDS1_STP":{"Gold-USD":6,"Silver-USD":60,"Oil&Energy-USD":6,"Forex-1":13,"Forex-L":13,"Gold-USD-L":6,"Silver-USD-L":60,"CFD":0,"NoTrade":0},"BRD_372":{"Gold-USD":-17,"Silver-USD":-170,"Oil&Energy-USD":-8,"Forex-1":-8,"Forex-L":-8,"Gold-USD-L":-17,"Silver-USD-L":-170,"Forex-M":-8,"CFD":0,"Gold-USD-M":-17,"Silver-USD-M":-170,"NoTrade":-8},"STP_372":{"Gold-USD":-17,"Silver-USD":-170,"Oil&Energy-USD":-8,"Forex-1":-8,"Forex-L":-8,"Gold-USD-L":-17,"Silver-USD-L":-170,"Forex-M":-8,"CFD":0,"Gold-USD-M":-17,"Silver-USD-M":-170,"NoTrade":-8}}}}
```

#### <span id = "symbol_price">7.获取单个价格信息（不是实时）</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/symbol_price
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/symbol_price
```
* 类型:HTTPS post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:symbol_price|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|symbol|string|是|产品|


返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true/false|
|error_msg|string|返回信息|
|error_code|number|返回码|
|0| |获取成功|
|101| |传递参数错误|
|303| |验证失败|
|data|Object|返回信息|
|bid|double|卖价|
|ask|double|买价|
|low|double|最低价|
|high|double|最高价|
|digits|int|小数位|
    
说明：
>该接口价格信息会有大概30秒左右延迟

返回成功json:
```
{
    "error_code":0,
    "error_msg":"获取成功",
    "is_succ":true,
    "data":{
        "ask":1.02209,
        "bid":1.02178,
        "low":1.02154,
        "high":1.02549,
        "digits":5
    }
}
```
