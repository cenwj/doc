# 老虎外汇文档

#### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html)

============================开户、个人中心============================
* <span id = "signup">开户</span>




#### 2. <span id = "get_master_group">获取跟随高手当前订单分组</span> 

* 测试请求URL:http://demo.tigerwit.com/action/public/api/get_master_group
* 线上请求URL:https://api.tigerwit.com/action/public/api/get_master_group
* 类型:HTTPS post
* 参数:JSON String 
* 传递参数:

|名称|类型|是否必须|说明|
|:--:|:--:|:--:|:--:|
|action|string|是|传递的方法:get_master_group|
|user_id|int|是|第三方user_id|
|mt4_id|int|是|老虎开户mt4_id|

返回参数说明:

|参数|类型|说明|
|:--:|:--:|:--:|
|is_succ|bool|true:成功 false:失败|
|error_msg|string|返回信息|
|error_code|number|返回码|
|0||请求成功|
|101||传递参数错误|
|105||获取不到第三方用户信息或者老虎账户信息|
|303||签名验证失败|
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
