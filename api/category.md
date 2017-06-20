# 老虎外汇文档

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html)


## 接口分类
 
>=============================接口说明============================
>测试服务器接口统一地址入口: `https://demo.tigerwit.com/action/public/api/`
>正式服务器接口统一地址入口: `https://api.tigerwit.com/action/public/api/`
>生成签名方式点击:[加密方式](/index.html#fangshi)
>===============================================================


### 开户、个人中心
* [H5开户、实名认证 ](/api/register.html#register)
* [开户(废弃、用H5开户)](/api/user.html#signup)
* [开户（加上密码参数）（废弃、用H5开户）](/api/user.html#signup_v3)
* [获取跟随高手当前订单分组](/api/user.html#get_master_group)
* [获取用户跟随单个高手持仓明细](/api/user.html#get_master_order_info)
* [获取跟随高手历史订单分组](/api/user.html#get_master_history_group)
* [获取用户跟随单个高手平仓明细](/api/user.html#get_master_history_info)
* [获取用户所有历史交易记录](/api/user.html#get_trade_record)
* [获取跟单的持仓订单](/api/user.html#documentary_order) 
* [外汇持仓接口](/api/user.html#foreign_order)
* [外汇账户汇总接口](/api/user.html#foreign_exchange_account)
* [充值记录](/api/user.html#get_payment_record)
* [检查mt4_id、密码是否正确](/api/user.html#check_mt4)
* [修改mt4密码](/api/user.html#change_password)
* [获取交易手数、收益率、平仓总收益](/api/user.html#transaction)

### 红包
* [红包列表](/api/bonus.html#bonus_lists) 
* [领取红包](/api/bonus.html#bonus_receive) 
* [我的红包列表](/api/bonus.html#my_bonus) 
* [兑换红包](/api/bonus.html#bonus_pay_condition) 


### 高手 
* [获取高手列表](/api/master.html#get_master_list_v2)
* [高手的基本信息](/api/master.html#get_master_info_v2)
* [高手历史月收益率表现图标](/api/master.html#historical_rate)
* [高手复制者变化图标](/api/master.html#copy_change)
* [高手月交易品种图标](/api/master.html#monthly_symbols)
* [获取高手当前投资详情](/api/master.html#get_master_order)
* [获取高手历史投资详情](/api/master.html#get_master_history)
* [复制高手](/api/master.html#copy_master_v2)
* [解除复制高手并强平](/api/master.html#cancel_copy)
* [解除复制高手并强平前的预算金钱](/api/master.html#uncopy_master_budget)
<!-- * [获取高手最低复制金额](/api/master.html#get_master_min_copy_amount) -->

### 交易品种
* [获取交易品种汇总](/api/symbols.html#get_symbols)
* [所有交易品种详情](/api/symbols.html#symbol_list_info)
* [获取单个品种、开收盘信息](/api/symbols.html#history_day_info)
* [获取多个品种、昨日收盘价格【有缓存】](/api/symbols.html#yesterday_close_price)
* [历史报价](/api/symbols.html#get_symbols_history)
* [根据时间段获取历史报价](/api/symbols.html#history_info_start_time)
* [获得 组、品种、产品、点差 信息](/api/symbols.html#spread_info)
* [获取单个价格信息（不是实时）](/api/symbols.html#symbol_price)
* [产品交易时间段](/api/symbols.html#trade_date)

### 开仓、平仓、挂单
* [开仓](/api/trade.html#open_trader)
* [平仓](/api/trade.html#close_trader)
* [修改订单止盈止损](/api/trade.html#update_trader)
* [挂单交易接口](/api/trade.html#pending_order) 
* [修改挂单](/api/trade.html#pending_modify) 
* [删除挂单](/api/trade.html#pending_delete) 
* [获取所有挂单](/api/trade.html#get_pending) 

### 入金、出金、汇率

* [申请入金【手机客户端入金】](/api/payment.html#deposit_v2)
* [申请出金[将要废弃]](/api/payment.html#withdraw)
* [申请出金_v2](/api/payment.html#withdraw_v2)
* [出金汇率](/api/payment.html#get_withdraw_rate)
* [入金汇率](/api/payment.html#get_exchange_rate)
* [获取银行卡信息](/api/payment.html#check_user_card)
* [获取可出余额，信用值，交易手数](/api/payment.html#get_withdraw_info)
* [pc电脑端入金(不回调)(废弃)](/api/payment.html#pay)
* [pc电脑端入金(有回调)](/api/payment.html#pay_callback)


### 老虎回调第三方接口(需提供第三方回调地址)
* [老虎外汇对接第三方出金入金回调接口文档](/api/callback.html#)




