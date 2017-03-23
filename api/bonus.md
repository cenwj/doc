# 老虎外汇文档

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html)

## 接口分类 
### 红包

#### <span id = "bonus_lists">1.红包列表</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/bonus_lists
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/bonus_lists
```
* 类型:HTTP(S) post,get
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:bonus_lists|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|page|int|是|页数|
|pagesize|int|是|条数|

返回参数说明:

|名称|类型|说明|
|:-------------:|:-------------:|:-------------:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码 0 成功 其他失败|
| num |int|总条数|
|data|array|返回详情|
| name |string|红包名称|
| amount |float|红包金额|
| num |int|红包发放数量|
| id |int|红包id |
| pay_condition |int|兑换条件ID|
| pay_condition_desc |string|兑换条件描述|
| acquire_mode |int|1:自动，2:手动|
| is_receive |string|1:已领取、2:未领取[手动领取]、3:已领完、4:未到领取时间|
|status_name|string|红包状态名称|
|acquire_start|string|红包领取期限起始日期|
|acquire_end|string|红包领取期限结束日期|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "data":[
        {
            "num":1333,
            "id":87,
            "pay_condition":6,
            "acquire_end":"2017-04-04 04:44:44",
            "acquire_start":"2017-03-15 00:00:00",
            "name":"充一万150手cfd",
            "acquire_mode":2,
            "amount":10000,
            "pay_condition_desc":"首次入金后5天内累计入金1万美元以上，完成200手交易，且兑换前没有出金操作（包含首次入金金额）(CFD产品不参与活动)",
            "is_receive":1,
            "status_name":"已领取"
        }
    ],
    "num":4
}
```

#### <span id = "bonus_receive">2.领取红包</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/bonus_receive
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/bonus_receive
```
* 类型:HTTP(S) post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:bonus_receive|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|id|int|是|红包id|

返回参数说明:

|名称|类型|说明|
|:-------------:|:-------------:|:-------------:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码 0 成功 其他失败|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"领取成功",
    "is_succ":true
}
```

#### <span id = "my_bonus">3.我的红包列表</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/my_bonus
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/my_bonus
```
* 类型:HTTP(S) post,get
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:my_bonus|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|type|int|是|红包类型：2=>['已领取','可兑换'】 ,3 => '已兑换',4 => 【'已过期'，'已失效'】|
|page|int|是|页数|
|pagesize|int|是|条数|

返回参数说明:

|名称|类型|说明|
|:-------------:|:-------------:|:-------------:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码 0 成功 其他失败|
|num|int|总条数|
|data|array|详情数据|
| amount | float |红包金额|
| bonus_id | int |用户领取的所属红包id|
| user_bonus_id | int |用户领取的红包列表id|
| pay_condition_name | string |兑换条件名称|
| pay_expire | int |兑换期限，天数|
| valid_start | string |有效期起始日期|
| valid_end | string |兑换截止时间|
| bonus_desc | string |红包描述|
| bonus_name | string |红包名称|
| acquire_time | string |领取期限起始日期|
| acquire_end | string |领取期限结束日期|
| cfd | int |是否计算CFD交易手数，0-不计算，1-计算|
| bonus_status | int |红包状态 1 => '已领取',2 => '可兑换',3 => '已兑换',,4 => ['已过期'，'已失效'],5=>['已兑换','已过期','已失效']|
| status_name | string |红包状态名称|
| pay_time | string |兑换时间|
| redirect | int |app需要调整的页面|

说明：
移动端红包“去完成”对应跳转页面

|序号|APP红包跳转涉及页面汇总|
|:----:|:-------------:|
|1|交易品种订阅列表|
|2|充值页面|
|6|高手列表页|

###第一版红包跳转页面

|序号|兑换条件（括号内容不显示在用户页面）|“去完成”对应跳转|
|-----|----------|--------------------|
|1|体验金交易满2手、盈利15%以上（无持仓订单），完成首次入金后即可兑现|跳转至交易列表页面|
|2|首次入金并完成5手交易，且兑换前没有出金操作|跳转至充值页面|
|3|首次入金并完成15手交易，且兑换前没有出金操作|跳转至充值页面|
|4|首次入金并完成30手交易，且兑换前没有出金操作|跳转至充值页面|
|5|首次入金并完成50手交易，且兑换前没有出金操作|跳转至充值页面|
|6|首次入金后5天内累计入金1万美元以上，完成150手交易，且兑换前没有出金操作（包含首次入金金额）|跳转至充值页面|
|8|完成首次入金，累计完成25手交易，且兑换前未出金|跳转至充值页面|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"",
    "is_succ":true,
    "num":2,
    "data":[
        {
            "amount":10000,
            "bonus_id":87,
            "user_bonus_id":505452,
            "pay_condition_name":"首次入金后5天内累计入金1万美元以上，完成200手交易，且兑换前没有出金操作（包含首次入金金额）",
            "pay_expire":10000,
            "valid_start":"2017-03-15 00:00:00",
            "valid_end":"2017-04-16 23:59:59",
            "bonus_desc":"",
            "bonus_name":"充一万150手cfd",
            "acquire_time":"2017-03-21 16:00:41",
            "acquire_start":"2017-03-15 00:00:00",
            "acquire_end":"2017-04-04 04:44:44",
            "cfd":1,
            "bonus_status":1,
            "pay_time":null,
            "redirect":2,
            "status_name":"未完成"
        },
        {
            "amount":10000,
            "bonus_id":87,
            "user_bonus_id":505449,
            "pay_condition_name":"首次入金后5天内累计入金1万美元以上，完成200手交易，且兑换前没有出金操作（包含首次入金金额）",
            "pay_expire":10000,
            "valid_start":"2017-03-15 00:00:00",
            "valid_end":"2017-04-16 23:59:59",
            "bonus_desc":"",
            "bonus_name":"充一万150手cfd",
            "acquire_time":"2017-03-21 15:59:54",
            "acquire_start":"2017-03-15 00:00:00",
            "acquire_end":"2017-04-04 04:44:44",
            "cfd":1,
            "bonus_status":1,
            "pay_time":null,
            "redirect":2,
            "status_name":"未完成"
        }
    ]
}
```

#### <span id = "bonus_pay_condition">4.兑换红包</span> 

* 测试请求URL:
```
http://demo.tigerwit.com/action/public/api/bonus_pay_condition
```
* 线上请求URL:
```
https://api.tigerwit.com/action/public/api/bonus_pay_condition
```
* 类型:HTTP(S) post
* 参数:JSON String
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:bonus_pay_condition|
|signature|string|是|签名|
|private_key|string|是|分配给第三方的key|
|user_id|int|是|第三方用户id|
|mt4_id|int|是|老虎mt4_id|
|user_bonus_id|int|是|用户领取的红包列表id|

返回参数说明:

|名称|类型|说明|
|:-------------:|:-------------:|:-------------:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回错误信息|
|error_code|int|返回码 0 成功 其他失败|
|0| |获取成功|
|1| |不是可兑换红包|
|2| |红包已经过期，不过兑换|
|3| |领取失败，系统错误|
|msg|string|红包兑换提示|

返回成功json:
```
{
    "error_code":0,
    "error_msg":"兑换成功",
    "is_succ":true,
    "msg":"$50.00红包已经成功转到你的账户!"
}
```