---
title: ByteTrade API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='https://doc.byte-trade.com'>English</a>
  - <a href='https://doc.byte-trade.com/cn'>中文</a>
includes:
  - errors

search: true
---

# 说明

欢迎使用ByteTrade API！您可以访问我们的API来使用ByteTrade链上相关服务。

在网页右侧有shell代码示例,您可以用代码示例进行测试。


# 基础信息

## 获取所有币种

```shell
curl "https://api-v2.byte-trade.com/currencies"
```

获取ByteTrade链上支持的所有币种

### HTTP Request

`GET https://api-v2.byte-trade.com/currencies`

### 请求参数

无

> 响应数据:

```json
[{
	"name": "ETH",
	"code": "2",
	"type": "crypto",
	"fullname": "Ethereum",
	"active": true,
	"chainType": "ethereum",
	"basePrecision": 18,
	"transferPrecision": 10,
	"externalPrecision": 18,
	"chainContractAddress": "0x0000000000000000000000000000000000000000",
	"fee": "",
	"limits": {
		"deposit": {
			"min": "0.01",
			"max": "-1"
		},
		"withdraw": {
			"min": "0.02",
			"max": "-1"
		}
	}
}...]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
name | string | 资产名
code | string | 资产id
type | int | 链类型
fullname |string| 资产全名
active | int |
basePrecision | int |  在ByteTrade链上,1个BTC将表示为1000000000000000000的整数
transferPrecision | int | 在ByteTrade链上,进行转账时,转账数量转成链上的整数后,最后8位(basePrecision-transferPrecision)为0,即至少转100000000的整数倍
externalPrecision | int | 在BTC的链上,最小单位为0.00000001
fee | string | 提现预估手续费汇率,仅适合BTC
limits | object | 

 * limits
 
 参数名 | 类型 |说明
 --------- | ------- | -----------
 deposit| object | 充值的最小值和最大值,-1代表不限
 withdraw| object | 提现的最小值和最大值,-1代表不限




## 获取所有交易对

```shell
curl "https://api-v2.byte-trade.com/symbols"
```


获取ByteTrade链上支持的所有交易对

### HTTP Request

`GET https://api-v2.byte-trade.com/symbols`

### 请求参数

无

> 响应数据:

```json
[{
	"symbol": "122406567911",
	"name": "BTC/USDT",
	"base": "32",
	"quote": "57",
	"marketStatus": 0,
	"baseName": "BTC",
	"quoteName": "USDT",
	"active": true,
	"maker": "0.0008",
	"taker": "0.0008",
	"precision": {
		"amount": 6,
		"price": 2
	},
	"limits": {
		"amount": {
			"min": "0.000001",
			"max": "-1"
		},
		"price": {
			"min": "0.01",
			"max": "-1"
		}
	}
}]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
symbol | string |交易对id,唯一
name | string | 交易对名称,非唯一
base | string | 基础货币id
quote | string | 计价货币id
marketStatus | int | 市场状态。0:闭市,1:开市
baseName | string | 基础货币名称
quoteName | string | 计价货币名称
active | Boolean | 
maker | string | maker 手续费
taker | string | taker 手续费
precision | object |
limits | object |

 * precision
 
 参数名 | 类型 |说明
 --------- | ------- | -----------
 amount| int | 交易时,amount的精度,代表小数点后的最大位数
 price| int | 交易时,price的精度,代表小数点后的最大位数

 * limits
 
 参数名 | 类型 |说明
 --------- | ------- | -----------
 amount| string | 限制base的最小值和最大值(当订单为限价买卖单或订单为市价卖单);限制quote的最小值和最大值(当订单为市价买单)
 price| string | 限制quote的最小值和最大值(当订单为限价买卖单或订单为市价卖单);限制base的最小值和最大值(当订单为市价买单)


# 市场信息

## 市场行情

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/tickers"
```


查询全部市场或单个市场的24小时的价格变化

### HTTP Request

`GET https://api-v2.byte-trade.com/tickers`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
symbol |long| false | NA|交易对id|


> 响应数据:

