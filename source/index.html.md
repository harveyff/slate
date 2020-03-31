---
title: ByteTrade API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='#'>English</a>
  - <a href='#'>中文</a>
includes:
  - errors

search: true
---

# 说明

Welcome to the ByteTrade API! You can use our API to access ByteTrade API endpoints。

We have language bindings in Shell, You can view code examples in the dark area to the right.




# 基础信息

## Get all Supported Currencies

```shell
curl "https://api-v2.byte-trade.com/currencies"
```




This endpoint retrieves a specific kitten.


### HTTP Request

`GET https://api-v2.bytetrade.com/currencies`

### Request Parameters

No parameter is needed for this endpoint.


> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
name | String | If set to false, the result will include have already been adopted.
code | String | If set to false, the result will include kittens that have already been adopted.
type | Int | If set to false, the result wil.
fullname | Int | If set to false, the result will incluy been adopted.
active | Int | If set to false, the result will incluy been adopted.
basePrecision | Int | If set to false, the result will incluy been adopted.
transferPrecision | Int | If set to false, the result will incluy been adopted.
externalPrecision | Int | If set to false, the result will incluy been adopted.
fee | Int | If set to false, the result will incluy been adopted.
limits | Object | If set to false, the result will incluy been adopted.




## Get all Supported Symbols

```shell
curl "https://api-v2.byte-trade.com/symbols"
```


This endpoint retrieves a specific kitten.


### HTTP Request

`GET https://api-v2.bytetrade.com/symbols`

### Request Parameters

No parameter is needed for this endpoint.


> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
symbol | String | If set to false, the result will include have already been adopted.
name | String | If set to false, the result will include kittens that have already been adopted.
base | String | If set to false, the result wil.
quote | String | If set to false, the result will incluy been adopted.
marketStatus | Int | If set to false, the result will incluy been adopted.
baseName | String | If set to false, the result will incluy been adopted.
quoteName | String | If set to false, the result will incluy been adopted.
active | Boolean | If set to false, the result will incluy been adopted.
maker | String | If set to false, the result will incluy been adopted.
taker | String | If set to false, the result will incluy been adopted.
precision | Object | If set to false, the result will incluy been adopted.
limits | Object | If set to false, the result will incluy been adopted.


# 市场信息

## 市场行情

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/tickers"
```


查询全部symbol或单个symbol的24小时的价格变化

### HTTP Request

`GET https://api-v2.bytetrade.com/tickers`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |Long| false | NA|交易对symbol|


> Response:

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
        "change": "2.6e-05",                    
        "percentage": "0.084",                  
        "baseVolume": "209771.771",             
        "quoteVolume": "6519.97393184"          
      }
]...]
```

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
symbol | String | unique id, unique
name | String | string symbol of the market, non-unique
base | String | base asset id
quote | String | quote asset id
timestamp | Long |(64-bit Unix Timestamp in milliseconds since Epoch 1 Jan 1970)
datetime | Date | ISO8601 datetime string with milliseconds
high | String | highest price
low | String | lowest price
open | String | opening price
close | String | price of last trade (closing price for current period)
last | String | same as `close`, duplicated for convenience
change | String | absolute change, `last - open`
percentage | String | relative change, `(change/open) * 100`
baseVolume | String | volume of base currency traded for last 24 hours
quoteVolume | String | volume of quote currency traded for last 24 hours



## 深度

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/depth"
```

查询单个symbol的市场深度行情

### HTTP Request

`GET https://api-v2.bytetrade.com/depth?symbol=68719476706`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |Long| true | NA|交易对symbol|
limit |Int| false |20 |asks或bids个数|[1,100]
type |String|false | step0|深度的价格聚合度，step0时无聚合，step1\2\3\4\5分别代表聚合度为报价精度*10\100\1000\10000\100000|step0|step0，step1，step2，step3，step4，step5


> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
bids | Array | 当前最新的卖单价和卖单量[[price,amount]]
asks | Array | 当前最新的买单价和买单量[[price,amount]]
timestamp | String | 
datetime | String | 



## K线数据(蜡烛图)

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/klines"
```

查询单个symbol的市场深度行情

### HTTP Request

`GET https://api-v2.bytetrade.com/klines?symbol=68719476706`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |Long| true | NA|交易对symbol|
timeframe |String| true | |K线类型		|1m, 5m,15m,30m,1h,4h,1d,5d,1w,1M
since |Long| false |NA |K线开始时间(utc毫秒)，如果不设置这个值，则默认获取从当前时刻向前的limit个记录	|
limit |Int| false |100 |返回数据的条数|[1,500]


> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 | Long | UTC timestamp in milliseconds,
 | String | (O)pen price, String
 | String | (H)ighest price
 | String | (L)owest price
 | String | (C)losing price
 | String | (L)owest price
 | String | (V)olume (in terms of the base currency)

## 市场最新交易

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/trades"
```

查询单个symbol的市场深度行情

### HTTP Request

`GET https://api-v2.bytetrade.com/klines?symbol=68719476706`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |Long| true | NA|交易对symbol|
since |Long| false |NA |开始时间(utc毫秒)，如果不设置这个值，则默认获取从当前时刻向前的limit个记录	|
limit |Int| false |100 |返回数据的条数|[1,500]


> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 id| String |  trade id
 txid| String | transaction id in bytetrade
 timestamp| Long | Unix timestamp in milliseconds
 datetime| String | ISO8601 datetime with milliseconds
 symbol| String | symbol id
 name| String | symbol name
 side| String | direction of the trade, "buy" or "sell"
 price| String | price in quote currency
 amount| String | amount of base currency
 cost| String |  amount of quote currency



## 获取用户balance

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/balance"
```

查询单个symbol的市场深度行情

### HTTP Request

`GET https://api-v2.bytetrade.com/balance?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |String| true | NA|用户id|



> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 code| String | asset id
 name| String | asset name
 free| Long | money available for trading
 used| String | money on hold, locked, frozen or pending
 total| String | total balance (free + used)

# 用户订单

## 获取用户的所有订单

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/all"
```

查询单个用户的所有订单

### HTTP Request

`GET https://api-v2.bytetrade.com/orders/all?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |String| true | NA|用户id|
symbol |Long| false | NA|交易对symbol|
since |Long| false |NA |开始时间(utc毫秒)，如果不设置这个值，则默认获取从当前时刻向前的limit个记录	|
limit |Int| false |100 |返回数据的条数|[1,500]



> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 id| String | order id
 txid| String | transaction id in bytetrade
 timestamp| Long | Unix timestamp in milliseconds
 datetime| String | ISO8601 datetime with milliseconds
 lastTradeTimestamp| Long | Unix timestamp of the most recent trade on this order
 status| String |order status(open/closed/cancelled)
 symbol| String |symbol id
 name| String |symbol name
 type| String |order type(market/limit)
 side| String |order side(sell/buy)
 price| String | float price in quote currency
 average| String |
 amount| String |ordered amount of base currency
 filled| String |filled amount of base currency
 remaining| String |remaining amount to fill
 cost| String |"filled" * "price" (filling price used where available)
 fee| Object |-
 
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| String | which currency the fee is (usually quote)
  name| String | 
  cost| String | the fee amount in that currency
  rate| String | the fee rate (if available)


## 获取用户的委托订单

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/open"
```

查询单个用户的委托订单

### HTTP Request

`GET https://api-v2.bytetrade.com/orders/open?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |String| true | NA|用户id|
symbol |Long| false | NA|交易对symbol|
since |Long| false |NA |开始时间(utc毫秒)，如果不设置这个值，则默认获取从当前时刻向前的limit个记录	|
limit |Int| false |100 |返回数据的条数|[1,500]



> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 id| String | order id
 txid| String | transaction id in bytetrade
 timestamp| Long | Unix timestamp in milliseconds
 datetime| String | ISO8601 datetime with milliseconds
 lastTradeTimestamp| Long | Unix timestamp of the most recent trade on this order
 status| String |order status(open/closed/cancelled)
 symbol| String |symbol id
 name| String |symbol name
 type| String |order type(market/limit)
 side| String |order side(sell/buy)
 price| String | float price in quote currency
 average| String |
 amount| String |ordered amount of base currency
 filled| String |filled amount of base currency
 remaining| String |remaining amount to fill
 cost| String |"filled" * "price" (filling price used where available)
 fee| Object |-
 
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| String | which currency the fee is (usually quote)
  name| String | 
  cost| String | the fee amount in that currency
  rate| String | the fee rate (if available)



## 获取用户的已成交订单

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/closed"
```

查询单个用户的已成交订单

### HTTP Request

`GET https://api-v2.bytetrade.com/orders/closed?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |String| true | NA|用户id|
symbol |Long| false | NA|交易对symbol|
since |Long| false |NA |开始时间(utc毫秒)，如果不设置这个值，则默认获取从当前时刻向前的limit个记录	|
limit |Int| false |100 |返回数据的条数|[1,500]



> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 id| String | order id
 txid| String | transaction id in bytetrade
 timestamp| Long | Unix timestamp in milliseconds
 datetime| String | ISO8601 datetime with milliseconds
 lastTradeTimestamp| Long | Unix timestamp of the most recent trade on this order
 status| String |order status(open/closed/cancelled)
 symbol| String |symbol id
 name| String |symbol name
 type| String |order type(market/limit)
 side| String |order side(sell/buy)
 price| String | float price in quote currency
 average| String |
 amount| String |ordered amount of base currency
 filled| String |filled amount of base currency
 remaining| String |remaining amount to fill
 cost| String |"filled" * "price" (filling price used where available)
 fee| Object |-
 
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| String | which currency the fee is (usually quote)
  name| String | 
  cost| String | the fee amount in that currency
  rate| String | the fee rate (if available)



## 用户成交明细

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/trades"
```

查询单个用户的成交明细

### HTTP Request

`GET https://api-v2.bytetrade.com/orders/trades?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |String| true | NA|用户id|
symbol |Long| false | NA|交易对symbol|
orderid |String| false | NA|order id|
since |Long| false |NA |开始时间(utc毫秒)，如果不设置这个值，则默认获取从当前时刻向前的limit个记录	|
limit |Int| false |100 |返回数据的条数|[1,500]



> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 id| String | order id
 txid| String | transaction id in bytetrade
 timestamp| Long | Unix timestamp in milliseconds
 datetime| String | ISO8601 datetime with milliseconds
 symbol| String |symbol id
 name| String |symbol name
 order| String |order id
 type| String |order type(market/limit)
 side| String |order side(sell/buy)
 price| String | float price in quote currency
 average| String |
 amount| String |ordered amount of base currency
 takerOrMaker| String |taker/marker
 cost| String |"filled" * "price" (filling price used where available)
 fee| Object |-
 
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| String | which currency the fee is (usually quote)
  name| String | 
  cost| String | the fee amount in that currency
  rate| String | the fee rate (if available)

# 充值提现

## 获取用户充提地址

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/depositaddress"
```

查询单个用户的成交明细

### HTTP Request

`GET https://api-v2.bytetrade.com/depositaddress?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |String| true | NA|用户id|
code |Int| false | NA|currency的code	|


> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 code| String | asset id
 name| String | asset name
 chainType| String | chain type
 address| String |  address in terms of requested currency
 tag| String |



