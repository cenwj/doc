# 老虎外汇文档

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html) 

# <center><span id = "signup">H5开户、实名认证 </span> </center>

## 一、概述
1.第三方平台开通老虎外汇平台账户，需要通过调用老虎外汇h5页面开通mt4账户。
2.当第三方平台用户还没有开户成功时，需要进行：kyc认证、身份信息填写、上传身份证正反面，然后等待审核。审核通过会回调第三方平台提交的api接口，通知第三方平台的用户已经成功开通老虎外汇平台账户。审核不通过，会回调第三方平台提交的api接口，通知第三方平台让用户重新填写实名认证资料。
3.第三方平台用户没有开户时需要以下情景跳转到h5开户页面
&nbsp;&nbsp;&nbsp;1）交易前（未开户或没有审核通过）
&nbsp;&nbsp;&nbsp;2）入金前（未开户或没有审核通过）
&nbsp;&nbsp;&nbsp;3）查看持仓前 （未开户或没有审核通过）
4.第三方平台用户已经开户再调用h5页面会到用户开户成功页面。
5.第三方平台用户已经开户需要修改mt4密码，第三方手动调用修改mt4密码h5页面。

## 二、开户流程
如下图：
![示例](http://www.processon.com/chart_image/58f6c936e4b0c9097c9046d2.png)


下面对其步骤详细介绍:
### 步骤一：第三方平台在老虎平台开户
>引用h5开户页面时，需要把老虎平台需要的参数和签名带到h5页面url。

开户h5页面链接:
测试：`https://demo.tigerwit.com/m/third/register`
线上：`https://www.tigerwit.com/m/third/register`

用到的参数
1）第三方用户id参数为: user_id
2）第三方用户手机号参数为:phone
3）提供给第三方的私有key参数为:private_key
4）第三方生成的签名参数为:sign
5）请求行为参数为:action

签名生成方法：
>签名不在第三方app客户端生成，必须由第三方服务器生存。 
>签名同提供第三方的接口生成签名一样。 

生成签名sign用到的参数：

|名称|说明|必须|
|:--:|:--:|:--:|
|action|请求行为，固定值为：register|是|
| user_id |第三方平台用户id|是|
|phone |第三方平台用户手机号码|是|
|private_key|老虎平台分配给第三方平台的私有Key |是|
|partner_key |老虎平台分配给第三方平台合作伙伴Key|是|
| partner_secret |老虎平台分配给第三方平台合作伙伴Secret |是|

### 步骤二：用户开户成功

1.引用修改mt4密码h5页面
>引用h5开户页面时，需要把老虎平台需要的参数和签名带到h5页面url。

修改mt4密码h5页面链接:
测试：`https://demo.tigerwit.com/m/third/password`
线上：`https://www.tigerwit.com/m/third/password`
 <!-- /third/complete/changePassword  和app交互请求链接 -->
用到的参数

1）第三方用户id参数为:user_id
2）老虎平台mt4_id参数为:mt4_id
3）提供给第三方的私有key参数为:private_key
4）第三方生成的签名参数为:sign
5）请求行为参数为:action

生成签名sign用到的参数：

|名称|说明|必须|
|:--:|:--:|:--:|
|action|请求行为，固定值为：password|是|
| user_id |第三方平台用户id|是|
| mt4_id |老虎平台mt4_id|是|
|private_key|老虎平台分配给第三方平台的私有Key |是|
|partner_key |老虎平台分配给第三方平台合作伙伴Key|是|
| partner_secret |老虎平台分配给第三方平台合作伙伴Secret |是|

**注意：**第三方的带到h5页面链接的参数，会储存在cookie，cookie有效时间为30分钟。

### 步骤三：审核失败回调第三方

第三方平台接收回调参数：

|- |-|
|:--:|:--:|
|请求类型|post|
|请求地址|需第三方提供|
|请求说明|入金\出金结束后回调的接口|

请求第三方地址接收参数:

|参数名称|描述|类型|必填|
|:--|:--|:--|:--|
|function|AUDIT|varchar(8)|是|
|signature|签名|varchar(64)|是|
|user_id|第三方平台用户id|int(11)|是|
|error_msg|审核失败原因|string|是|

返回参数:

|参数名称|说明|类型|必需|
|:--|:--|:--|:--|
|code|是否成功 [成功:success,失败:fail]|string|yes|
|message|返回信息|string|yes|

>说明:第三方平台接收到的参数，用于生成signature（签名），第三方生成签名同入金、出金回调。

json:
```
{
   "code": "success",
   "message": "回调成功"
}
```

### 步骤四：开户成功回调第三方

第三方平台接收回调参数：

|- |-|
|:--:|:--:|
|请求类型|post|
|请求地址|需第三方提供|
|请求说明|入金\出金结束后回调的接口|

请求第三方地址接收参数:

|参数名称|描述|类型|必填|
|:--|:--|:--|:--|
|function|REGISTER|varchar(8)|是|
|signature|签名|varchar(64)|是|
|certificate_no|身份证号|varchar(32)|是|
|real_name|真实姓名|varchar(32)|是|
|user_id|第三方平台用户id|int(11)|是|
|mt4_id|老虎平台mt4_id|int(11)|是|
|register_time|注册时间| date|是|
|apply_time|开户成功时间|date|是|
|password|mt4密码|string|是|

返回参数:

|参数名称|说明|类型|必需|
|:--|:--|:--|:--|
|code|是否成功 [成功:success,失败:fail]|string|yes|
|message|返回信息|string|yes|

>说明:第三方平台接收到的参数，用于生成signature（签名），第三方生成签名同入金、出金回调。

json:
```
{
   "code": "success",
   "message": "回调成功"
}
```

<center> [返回顶部](#top) </center>     
