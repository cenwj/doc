# <span id = "liucheng">老虎外汇文档</span>

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html)

## 止盈止损
cmd 
enum { OP_BUY=0,OP_SELL,OP_BUY_LIMIT,OP_SELL_LIMIT,OP_BUY_STOP,OP_SELL_STOP,OP_BALANCE,OP_CREDIT };

1：普通订单开仓止盈止损设置

1.1：开仓买涨时

TP 的值 应 大于等于 平仓价格 BID + stops_level => (TP-BID) * multiply >= level 
SL 的值 应 小于等于 平仓价格 BID - stops_level => (BID-SL) * multiply >= level

1.2：开仓买跌时

TP 的值 应 小于等于 平仓价格 ASK+ stops_level => (ASK-TP) * multiply >= level 
SL 的值 应 大于等于 平仓价格 ASK - stops_level => (SL-ASK) * multiply >= level


2：持仓单修改止盈止损

同开仓设置

3：挂单开仓止盈止损 和 挂单还未成交时修改止盈止损

按照挂单价格(pending_price)\小数位数(multiply = 10^nDigit)\止损水平(stopslevel)计算

3.1 buy_limit 
>(pending_price - SL) * multiply >= level

3.2 buy_stop 
>(TP - pending_price) * multiply >= level

3.3 sell_limit 
>(SL - pending_price) * multiply >= level

3.4 sell_stop 
>(pending_price - TP) * multiply >= level