## 获取用户提现记录

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/withdrawals"
```

查询单个用户的提现记录

### HTTP Request

`GET https://api-v2.bytetrade.com/withdrawals?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |String| true | NA|用户id|
code |Int| false | NA|currency的code	|
since |Long| false |NA |开始时间(utc毫秒)，如果不设置这个值，则默认获取从当前时刻向前的limit个记录	|
limit |Int| false |100 |返回数据的条数|[1,500]



> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 id| String | withdraw id
 txid| String | 
 timestamp| String | 
 datetime| String | 
 address| String |
 tag| String |
 amount| String |
 code| String |
 name| String |
 status| String |Description of withdrawal status
 statusCode| Int |Code value of withdrawal status
 updated| String |
 fee| Object |
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| String | which currency the fee is (usually quote)
  name| String | 
  cost| String | the fee amount in that currency
  rate| String | the fee rate (if available)


## 获取用户充值记录

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/deposits"
```

查询单个用户的充值记录

### HTTP Request

`GET https://api-v2.bytetrade.com/deposits?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |String| true | NA|用户id|
code |Int| false | NA|currency的code	|
since |Long| false |NA |开始时间(utc毫秒)，如果不设置这个值，则默认获取从当前时刻向前的limit个记录	|
limit |Int| false |100 |返回数据的条数|[1,500]



> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 id| String | 
 txid| String | 
 timestamp| String | 
 datetime| String | 
 address| String |
 tag| String |
 amount| String |
 code| String |
 name| String |
 status| String |Description of deposit status
 statusCode| Int |Code value of deposit status
 updated| String |
 fee| Object |
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| String | which currency the fee is (usually quote)
  name| String | 
  cost| String | the fee amount in that currency
  rate| String | the fee rate (if available)


## 充值提现状态说明

* Withdraw Status

Parameter  |Description
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

* Deposits Status

Parameter  |Description
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
   const webSocket = new WebSocket('wss://p2.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'deals.subscribe', params: ['122406567911']};
       webSocket.send(JSON.stringify(params));
   };
```

订阅单个市场的最新成交

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |String| true |NA|symbol id|

> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 method| String | subscribe method
 price| String | deal price
 time| Double | deal time
 id| String | deal id
 type| String | deal type(buy/sell)
 amount| String | deal amount

## 24小时成交涨跌

```javascript
   const webSocket = new WebSocket('wss://p2.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'today.update', params: ['4294967329','4294967297']};
       webSocket.send(JSON.stringify(params));
   };
```

订阅单个或多个市场的24成交涨跌

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |String| true |NA|symbol id|

> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 method| String | subscribe method
 volume| String | volume currency traded for last 24 hours
 deal| String | deal currency traded for last 24 hours
 open| String | opening price
 change| String | relative change
 high| String | highest price
 last| String | same as `close`, duplicated for convenience
 low| String | lowest price


## K线数据


```javascript
   const webSocket = new WebSocket('wss://p2.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'kline.subscribe', params: ['4294967329',60]};
       webSocket.send(JSON.stringify(params));
   };
```

订阅单个市场的K线数据

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |String| true |NA|symbol id|
period |Int| true |NA|k线周期|需要换算成秒。1min, 5min, 15min, 30min, 60min, 4hour, 1day, 1mon, 1week, 1year


> Response:

```json
{
	"method": "kline.update",
	"params": [
		[1585638600, "0.0000546", "0.00005458", "0.00005477", "0.00005458", "1573.6132", "0.086050753577", "CMT/ETH", 4294967329]
	],
	"id": null
}
```

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 | Long | UTC timestamp in milliseconds,
 | String | (O)pen price, String
 | String | (H)ighest price
 | String | (L)owest price
 | String | (C)losing price
 | String | (L)owest price
 | String | (V)olume (in terms of the base currency)



## 市场深度

```javascript
   const webSocket = new WebSocket('wss://p2.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'depth.subscribe', params: ['4294967329',10,"0.001"]};
       webSocket.send(JSON.stringify(params));
   };
