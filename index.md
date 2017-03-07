# <span id = "liucheng">老虎外汇文档</span>

##### [系统功能](/) |  [接口分类](/api/category.html) | [报价推送](/quote.html) | [盈亏计算](/formula.html) | [止盈止损](/level.html) | [高手分成](/bouns.html) | [挂单](/pending.html) | [保证金计算](/ouccupy_asset.html) | [公告](/notice.html)

## 系统功能

##### [编写目的](#mudi) | [术语约定](#yueding) | [加密方式](#fangshi) | [处理流程](#liucheng) | [通信方式](#tongxin) | [返回格式](#fanhui)

### <span id = "mudi">编写目的 </span>
本文档旨在规范第三方对接的数据通信方式,数据格式等描述,目的是:

* 规范第三方系统与老虎外汇的系统对接
* 为第三方对接老虎外汇提供系统标准

### <span id = "yueding">术语约定</span>
* MD5 一种不可逆加密算法
* signature 数字签名
* partner_key 老虎外汇分配给第三方的合作伙伴Key
* private_key 老虎外汇分配给第三方的合作伙伴私有Key
* partner_secret 老虎外汇分配给第三方的合作伙伴Secret

>注意:
>partner_key，private_key，partner_secret不能直接从网上申请，需通过老虎外汇合作渠道获取。
>要先申请测试，等待测试完成所有功能后，才可以申请线上key。

### <span id = "fangshi">加密方式</span>
>传递的所有字段拼接字符串排序后使用md5加密。
>在生成API请求中的签名(signature)时，需要提供账户中的public_key,partner_key和partner_secret。
##### php示例:

```
<?php 
$private_key    = 'demo_key'; #私有key
$partner_key    = 'partner_key'; #合作伙伴Key
$partner_secret = 'partner_secret'; #合作伙伴Secret
$signature      = '46f09bb9fab4f12dfc160dae12273d5332b5debe'; #签名
?>
```

PHP生成签名代码示例:
```
<?php 
/**
 * @param string $private_key | 私有key
 * @param array $params | 加密参数
 *
 * @return string 签名
 */
function get_verify_ac($private_key, $params) 
{
    ksort($params); # 参数串排序
    $params_data = "";
    foreach($params as $key => $value) {
        $params_data .= $key;
        $params_data .= $value;
    }
    $params_data .= $private_key;
    return md5($params_data); # 生成的Signature值
}
?>
```

CURL请求HTTP(S)：
```
<?php
function curl_request($mothed, $url, $params = array())
{
       $is_post = false;
        if (strtolower($mothed) == "post") {
            $is_post = true;
        }
        $ssl = substr($url, 0, 8) == "https://" ? TRUE : FALSE;
        $ch = curl_init();
        curl_setopt($ch, CURLOPT_POST, $is_post);
        if($is_post) {
            $fields_string = http_build_query ( $params, '&');
            curl_setopt($ch, CURLOPT_POSTFIELDS,$fields_string);
        } else if(! empty($params)) {
            $url = rtrim($url,"/?");
            $uri = http_build_query($params);
            $url = "{$url}?$uri";
        }
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
        curl_setopt($ch, CURLOPT_URL, $url);
        if ($ssl) {
          curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, 2);
          curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, true);
        }
        curl_setopt($ch, CURLOPT_HEADER, "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)");
        $content = curl_exec($ch);
        curl_close($ch);
        return $content;
}
?>
```

PHP 生成签名代码 CURL请求HTTP(S) 实例
```
<?php
$params['private_key']    = 'test';
$params['partner_key']    = 'test';
$params['partner_secret'] = 'test';
$params['action']         = 'signup';
$params['phone']          = $phone;
$params['user_id']        = $user_id;

$signature = get_verify_ac($params['private_key'], $params); #生成签名
$params['signature'] = $signature; 
unset($params['partner_key']); # 销毁加密key
unset($params['partner_secret']); # 销毁加密key
$path = "http://demo.tigerwit.com/action/public/api/signup"; //测试
# $path = "https://api.tigerwit.com/action/public/api/signup"; //线上
$data = curl_request('post',  $path, $params); #CURL请求HTTP(S)
?>
```

## 功能:
#### <span id = "liucheng">处理流程</span>
* 用户在第三方网站开户
* 用户在第三方网站访问高手列表
* 用户在第三方网站复制高手(前提为已充值足够金额)
* 高手在老虎外汇下单,用户在老虎外汇自动下单
* 获取报价推送
* 用户挂单
* 用户设置止盈，止损
* 用户在第三方网站查看账户盈亏,持仓明细
* 高手在老虎外汇平仓,用户所跟订单自动平仓(用户在第三方网站取消复制高手,强制平仓)
* 用户在第三方网站查看收益
* 用户申请入金，出金

#### <span id = "tongxin"> 通信方式 </span>
测试服务器采用http方式，正式服务器采用https方式。
#### <span id = "fanhui"> 返回格式 </span>
返回结果统一为json格式,如下实例:
```

{ 
"data":[ 
{ 
"username":"测试ceshi", 
"usercode":"525100" 
} 
], 
"error_code":0, //0表示成功,其他表示错误 
"error_msg":"", //错误信息 
"is_succ":true //接口返回成功 
} 
```

<center> [返回顶部](#top) </center>     