```json
[
      {
        "symbol": "68719476706",                 
        "name": "ETH/BTC",                       
        "base": "2",                             
        "quote": "32",                          
        "timestamp": 1559124034283,            
        "datetime": "2019-05-29T10:00:34.283Z",  
        "high": "0.031526",                        
        "low": "0.030771",                      
        "open": "0.031009",                     
        "close": "0.031035",                    
        "last": "0.031035",                     
        "change": "0.00654",                    
        "percentage": "0.084",                  
        "baseVolume": "209771.771",             
        "quoteVolume": "6519.97393184"          
      }
]...]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
symbol | string | 交易对id
name | string | 交易对名称
base | string | 基础货币id
quote | string | 计价货币id
timestamp | long |时间戳(毫秒)
datetime | Date | ISO格式的时间
high | string | 本阶段最高价
low | string | 本阶段最低价
open | string | 本阶段开盘价
close | string | 本阶段收盘价
last | string | 本阶段收盘价
change | string | 本阶段涨跌点(本阶段收盘价-本阶段开盘价)
percentage | string | 本阶段涨跌百分比, 本阶段涨跌点*100
baseVolume | string | 本阶段基础货币交易量
quoteVolume | string | 本阶段计价货币交易量



## 深度

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/depth"
```

查询单个symbol的市场深度行情

### HTTP Request

`GET https://api-v2.byte-trade.com/depth?symbol=68719476706`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
symbol |long| true | NA|交易对id|
limit |int| false |20 |买单或卖单个数|[1,100]
type |string|false | step0|深度的价格聚合度,step0时无聚合,step1\2\3\4\5分别代表聚合度为报价精度*10\100\1000\10000\100000|step0|step0,step1,step2,step3,step4,step5


> 响应数据:

```json
{
      "bids": [
        [
          "0.031138",  
          "0.05"       
        ],
        [
          "0.031137",
          "1.94"
        ],
        [
          "0.031136",
          "0.236"
        ]
       ],
      "asks": [
        [
          "0.031147",
          "14.237"
        ],
        [
          "0.031149",
          "0.033"
        ],
        [
          "0.03115",
          "0.417"
        ],
        [
          "0.031151",
          "0.755"
        ],
    "timestamp": 1559549045008,
    "datetime": "2019-06-03T08:04:05.008Z"
}
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
bids | Array | 当前最新的卖单价和卖单量[[price,amount]]
asks | Array | 当前最新的买单价和买单量[[price,amount]]
timestamp | string | 
datetime | string | 



## K线数据(蜡烛图)

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/klines"
```

查询单个symbol的市场深度行情

### HTTP Request

`GET https://api-v2.byte-trade.com/klines?symbol=68719476706`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
symbol |long| true | NA|交易对id|
timeframe |string| true | |K线类型		|1m, 5m,15m,30m,1h,4h,1d,5d,1w,1M
since |long| false |NA |K线开始时间(utc毫秒),如果不设置这个值,则默认获取从当前时刻向前的limit个记录	|
limit |int| false |100 |返回数据的条数|[1,500]


> 响应数据:

```json
[
    [
      1559574540000,    
      "0.030753",
      "0.030778",
      "0.030752",
      "0.030778",
      "30.716"   
    ]
]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 | long | 时间戳(毫秒)
 | string | (O)开盘价
 | string | (H)最高价
 | string | (L)最低价
 | string | (C)收盘价
 | string | (L)收盘价
 | string | (V)基础货币成交量

## 市场最新交易

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/trades"
```

查询单个市场的最新成交信息

### HTTP Request

`GET https://api-v2.byte-trade.com/klines?symbol=68719476706`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
symbol |long| true | NA|交易对id|
since |long| false |NA |开始时间(utc毫秒),如果不设置这个值,则默认获取从当前时刻向前的limit个记录	|
limit |int| false |100 |返回数据的条数|[1,500]


> 响应数据:

```json
[
    {
      "id": "6863a873ed87443bfc8bd759451d5c9ec4a2dafc",
      "txid":"909108605661dfd3e6d85ae2a9faceb524dce733",
      "order":"c3f463ccdd2afba372c78d3eb02d60e6913c1020,
      "timestamp": 1559633809458,
      "datetime": "2019-06-04T07:36:49.458Z",
      "symbol": "68719476706",
      "name": "ETH/BTC",
      "side": "buy",
      "price": "0.031118",
      "amount": "0.2379",
      "cost": "0.0074029722"
    }
]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 id| string |  id
 txid| string | 在ByteTrade链上的交易id
 timestamp| long | 交易时间(毫秒)
 datetime| string | ISO时间
 symbol| string | 交易对id
 name| string | 交易对名称
 side| string | 交易方向, buy或sell
 price| string | 成交价
 amount| string | 成交数量
 cost| string |  成交额


# 用户信息

## 获取用户资产余额

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/balance"
```

