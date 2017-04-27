# <span id = "liucheng">老虎外汇文档</span>

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html)

## 盈亏计算

【A】产品信息 
合约量：contract_size 
存款货币：deposit_currency 
盈亏货币：profit_currency 
流通货币：profit_cal_currency 
注： 
① deposit_currency统一为美元USD 
② profit_cal_currency 为[【产品配置】](/api/symbols.html#symbol_list_info)，可获得 
【B】订单信息 
买涨买跌标识：cmd 
开仓价：open_price 
平仓价或市场价：close_price 
市场价买价：ask 
市场价卖价：bid 
交易手数：lots 
存款货币盈亏：profit 
公式计算盈亏：profit_cal 
注： 
① lots是volumeinlots的缩写，volume为接口返回数值。
表示手数的数字如果是整型lost=volume,浮点型 lots = volume * 0.01。
② 接口返回的盈亏为profit，以美元为单位，仅价格变动造成的盈亏，不包括过夜费、手续费、佣金等 
【C】计算公式 
profit_cal = (close_price - open_price) * contract_size * lots 
【D】公式结果货币单位 
公式结果货币单位即为profit_currency，分两种情况： 
① 如果产品是CFD（profit_cal_currency = USD），则profit_currency = profit_cal_currency 
② 如果产品是 普通货币对、原油、贵金属（profit_cal_currency != USD），则profit_currency为兑换货币，即货币对的第二个币种 
【E】货币换算 
① 如果profit_currency为美元USD，则 profit = prpfit_cal 
② 如果profit_currency不是美元USD，需要转换成美元盈亏，则使用相关货币 `USD***` 或 `***USD` 价格进行换算 
该换算价格price_trans即为平台推送的已经点差偏移的价格 
a. 如果相关货币的基础货币是USD 
如果cmd=0, 则price_trans为当前bid；cmd=1, 则price_trans为ask 
美元盈亏profit = profit_cal / price_trans 
b. 如果相关货币的兑换货币是USD 
如果cmd=0, 则price_trans为当前bid；cmd=1, 则price_trans为ask 
美元盈亏profit = profit_cal * price_trans