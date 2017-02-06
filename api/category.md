# 老虎外汇文档

#### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html)


## 接口分类
 
>=============================接口说明============================
>测试服务器接口统一地址入口:http://demo.tigerwit.com/action/public/api/
>正式服务器接口统一地址入口:https://api.tigerwit.com/action/public/api/
>生成签名方式点击:[加密方式](/index.html#fangshi)
>===============================================================


### 开户、个人中心
* [开户](/api/user.html#signup)
* [获取跟随高手当前订单分组](/api/user.html#get_master_group)
* [获取跟随高手历史订单分组](/api/user.html#get_master_history_group)
* [获取跟单的持仓订单](/api/user.html#documentary_order) 
* [外汇持仓接口](/api/user.html#foreign_order)
* [外汇账户汇总接口](/api/user.html#foreign_exchange_account)
* [获取用户所有历史交易记录](/api/user.html#get_trade_record)
* [充值记录](/api/user.html#get_payment_record)

### 高手 
* [获取高手列表](/api/master.html#get_master_list_v2)
* [高手的基本信息](/api/master.html#get_master_info_v2)
* [高手历史月收益率表现图标](/api/master.html#historical_rate)
* [高手复制者变化图标](/api/master.html#copy_change)
* [高手月交易品种图标](/api/master.html#monthly_symbols)
* [获取高手当前投资详情](/api/master.html#get_master_order)
* [获取高手历史投资详情](/api/master.html#get_master_history)
* [复制高手](/api/master.html#copy_master_v2)
* [解除复制高手并强平](/api/master.html#uncopy_master_forced_liquidation)
* 解除复制高手并强平前的预算金钱 
* 获取高手最低复制金额

### 持仓明细
* 获取用户持仓汇总 
* 获取用户持仓明细
* 获取用户跟随单个高手持仓汇总
* 获取用户跟随单个高手持仓明细 


### 交易品种
* 获取交易品种汇总
* 获取交易品种详情 
* 所有交易品种详情
* 获取单个品种、开收盘信息
* 获取多个品种、昨日收盘价格【有缓存】
* 历史报价


### 下单、平仓、挂单
* 开仓
* 平仓
* 修改订单止盈止损 
* 挂单交易接口 
* 修改挂单 
* 删除挂单 
* 获取所有挂单 

### 入金、出金、汇率

* 申请入金
* 申请出金
* 手机客户端入金(智付入金)
* pc电脑端入金
* 获取入金汇率
* 出金汇率
* 获取银行卡信息 
* 获取可出余额，信用值，交易手数 

### 老虎回调第三方接口(需提供第三方回调地址)
* 入金成功
* 申请出金成功



