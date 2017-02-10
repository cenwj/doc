# 老虎外汇文档

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html)

#保证金计算
【A】产品信息
单笔交易占用保证金：margin
合约量：contract_size
初始保证金：margin_initial
百分比：percentage
保证金百分比：margin_divider
存款货币：deposit_currency
保证金货币：margin_currency
用户杠杆：leverage
保证金公式计算结果:margin_calc
注：
① percentage = 100 / margin_divider
② deposit_currency统一为美元USD
③ leverage统一为100
【B】订单信息
买价：ask
卖价：bid
交易手数：lots
开仓价格：market_price
保证金换算比率：margin_rate
注：
① lots是volumeinlots的缩写，volume为接口返回数值，关系：lots = volume * 0.01
② 开仓价格：买入market_price使用ask, 卖出market_price使用bid
③ margin_rate为margin_currency与deposit_currency之间的换算比率，deposit_currency' = margin_currency' * margin_rate
【C】计算公式
① 普通货币对Forex
margin_calc = lots * contract_size / leverage * percentage / 100
② 原油、贵金属 （XAUUSD, XAGUSD, XNGUSD, XBRUSD, XTIUSD）
margin_calc = lots * margin_initial * percentage / 100
③ 指数产品CFD （AUS200,EUSTX50,GER30,HK50,JPN225,SPA35,NAS100,UK100,US30,USA500,FRA40）
margin_calc = lots * contract_size * market_price / leverage * percentage / 100
【D】货币换算
利用公式计算的结果，单位是margin_currency
若需转换为存款货币，即美元，分两种情况：
① 订单已成交（下单开仓，或获得用户持仓单）
则margin_rate可通过接口获得，该笔交易占用保证金
margin = margin_calc * margin_rate
其中，margin_currency为USD的margin_rate=1
② 订单未成交，需根据价格、手数预先计算需占用保证金，并换算为美元
a. 如果产品的margin_currency为美元USD，则无需换算
b. 如果产品的margin_currency不是美元，则使用相关货币 `USD***` 或 `***USD`的价格作为换算标准：price = (ask + bid) / 2
如果USD为基础货币（货币对第一个币种），则 margin = margin_calc / price;
如果USD为兑换货币（货币对第二个币种），则 margin = margin_calc * price