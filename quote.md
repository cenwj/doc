# 老虎外汇文档

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html)


## 报价推送

先建立与服务端quote.tigerwit.com的连接，监听8888端口，再执行登陆命令。

#### 1.登陆 
类型:socket 
参数:json格式字符串的byte数组 
```
{ 
"UserName":"xxx", 
"LoginTime":登陆时间,类型:datetime 
"DevId":唯一标示,GUID,类型:string 
"Token":登陆参数，类型:string 
} 
```
###### 描述: 
LoginTime的值需要格式化：yyyy-MM-dd HH:mm:ss 
DevId=Guid(); 
Token=(pwd(xxxx)+LoginTime +UserName + DevId)的值进行MD5加密，字节数组转换16进制 
>header： 1-2-3-bodysize/256-bodysize%256 

返回结果: 
5位字节的header：2-2-3-0-66+body数据：
>{"Code":"success","Message":"","RequestNo":"0","ServiceCode":null} 

判断是否登陆成功 即判断返回的header数据 5位的byte字节：2-2-3-0-66

|名称 |类型 |说明| 
|:---:|:--:|:---:|
|Code| string| 是否成功| 
|Message| string| 异常信息| 
|RequestNo |int |0为OK |
|ServiceCode| string| 服务端返回码 登陆成功返回Null|

#### 2.心跳 
登陆成功之后 需要开启独立的线程 
维护客户端心跳 
维护心跳 当每收到body为null 只有header的包 且header[0]为1时 向服务器发送 5位byte： 2-1-3-0-0 
同样需要开启独立的线程 
维护服务器心跳 
维护心跳需要每5秒定时发送header数据 =5位byte： 1-1-3-0-0
**说明：**
>服务端需要知道客户端是否alive 客户端也需要知道服务端是否alive 所以需要心跳，如果服务端检测到客户端没有心跳 也就5秒内没有收到客户端的心跳响应的时候 服务端认为客户端没有alive 会kill掉客户端，如何维护心跳 就是上面的文档内容，发送固定的只有header的数据 响应服务端的心跳请求。

#### 3.报价请求 
发送数据格式： 
>header：1-3-3-bodysize/256-bodySize%256 body

body为json格式字符串字节数组 
```
{ 
Params:["AUDUSD","CHFUSD"], 
RequestNo:"0", 
ServiceCode:"00001" 
}
```

#### 4.报价响应 
>symbol, ask, bid, mid, ctm 

其中 

* symbol为没有数字的产品名称 
* ask为有点差的买价，与MT4客户端相同 
* bid为有点差的卖价，与MT4客户端相同 
* mid为无点差的实时报价 
* ctm为报价读取时间。 


![示例](http://app2.mailpanda.com/recipient/image?a=20&f=151952970831888384.jpg)

#### 5.测试端口9999 
最新变动会在该端口更新，生产端口8888更新较慢。