---
title: BitExchange API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://www.byte-trade.com'>Exchange</a>
includes:
  - errors

search: true
---

# Introduction

Welcome to the ByteTrade API! You can use our API to access ByteTrade API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.


# APIs

## Get all Supported Currencies

```shell
curl "https://api-v2.byte-trade.com/currencies"
```

> The above command returns JSON structured like this:



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

> The above command returns JSON structured like this:



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




## 市场行情

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/tickers"
```

> The above command returns JSON structured like this:



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
symbol | String | unique id, unique.
name | String | string symbol of the market, non-unique.
base | String | base coin id.
quote | String | quote coin id.
timestamp | Long |int (64-bit Unix Timestamp in milliseconds since Epoch 1 Jan 1970).
datetime | Date | ISO8601 datetime string with milliseconds.
high | String | highest price.
low | String | lowest price.
open | String | opening price.
close | String | price of last trade (closing price for current period).
last | String | same as `close`, duplicated for convenience.
change | String | absolute change, `last - open`.
percentage | String | relative change, `(change/open) * 100`.
baseVolume | String | volume of base currency traded for last 24 hours.
quoteVolume | String | volume of quote currency traded for last 24 hours.



## 深度

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/depth"
```

> The above command returns JSON structured like this:



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
bids | Array | [[price,amount]]
asks | Array | [[price,amount]]
timestamp | String | 
datetime | String | 