用户单个用户的资产余额

### HTTP Request

`GET https://api-v2.byte-trade.com/balance?userid=test`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|



> 响应数据:

```json
[
    {
      "code": "32",  
      "name": "BTC", 
      "free": "0.23",
      "used": "0.03",
      "total": "0.26"
    }
]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 code| string | 资产id
 name| string | 资产名称
 free| long | 可用资产
 used| string | 锁定资产
 total| string | 所有资产 (可用资产+ 锁定资产)

## 获取用户的所有订单

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/all"
```

查询单个用户的所有订单

### HTTP Request

`GET https://api-v2.byte-trade.com/orders/all?userid=test`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
symbol |long| false | NA|交易对id|
since |long| false |NA |开始时间(utc毫秒),如果不设置这个值,则默认获取从当前时刻向前的limit个记录	|
limit |int| false |100 |返回数据的条数|[1,500]



> 响应数据:

```json
[{
	"id": "3b50925018eef574e7b113a49aa515dc7249fe28",
	"txid": "d8b5cfcdf55f52c11fd85d6573d0b6c753cd7e35",
	"timestamp": 1585205369822,
	"userid": "harvey1712",
	"datetime": "2020-03-26T06:49:29.822Z",
	"lastTradeTimestamp": 1585205369822,
	"status": "closed",
	"symbol": "122406567923",
	"type": "market",
	"side": "sell",
	"price": "0",
	"amount": "0.004",
	"filled": "0.004",
	"remaining": "0",
	"cost": "0.000004012",
	"average": "0.001003",
	"fee": {
		"cost": "0.0000000016048",
		"rate": "0.0004",
		"code": 57,
		"name": "USDT"
	},
	"name": "BHT/USDT"
}]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 id| string | 订单id
 txid| string | ByteTrade链上的交易id
 timestamp| long | 创建时间(毫秒)
 datetime| string | ISO时间
 lastTradeTimestamp| long | 最后交易时间(毫秒)
 status| string |订单状态(open/closed/cancelled)
 symbol| string |交易对id
 name| string |交易对名称
 type| string |订单类型,限价单:limit,市场价:market
 side| string |订单方向(sell/buy)
 price| string | 成交价(当市价单时成交价为"0")
 average| string |成交均价
 amount| string |订单amount
 filled| string |已成交
 remaining| string |未成交
 cost| string |成交额(已成交*price)
 fee| object |-
 
 * fee
 
 参数名 | 类型 |说明
 --------- | ------- | -----------
  code| string |资产id
  name| string |资产名称
  cost| string |手续费
  rate| string |手续费比例


## 获取用户的委托订单

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/open"
```

查询单个用户的委托订单

### HTTP Request

`GET https://api-v2.byte-trade.com/orders/open?userid=test`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
symbol |long| false | NA|交易对id|
since |long| false |NA |开始时间(utc毫秒),如果不设置这个值,则默认获取从当前时刻向前的limit个记录	|
limit |int| false |100 |返回数据的条数|[1,500]



> 响应数据:

```json
[{
	"id": "3b50925018eef574e7b113a49aa515dc7249fe28",
	"txid": "d8b5cfcdf55f52c11fd85d6573d0b6c753cd7e35",
	"timestamp": 1585205369822,
	"userid": "harvey1712",
	"datetime": "2020-03-26T06:49:29.822Z",
	"lastTradeTimestamp": 1585205369822,
	"status": "closed",
	"symbol": "122406567923",
	"type": "market",
	"side": "sell",
	"price": "0",
	"amount": "0.004",
	"filled": "0.004",
	"remaining": "0",
	"cost": "0.000004012",
	"average": "0.001003",
	"fee": {
		"cost": "0.0000000016048",
		"rate": "0.0004",
		"code": 57,
		"name": "USDT"
	},
	"name": "BHT/USDT"
}]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 id| string | 订单id
 txid| string | ByteTrade链上的交易id
 timestamp| long | 创建时间(毫秒)
 datetime| string | ISO时间
 lastTradeTimestamp| long | 最后交易时间(毫秒)
 status| string |订单状态(open/closed/cancelled)
 symbol| string |交易对id
 name| string |交易对名称
 type| string |订单类型,限价单:limit,市场价:market
 side| string |订单方向(sell/buy)
 price| string | 成交价(当市价单时成交价为"0")
 average| string |成交均价
 amount| string |订单amount
 filled| string |已成交
 remaining| string |未成交
 cost| string |成交额(已成交*price)
 fee| object |-
 
 * fee
 
 参数名 | 类型 |说明
 --------- | ------- | -----------
  code| string |资产id
  name| string |资产名称
  cost| string |手续费
  rate| string |手续费比例



## 获取用户的已成交订单

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/closed"
```

