# <span id = "liucheng">老虎外汇文档</span>

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html)

#价格规则
####推送的实时报价，ask，bid，mid，分别代表什么？
#####1.ask为基准买价，bid为基准卖价，mid为实时K线图中的跳动横线报价（卖价） 
#####2.用户实际成交价格需要在基准价基础上增加对应点差
>用户买价 = ask + SPREAD / 2
 用户卖价 = bid - SPREAD / 2
#####3.点差规则【SPREAD】
>不同产品拥有不同点差，[组的点差连接]
#####4.开平仓价格规则
>买涨:开仓取用户买价，平仓取用户卖价
 买跌:开仓取用户卖价，平仓取用户买价
#####5挂单价格、止盈止损规则
>buy_limit,buy_stop看用户买价
sell_limit,sell_stop看用户卖价