```

订阅单个市场的K线数据

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |String| true |NA|symbol id|
limit |Int| true |NA|条数|
step |String| true |NA|深度聚合度| 0(不聚合)/0.1/0.001/0.0001/0.00001


> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
asks | Array | 当前最新的买单价和买单量[[price,amount]]
bids | Array | 当前最新的卖单价和卖单量[[price,amount]]
 
 
## 用户鉴权

```javascript
   const webSocket = new WebSocket('wss://p2.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'server.sign', params: ['test']};
       webSocket.send(JSON.stringify(params));
   };
```

用户鉴权，用户必须完成鉴权，才可以使用用户资产和用户余额的订阅

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |String| true |NA|user id|



> Response:

```json
{
	"error": null,
	"result": {
		"status": "success"
	},
	"id": 12345
}
```

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
status | String | server status
 
 
## 用户订单

```javascript
   const webSocket = new WebSocket('wss://p2.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'order.subscribe', params: ['122406567923']};
       webSocket.send(JSON.stringify(params));
   };
```


订阅用户订单，只会推送订阅后的订单数据。
<aside class="warning">
必须先完成用户鉴权
</aside>
### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |String| true |NA|symbol id|



> Response:

```json
{
	"method": "order.update",
	"params": [1, {
		"use_btt_as_fee": 0,
		"deal_fee": "0",
		"taker_fee": "0.0004",
		"price": "0.000918", // float price in quote currency
		"source": "",
		"deal_money": "0", //
		"deal_stock": "0", //
		"id": "3eef56799c81dfd0cf59eb49d65339d6435909e7",// order id
		"left": "22",//amount not deal
		"mtime": 1585640948.3282981,
		"type": 1,// order type(market/limit)
		"side": 2,// order side(sell/buy)
		"market": "BHT/USDT",//symbol name
		"tid": "db91c645b609e1733e43f5b00a99db5dbbca6d9d",// transaction id in bytetrade
		"freeze_btt_fee": 0.0,
		"amount": "22",// order amount
		"user": "test",// user id
		"ctime": 1585640948.3282981,
		"maker_fee": "0.0004",// fee rate
		"dapp": "Sagittarius",//dapp id
		"market_id": 122406567923//symbol id
	}],
	"id": null
}
```

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
id | String | 
tid | String | 
user | String | 
deal_money | String | 
deal_stock | String | 
price | String | 
left | String | 
type | int | 
side | int | 
amount | String | 
ctime | String | 
maker_fee | String | 
dapp | String | 
market_id | String |
 
 
## 用户余额

```javascript
   const webSocket = new WebSocket('wss://p2.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'asset.subscribe2', params: [2,3]};
       webSocket.send(JSON.stringify(params));
   };
```

订阅用户一个或多个资产的余额变化
<aside class="warning">
必须先完成用户鉴权
</aside>
### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
asset |Int| true |NA|asset id|



> Response:

```json
{
	"method": "asset.update",
	"params": [{
		"2": ["0.001644065", "0.0026325", "0"]
	}, "harvey1712", 2],
	"id": null
}
```

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
 | String | available
 | String | frozen
 | String | pledge


## 心跳检测

```javascript
   const webSocket = new WebSocket('wss://p2.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'server.ping', params: []};
       webSocket.send(JSON.stringify(params));
   };
```

Websocket默认1小时断开连接，如果需要持续接收数据，请保持心跳。

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |String| true |NA|user id|



> Response:

```json
{
	"error": null,
	"result": {
		"status": "success"
	},
	"id": 12345
}
```

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
status | String | server status


## 取消订阅
与订阅类型，只是将"method"里的"subscribe"改为"unsubscribe",如取消最新成交

```javascript
   const webSocket = new WebSocket('wss://p2.byte-trade.com/ws/');
   webSocket.onopen = function(event) {
       var params={id: 12345, method: 'deals.unsubscribe', params: []};
       webSocket.send(JSON.stringify(params));
   };
```