查询单个用户的已成交订单

### HTTP Request

`GET https://api-v2.byte-trade.com/orders/closed?userid=test`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
symbol |long| false | NA|交易对id|
since |long| false |NA |开始时间(utc毫秒),如果不设置这个值,则默认获取从当前时刻向前的limit个记录	|
limit |int| false |100 |返回数据的条数|[1,500]



> 响应数据:

```json
[{
	"id": "3b50925018eef574e7b113a49aa515dc7249fe28",
	"txid": "d8b5cfcdf55f52c11fd85d6573d0b6c753cd7e35",
	"timestamp": 1585205369822,
	"userid": "harvey1712",
	"datetime": "2020-03-26T06:49:29.822Z",
	"lastTradeTimestamp": 1585205369822,
	"status": "closed",
	"symbol": "122406567923",
	"type": "market",
	"side": "sell",
	"price": "0",
	"amount": "0.004",
	"filled": "0.004",
	"remaining": "0",
	"cost": "0.000004012",
	"average": "0.001003",
	"fee": {
		"cost": "0.0000000016048",
		"rate": "0.0004",
		"code": 57,
		"name": "USDT"
	},
	"name": "BHT/USDT"
}]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
  id| string | 订单id
  txid| string | ByteTrade链上的交易id
  timestamp| long | 创建时间(毫秒)
  datetime| string | ISO时间
  lastTradeTimestamp| long | 最后交易时间(毫秒)
  status| string |订单状态(open/closed/cancelled)
  symbol| string |交易对id
  name| string |交易对名称
  type| string |订单类型,限价单:limit,市场价:market
  side| string |订单方向(sell/buy)
  price| string | 成交价(当市价单时成交价为"0")
  average| string |成交均价
  amount| string |订单amount
  filled| string |已成交
  remaining| string |未成交
  cost| string |成交额(已成交*price)
  fee| object |-
  
  * fee
  
  参数名 | 类型 |说明
  --------- | ------- | -----------
   code| string |资产id
   name| string |资产名称
   cost| string |手续费
   rate| string |手续费比例



## 用户成交明细

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/trades"
```

查询单个用户的成交明细

### HTTP Request

`GET https://api-v2.byte-trade.com/orders/trades?userid=test`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
symbol |long| false | NA|交易对id|
orderid |string| false | NA|order id|
since |long| false |NA |开始时间(utc毫秒),如果不设置这个值,则默认获取从当前时刻向前的limit个记录	|
limit |int| false |100 |返回数据的条数|[1,500]



> 响应数据:

```json
[
    {
        "id":           "3b185509047d385381fa1ec4d975ebb0d41c97c3", 
        "txid":         "909108605661dfd3e6d85ae2a9faceb524dce733", 
        "timestamp":    1502962946216,                              
        "datetime":     "2017-08-17 12:42:48.000",                  
        "symbol":       "4294967297",                               
        "name":         "ETH/BTC",                                  
        "order":        "d891f26f8cbc08e27434eb9ab9fb937ee1e7e438", 
        "side":         "sell",                                     
        "type":         "limit",                                    
        "takerOrMaker": "taker",                                    
        "price":        "0.00007412",                               
        "amount":       "27.29041663",                              
        "cost":         "0.0020227656806156",                       
        "fee":          {                                           
            "cost":  "0.0000016182125445",                          
            "code": "32",                                           
            "name": "BTC",
            "rate": 0.002,                                          
        }
    }
]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 id| string | 成交id
 txid| string | ByteTrade链上交易id
 timestamp| long | 成交时间(毫秒)
 datetime| string | ISO时间
 symbol| string |交易对id
 name| string |交易对名称
 order| string |订单id
 type| string |订单类型,限价单:limit,市场价:market
 side| string |订单方向(sell/buy)
 price| string | 成交价
 average| string |成交均价
 amount| string |成交量
 takerOrMaker| string |taker/marker
 cost| string |成交额（amount*price）
 fee| object |-
 
 * fee
 
 参数名 | 类型 |说明
 --------- | ------- | -----------
   code| string |资产id
   name| string |资产名称
   cost| string |手续费
   rate| string |手续费比例

# 充值提现

## 获取用户充值地址

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/depositaddress"
```

