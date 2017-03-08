# 老虎外汇文档

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html) 

#挂单 
在未来某个价格设定挂单，到达后会自动生成此订单 
cmd自动从2.3.4.5变化为0.1 
【A】下单规则 
0 挂单设定 
一直有效，直至客户取消 
挂单不跟单，成交时跟单 
1 cmd 
enum { OP_BUY=0,OP_SELL,OP_BUY_LIMIT,OP_SELL_LIMIT,OP_BUY_STOP,OP_SELL_STOP}; 
limit → 与buy盈利的方向，即向上，相反；做多单，buy 
① buy_limit 
买入限价, 在现在价格的下方挂多单 
② sell_limit 
卖出限价, 在现在价格的上方挂空单 
③ buy_stop 
买入止损, 在现在价格的上方挂多单 
④ sell_stop 
卖出止损, 在现在价格的下方挂空单

2 pending_price 
普通外汇 - 挂单及止损点差level - 配置 
① buy_limit 
pending_price <= ask - level 
② sell_limit 
pending_price >= bid + level 
③ buy_stop 
pending_price >= ask + level 
④ sell_stop 
pending_price <= bid - level

3 pending order's expiration time 
挂单到期日必须远离当前时间至少10分钟

4 止盈止损 
按照挂单价格(pending_price)\小数位数(multiply = 10^nDigit)\止损水平(stopslevel)计算 
① buy_limit, buy_stop 
(pending_price - sl) * multiply > level 
(tp - pending_price) * multiply > level 
② sell_limit, sell_stop 
(sl - pending_price) * multiply > level 
(pending_price - tp) * multiply > level

【B】修改规则 
1 删除挂单 
2 修改止盈止损(sl/tp) 
3 修改挂单价格 
根据现有的止盈止损价格，如果挂单价格不满足止盈止损条件和市场价格条件，则不允许修改 
4 修改挂单到期时间 
根据当前时间判断 
5 不允许修改交易手数 
6 挂单成交后，转为普通订单修改

【C】与市价成交 
1 需要市场价格 
① 周末，市场关闭，禁止交易 
② 与①相同，设置的交易时间外，市场关闭，请稍后再试 
③ 市场流动性不足，禁止交易 
2 仅支持100、50、200杠杆产品 
3 只读账户不允许交易 
4 无需判断保证金，成交时系统自动判断 
5 下单手数 
① 满足设置规则 
② 无需判断手数过大超过余额 
6 止盈止损