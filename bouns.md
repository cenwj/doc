# <span id = "liucheng">老虎外汇文档</span>

#### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html)

## 高手分成
#### 跟单及分成逻辑优化—高手分成水位线
**1.客户账户**

分成水位计算方法： 
系统自动记录历史最高收益水位线b，触发分成结算条件时，计算历史总收益a，判断（a-b）值是否大于0： 
是，在复制金额中扣除（a-b）的20%作为高手分成；更新最高收益水位线b值。 
否，不扣分成。

备注： 
1.最高收益水位线初始值默认为0 
2.有效跟单更改为：只要跟随高手成功开仓的订单均视为有效跟单。 
3.触发分成结算条件：
①“取消复制高手并跟随高手平仓”的订单全部已平仓时 
②取消复制高手并强制平仓”时 
③“每月1日

**2.高手账户**

每月10日系统自动将高手分成转入对应账户