查询单个用户的充值地址

### HTTP Request

`GET https://api-v2.byte-trade.com/depositaddress?userid=test`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
code |int| false | NA|资产id	|


> 响应数据:

```json
[
    {
        "code": "2",                                            
        "name": "ETH",
        "chainType":"ethereum",                                 
        "address": "0x10c03cde1395e8e1e7626b890384c9897f7f597b",
        "tag": ""                                               
    }
]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 code| string | 资产id
 name| string | 资产名称
 chainType| string | 链类型
 address| string |  充值地址
 tag| string |



## 获取用户提现记录

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/withdrawals"
```

查询单个用户的提现记录

### HTTP Request

`GET https://api-v2.byte-trade.com/withdrawals?userid=test`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
code |int| false | NA|currency的code	|
since |long| false |NA |开始时间(utc毫秒),如果不设置这个值,则默认获取从当前时刻向前的limit个记录	|
limit |int| false |100 |返回数据的条数|[1,500]



> 响应数据:

```json
[
    {
      "id": "e523e01b778e377c9bbc3a883305409c3774efb1",                             
      "txid": "0xc42f1611d795cb5a9bda63af4a9fd28c7958a18d908bf1750ccfea9ace88d48f
      "timestamp": 1553134089103,                                                  
      "datetime": "2019-03-21T02:08:09.103Z",                                      
      "address": "0x32d74896f05204d1b6ae7b0a3cebd7fc0cd8f9c7",                   
      "tag": "",                                                                  
      "type": "withdrawal",                         
      "amount": 10,                                       
      "code": "3",     
      "name": "KCASH",                                                         
      "status": "SUCCEED",    
      "statusCode": 8,                                   
      "updated": 1553134584448,                          
      "fee": {                                   
        "code": "3",    
        "name": "KCASH",                      
        "cost": "0",                            
        "rate": "0"
      }
    }
]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 id| string | id
 txid| string | ByteTrade链上的交易id
 timestamp| string | 创建时间(毫秒)
 datetime| string | ISO时间
 address| string | 提现地址
 tag| string |
 amount| string | 提现数量
 code| string | 资产id
 name| string | 资产名称
 status| string |提现状态说明
 statusCode| int |提现状态码(参考充提状态码)
 updated| string |
 fee| object |
 * fee
 
 参数名 | 类型 |说明
 --------- | ------- | -----------
   code| string |资产id
   name| string |资产名称
   cost| string |手续费
   rate| string |手续费比例


## 获取用户充值记录

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/deposits"
```

查询单个用户的充值记录

### HTTP Request

`GET https://api-v2.byte-trade.com/deposits?userid=test`

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
code |int| false | NA|currency的code	|
since |long| false |NA |开始时间(utc毫秒),如果不设置这个值,则默认获取从当前时刻向前的limit个记录	|
limit |int| false |100 |返回数据的条数|[1,500]



> 响应数据:

```json
[
    {
      "id": "e523e01b778e377c9bbc3a883305409c3774efb1",                             
      "txid": "0xc42f1611d795cb5a9bda63af4a9fd28c7958a18d908bf1750ccfea9ace88d48f", 
      "timestamp": 1553134089103,                                                  
      "datetime": "2019-03-21T02:08:09.103Z",                                      
      "address": "0x32d74896f05204d1b6ae7b0a3cebd7fc0cd8f9c7",                   
      "tag": "",                                                                  
      "type": "deposit",                         
      "amount": 10,                                       
      "code": "3",     
      "name": "KCASH",                                                         
      "status": "succeed",                              
      "statusCode": 10,                              
      "updated": 1553134584448,                          
      "fee": {                                   
        "code": "3",    
        "name": "KCASH",                      
        "cost": "0",                            
        "rate": "0"
      }
    }
]
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 id| string | 
 txid| string | ByteTrade链上的交易id
 timestamp| string | 创建时间(毫秒)
 datetime| string | ISO时间
 address| string |充值地址
 tag| string |
 amount| string |充值数量
 code| string | 资产id
 name| string | 资产名称
 status| string |充值状态说明
 statusCode| int |充值状态码(参考充提状态码)
 updated| string |
 fee| object |
 * fee
 
 参数名 | 类型 |说明
 --------- | ------- | -----------
   code| string |资产id
   name| string |资产名称
   cost| string |手续费
   rate| string |手续费比例



## 充值提现状态码说明

* 提现状态码

状态码  |含义
---------  | -----------
3|FEE_PAID              
2|FEE_SEND_FAILED       
4|FEE_FAILED                
13|UNLOKING         
14|UNLOCK_FAILED        
5|EXECUTING             
8|SUCCEED                
6|WITHDRAW_FAILED      
7|FAILED                       
101|BELOW_THE_MINIMUM 

* 充值状态码

状态码  |含义
---------  | -----------
3|FEE_PAID              
2|FEE_SEND_FAILED       
4|FEE_FAILED                
5|LOCKING               
8|LOCK_SUCCEED       
6|LOCK_SEND_FAILED     
7|LOCK_FAILED              
9|FAILED                      
10|SUCCEED        
31|BELOW_THE_MINIMUM 

# Websocket

## 市场最新成交

```javascript
   const webSocket = new WebSocket('wss://api.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'deals.subscribe', params: ['122406567911']};
       webSocket.send(JSON.stringify(params));
   };
```

订阅单个市场的最新成交

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
symbol |string| true |NA|交易对id|

> 响应数据:

```json
{
	"method": "deals.update",
	"params": ["122406567911", [{
		"price": "6397.86",
		"time": 1585634793.734211,
		"id": "25f82ee8592fa8a0a806da8b5ad65b92fc0dc6a0",
		"type": "buy",
		"amount": "0.000023"
	}]],
	"id": null
}
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 method| string | 订阅方式
 price| string | 价格
 time| Double | 时间
 id| string | 
 type| string | 成交方向(buy/sell)
 amount| string | 成交数量

## 24小时成交涨跌

```javascript
   const webSocket = new WebSocket('wss://api.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'today.update', params: ['4294967329','4294967297']};
       webSocket.send(JSON.stringify(params));
   };
```

订阅单个或多个市场的24成交涨跌

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
symbol |string| true |NA|交易对id|

> 响应数据:

```json
{
	"method": "today.update",
	"params": [4294967329, {
		"volume": "998178.85873774",
		"deal": "53.6595488505712682",
		"open": "0.00005326",
		"change": "1.02327327",
		"high": "0.00005501",
		"last": "0.00005452",
		"low": "0.00005309"
	}],
	"id": null
}
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 method| string | 
 volume| string | 成交数量
 deal| string | 成交额
 open| string | 开盘价
 change| string | 涨跌幅
 high| string | 最高价
 last| string | 收盘价
 low| string | 收盘价


## K线数据


```javascript
   const webSocket = new WebSocket('wss://api.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'kline.subscribe', params: ['4294967329',60]};
       webSocket.send(JSON.stringify(params));
   };
```

订阅单个市场的K线数据

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
symbol |string| true |NA|交易对id|
period |int| true |NA|k线周期|需要换算成秒。1min, 5min, 15min, 30min, 60min, 4hour, 1day, 1mon, 1week, 1year


> 响应数据:

```json
{
	"method": "kline.update",
	"params": [
		[1585638600, "0.0000546", "0.00005458", "0.00005477", "0.00005458", "1573.6132", "0.086050753577", "CMT/ETH", 4294967329]
	],
	"id": null
}
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 | long | 时间(秒)
 | string | (O)开盘价
 | string | (H)最高价
 | string | (L)最低价
 | string | (C)收盘价
 | string | (L)收盘价
 | string | (V)成交量
 | string | 交易对名称
 | long | 交易对id



## 市场深度

```javascript
   const webSocket = new WebSocket('wss://api.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'depth.subscribe', params: ['4294967329',10,"0.001"]};
       webSocket.send(JSON.stringify(params));
   };
```

订阅单个市场的K线数据

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
symbol |string| true |NA|交易对id|
limit |int| true |NA|条数|
step |string| true |NA|深度聚合度| 0(不聚合)/0.1/0.001/0.0001/0.00001


> 响应数据:

```json
{
	"method": "depth.update",
	"params": [true, {
		"asks": [
			["0.00006", "5994.292598"],
			["0.00007", "2855.568381"]
		],
		"bids": [
			["0.00005", "8365.835532"],
			["0.00004", "7496.585197"]
		]
	}, "4294967329"],
	"id": null
}
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
asks | Array | 当前最新的买单价和买单量[[price,amount]]
bids | Array | 当前最新的卖单价和卖单量[[price,amount]]
 
 
## 用户鉴权

```javascript
   const webSocket = new WebSocket('wss://api.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'server.sign', params: ['test']};
       webSocket.send(JSON.stringify(params));
   };
```

用户鉴权,用户必须完成鉴权,才可以使用用户资产和用户余额的订阅

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true |NA|user id|



> 响应数据:

```json
{
	"error": null,
	"result": {
		"status": "success"
	},
	"id": 12345
}
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
status | string | server status
 
 
## 用户订单

```javascript
   const webSocket = new WebSocket('wss://api.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'order.subscribe', params: ['122406567923']};
       webSocket.send(JSON.stringify(params));
   };
```


订阅用户订单,只会推送订阅后的订单数据。
<aside class="warning">
必须先完成用户鉴权
</aside>
### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
symbol |string| true |NA|交易对id|



> 响应数据:

```json
{
	"method": "order.update",
	"params": [1, {
		"use_btt_as_fee": 0,
		"deal_fee": "0",
		"taker_fee": "0.0004",
		"price": "0.000918", 
		"source": "",
		"deal_money": "0", 
		"deal_stock": "0", 
		"id": "3eef56799c81dfd0cf59eb49d65339d6435909e7",
		"left": "22",
		"mtime": 1585640948.3282981,
		"type": 1,
		"side": 2,
		"market": "BHT/USDT",
		"tid": "db91c645b609e1733e43f5b00a99db5dbbca6d9d",
		"freeze_btt_fee": 0.0,
		"amount": "22",
		"user": "test",
		"ctime": 1585640948.3282981,
		"maker_fee": "0.0004",
		"dapp": "Sagittarius",
		"market_id": 122406567923
	}],
	"id": null
}
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
id | string | 订单id
tid | string | ByteTrade链上的交易id
user | string | 用户id
deal_money | string | 已成交额
deal_stock | string | 已成交量
price | string | 价格
left | string | 未成交数量
type | int | 订单类型,限价单:limit,市场价:market
side | int | 订单方向(sell或buy)
amount | string | 订单数量
ctime | string | 创建时间(秒)
maker_fee | string | 手续费比例
dapp | string | 
market_id | string | 交易对id
 
 
## 用户余额

```javascript
   const webSocket = new WebSocket('wss://api.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'asset.subscribe2', params: [2,3]};
       webSocket.send(JSON.stringify(params));
   };
```

订阅用户一个或多个资产的余额变化
<aside class="warning">
必须先完成用户鉴权
</aside>
### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
asset |int| true |NA|asset id|



> 响应数据:

```json
{
	"method": "asset.update",
	"params": [{
		"2": ["0.001644065", "0.0026325", "0"]
	}, "harvey1712", 2],
	"id": null
}
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
 | string | 可用资产
 | string | 冻结资产
 | string | 抵押资产


## 心跳检测

```javascript
   const webSocket = new WebSocket('wss://api.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'server.ping', params: []};
       webSocket.send(JSON.stringify(params));
   };
```

Websocket默认1小时断开连接,如果需要持续接收数据,请保持心跳。

### 请求参数

参数名|类型	| 是否必须 |默认值| 说明|取值范围
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true |NA|user id|



> 响应数据:

```json
{
	"error": null,
	"result": {
		"status": "success"
	},
	"id": 12345
}
```

### 响应参数

参数名 | 类型 |说明
--------- | ------- | -----------
status | string | server status


## 取消订阅
与订阅类型,只是将"method"里的"subscribe"改为"unsubscribe",如取消最新成交：

```javascript
   const webSocket = new WebSocket('wss://api.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'deals.unsubscribe', params: []};
       webSocket.send(JSON.stringify(params));
   };
```

# 错误码含义

API错误码含义

错误码 | 含义
---------- | -------
400 | Bad Request
403 | Forbidden
404 | Not Found
405 | Method Not Allowed 
406 | Not Acceptable
429 | Too Many Requests
500 | Internal Server Error 
501 | Request Error 
503 | Service Unavailable 
