---
title: ByteTrade API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  
toc_footers:
  - <a href='https://doc.byte-trade.com'>English</a>

search: true
---

# Description

Welcome to the ByteTrade API! You can use our API to access ByteTrade API endpoints.

At the same time, we have access to [CCXT](https://github.com/ccxt/ccxt), it's a JavaScript / Python / PHP library,if you use these languages, you can use them easily,it supports more interfaces, such as withdraw.

## Access URLs
* REST API

  `https://api-v2.byte-trade.com`
  
* Websocket Feed       

  `https://api.byte-trade.com/ws/`                                                                                                                                                            

## Rate Limiting Rule
* Each IP is limited to 10 times per second

## Request Format

The API is restful and there are two method: GET and POST.

* GET request: All parameters are included in URL
* POST request: All parameters are formatted as JSON and put int the request body

## Error Http Status

The ByteTrade API use the following error http status:

Parameter | Description
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



# Basic Information

## Get all Supported Currencies

```shell
curl "https://api-v2.byte-trade.com/currencies"
```

This endpoint returns all ByteTrade's supported trading currencies.


### HTTP Request

`GET https://api-v2.byte-trade.com/currencies`

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
name | string | asset name
code | string | asset id
type | int | chain type
fullname |string| asset fullname
active | int |
basePrecision | int |  On ByteTrade blockchain, 1 BTC will be represented as an integer of 1000000000000000000
transferPrecision | int | On ByteTrade blockchain, when transferring, after the amount of transfer is converted to an integer on the chain, and the last 8 bits (basePrecision-transferPrecision) are 0, so need to transfer at least a multiple of 100000000
externalPrecision | int | On BTC blockchain, the minimum unit is 0.00000001
fee | string | withdraw fee, only valid for BTC
limits | object | 

 * limits
 
 Parameter | Type |Description
 --------- | ------- | -----------
 deposit| object | Minimum and maximum of deposit, -1 means unlimited
 withdraw| object | The minimum and maximum of withdrawal, -1 means unlimited




## Get all Supported Symbols

```shell
curl "https://api-v2.byte-trade.com/symbols"
```


This endpoint returns all ByteTrade's supported trading symbol.


### HTTP Request

`GET https://api-v2.byte-trade.com/symbols`

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
symbol | string |market symbol, unique
name | string | market symbol name, non-unique
base | string | base asset currency
quote | string | quote asset currency
marketStatus | int | market status,0 is closed,1 is open
baseName | string | base asset name
quoteName | string | quote asset code
active | Boolean | 
maker | string | maker fee
taker | string | taker fee
precision | object |
limits | object |

 * precision
 
 Parameter | Type |Description
 --------- | ------- | -----------
 amount| int |When trading, the precision of amount represents the maximum number of digits after the decimal point
 price| int | When trading, the precision of price represents the maximum number of digits after the decimal point

 * limits
 
 Parameter | Type |Description
 --------- | ------- | -----------
 amount| string | Limit the minimum and maximum of the base (when the order is a limit buy or sell order or the market sell order); limit the minimum and maximum of the quote (when the order is a market buy order)
 price| string | Limit the minimum and maximum of the quote (when the order is a limit buy or sell order or a market sell order); limit the minimum and maximum of the base (when the order is a market buy order)


# Market Data

## Get the Last 24h Market Summary

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/tickers"
```

This endpoint retrieves the summary of trading in the market for the last 24 hours.


### HTTP Request

`GET https://api-v2.byte-trade.com/tickers`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |long| false | NA|symbol id|


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
symbol | string | unique id, unique
name | string | string symbol of the market, non-unique
base | string | base asset id
quote | string | quote asset id
timestamp | long |(64-bit Unix Timestamp in milliseconds since Epoch 1 Jan 1970)
datetime | Date | ISO8601 datetime string with milliseconds
high | string | highest price
low | string | lowest price
open | string | opening price
close | string | price of last trade (closing price for current period)
last | string | same as `close`, duplicated for convenience
change | string | absolute change, `last - open`
percentage | string | relative change, `(change/open) * 100`
baseVolume | string | volume of base currency traded for last 24 hours
quoteVolume | string | volume of quote currency traded for last 24 hours



## Get Market Depth

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/depth"
```

This endpoint retrieves the current order book of a specific pair.

### HTTP Request

`GET https://api-v2.byte-trade.com/depth?symbol=68719476706`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |long| true | NA|symbol id|
limit |int| false |20 |numbre of asks or bids|[1,100]
type |string|false | step0|depth's price aggregation degree,no aggregation at step0,a step1/2/3/4/5 respectively represents the aggregation degree as the quote precision *10\100\1000\10000\100000|step0/step1/step2/step3/step4/step5


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
bids | Array | Current latest sell order price and sell order amount: [ [ price,amount ] ]
asks | Array | Current latest buy order price and buy order amount: [ [ price,amount ] ]
timestamp | string | 
datetime | string | 



## Get Kline(Candles)

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/klines"
```

This endpoint retrieves all klines in a specific range.

### HTTP Request

`GET https://api-v2.byte-trade.com/klines?symbol=68719476706`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |long| true | NA|symbol id|
timeframe |string| true | |K-line type|1m/5m/15m/30m/1h/4h/1d/5d/1w/1M
since |long| false |NA |start time of Kline(ms),If this value is not ,get limit records forward from the current moment by default	|
limit |int| false |100 |number of returned data|[1,500]


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

 Type |Description
 ------- | -----------
 long | UTC timestamp in milliseconds,
 string | (O)pen price, string
 string | (H)ighest price
 string | (L)owest price
 string | (C)losing price
 string | (L)owest price
 string | (V)olume (in terms of the base currency)

## Get the Last Trade

```shell
curl -d "symbol=68719476706" "https://api-v2.byte-trade.com/trades"
```

This endpoint retrieves market last trades of a single symbol.

### HTTP Request

`GET https://api-v2.byte-trade.com/klines?symbol=68719476706`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |long| true | NA|symbol id|
since |long| false |NA |start time (ms),If this value is not set,get the limit records forward from the current moment by default	|
limit |int| false |100 |number of returned data|[1,500]


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
 id| string |  trade id
 txid| string | transaction id in ByteTrade
 timestamp| long | Unix timestamp in milliseconds
 datetime| string | ISO8601 datetime with milliseconds
 symbol| string | symbol id
 name| string | symbol name
 side| string | direction of the trade, "buy" or "sell"
 price| string | price in quote currency
 amount| string | amount of base currency
 cost| string |  amount of quote currency


# Account
## Create Account

To create an account, please click "create" in the upper right corner of [ByteTrade](https://www.byte-trade.com/) website. 

<aside class="warning">
Please save your private key after creation.
</aside>


## Get Account Balance

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/balance"
```

This endpoint returns the balance of an account specified by account id.

### HTTP Request

`GET https://api-v2.byte-trade.com/balance?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|



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
 code| string | asset id
 name| string | asset name
 free| long | money available for trading
 used| string | money on hold,locked,frozen or pending
 total| string | total balance (free + used)

## Get All Orders

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/all"
```

This endpoint retrieves all orders of a single user.

### HTTP Request

`GET https://api-v2.byte-trade.com/orders/all?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
symbol |long| false | NA|symbol id|
since |long| false |NA |start time(ms),If this value is not set,get the limit records forward from the current moment by default |
limit |int| false |100 |number of returned data|[1,500]



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
 id| string | order id
 txid| string | transaction id in ByteTrade
 timestamp| long | Unix timestamp in milliseconds
 datetime| string | ISO8601 datetime with milliseconds
 lastTradeTimestamp| long | Unix timestamp of the most recent trade on this order
 status| string |order status(open/closed/cancelled)
 symbol| string |symbol id
 name| string |symbol name
 type| string |order type(market/limit)
 side| string |order side(sell/buy)
 price| string | float price in quote currency
 average| string |
 amount| string |ordered amount of base currency
 filled| string |filled amount of base currency
 remaining| string |remaining amount to fill
 cost| string |"filled" * "price" (filling price used where available)
 fee| object |-
 
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| string | which currency the fee is (usually quote)
  name| string | 
  cost| string | the fee amount in that currency
  rate| string | the fee rate (if available)


## Get All Open Orders

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/open"
```

This endpoint returns all open orders which have not been filled completely.


### HTTP Request

`GET https://api-v2.byte-trade.com/orders/open?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
symbol |long| false | NA|symbol id|
since |long| false |NA |start time(ms),If this value is not set,get the limit records forward from the current moment by default	|
limit |int| false |100 |number of returned data|[1,500]



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
 id| string | order id
 txid| string | transaction id in ByteTrade
 timestamp| long | Unix timestamp in milliseconds
 datetime| string | ISO8601 datetime with milliseconds
 lastTradeTimestamp| long | Unix timestamp of the most recent trade on this order
 status| string |order status(open/closed/cancelled)
 symbol| string |symbol id
 name| string |symbol name
 type| string |order type(market/limit)
 side| string |order side(sell/buy)
 price| string | float price in quote currency
 average| string |
 amount| string |ordered amount of base currency
 filled| string |filled amount of base currency
 remaining| string |remaining amount to fill
 cost| string |"filled" * "price" (filling price used where available)
 fee| object |-
 
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| string | which currency the fee is (usually quote)
  name| string | 
  cost| string | the fee amount in that currency
  rate| string | the fee rate (if available)



## Get History Orders

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/closed"
```

This endpoint retrieves history orders of a single user.

### HTTP Request

`GET https://api-v2.byte-trade.com/orders/closed?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
symbol |long| false | NA|symbol id|
since |long| false |NA |start time(ms),If this value is not se,get the limit records forward from the current moment by default	|
limit |int| false |100 |number of returned data|[1,500]



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
 id| string | order id
 txid| string | transaction id in ByteTrade
 timestamp| long | Unix timestamp in milliseconds
 datetime| string | ISO8601 datetime with milliseconds
 lastTradeTimestamp| long | Unix timestamp of the most recent trade on this order
 status| string |order status(open/closed/cancelled)
 symbol| string |symbol id
 name| string |symbol name
 type| string |order type(market/limit)
 side| string |order side(sell/buy)
 price| string | float price in quote currency
 average| string |
 amount| string |ordered amount of base currency
 filled| string |filled amount of base currency
 remaining| string |remaining amount to fill
 cost| string |"filled" * "price" (filling price used where available)
 fee| object |-
 
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| string | which currency the fee is (usually quote)
  name| string | 
  cost| string | the fee amount in that currency
  rate| string | the fee rate (if available)



## Get User Trades

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/orders/trades"
```

This endpoint get user order trade details.

### HTTP Request

`GET https://api-v2.byte-trade.com/orders/trades?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
symbol |long| false | NA|symbol id|
orderid |string| false | NA|order id|
since |long| false |NA |start time(ms),If this value is not set,get the limit records forward from the current moment by default	|
limit |int| false |100 |number of returned data|[1,500]



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
 id| string | order id
 txid| string | transaction id in ByteTrade
 timestamp| long | Unix timestamp in milliseconds
 datetime| string | ISO8601 datetime with milliseconds
 symbol| string |symbol id
 name| string |symbol name
 order| string |order id
 type| string |order type(market/limit)
 side| string |order side(sell/buy)
 price| string | float price in quote currency
 average| string |
 amount| string |ordered amount of base currency
 takerOrMaker| string |taker/marker
 cost| string |"filled" * "price" (filling price used where available)
 fee| object |-
 
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| string | which currency the fee is (usually quote)
  name| string | 
  cost| string | the fee amount in that currency
  rate| string | the fee rate (if available)

# Deposit And Withdraw

## Get Deposit Address

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/depositaddress"
```

This endpoint retrieves deposit address of a user.

### HTTP Request

`GET https://api-v2.byte-trade.com/depositaddress?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
code |int| false | NA|code of currency	|


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
 code| string | asset id
 name| string | asset name
 chainType| string | chain type
 address| string |  address in terms of requested currency
 tag| string |


## Withdraw

Please use [ccxt] (https://github.com/ccxt/ccxt) for user withdrawal, because we have a lot of chaintypes and assets, it is more convenient and quick to use ccxt without paying attention to these details.

## Get Withdraw History

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/withdrawals"
```

This endpoint retrieves withdrawal history of a user.

### HTTP Request

`GET https://api-v2.byte-trade.com/withdrawals?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
code |int| false | NA|currency的code	|
since |long| false |NA |start time(ms),If this value is not set,get the limit records forward from the current moment by default	|
limit |int| false |100 |number of returned data|[1,500]



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
 id| string | withdraw id
 txid| string | transaction id in ByteTrade
 timestamp| string | creation time (ms)
 datetime| string | ISO format time
 address| string | withdraw address
 tag| string |
 amount| string | withdraw amount
 code| string | asset id
 name| string | asset name
 status| string |description of withdrawal status
 statusCode| int |code value of withdrawal [status](#deposit-withdraw-status)
 updated| string |
 fee| object |
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| string | which currency the fee is (usually quote)
  name| string | 
  cost| string | the fee amount in that currency
  rate| string | the fee rate (if available)


## Get Deposit History

```shell
curl -d "userid=test" "https://api-v2.byte-trade.com/deposits"
```

This endpoint retrieves deposit record of a user.

### HTTP Request

`GET https://api-v2.byte-trade.com/deposits?userid=test`

### URL Parameters

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true | NA|user id|
code |int| false | NA|currency的code	|
since |long| false |NA |start time(utc milliseconds),If this value is not set,get 
 the limit records forward from the current moment by default	|
limit |int| false |100 |number of returned data|[1,500]

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
 id| string | deposit id
 txid| string |  transaction id in ByteTrade
 timestamp| string | creation time (ms)
 datetime| string | ISO format time
 address| string | deposit address
 tag| string |
 amount| string | deposit amount
 code| string | asset id
 name| string | asset name
 status| string | cescription of deposit status
 statusCode| int | code value of deposit [status](#deposit-withdraw-status)
 updated| string |
 fee| object |
 * fee
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| string | which currency the fee is (usually quote)
  name| string | 
  cost| string | the fee amount in that currency
  rate| string | the fee rate (if available)


## Deposit/Withdraw Status

* Withdraw Status

Code  |Description
---------  | -----------    
2|FEE_SEND_FAILED       
3|FEE_PAID 
4|FEE_FAILED                      
5|EXECUTING
6|WITHDRAW_FAILED      
7|FAILED  
8|SUCCEED                            
13|UNLOKING         
14|UNLOCK_FAILED  
101|BELOW_THE_MINIMUM 

* Deposits Status

Code  |Description
---------  | -----------
2|FEE_SEND_FAILED  
3|FEE_PAID                   
4|FEE_FAILED                
5|LOCKING
6|LOCK_SEND_FAILED     
7|LOCK_FAILED     
8|LOCK_SUCCEED                
9|FAILED                      
10|SUCCEED        
31|BELOW_THE_MINIMUM 

# Websocket

## Market Trades

```shell
  {id: 12345, method: 'deals.subscribe', params: ['122406567911']}
```

This topic sends the latest trades in a single market.

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |string| true |NA|symbol id|

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
 method| string | subscribe method
 price| string | deal price
 time| Double | deal time
 id| string | deal id
 type| string | deal type(buy/sell)
 amount| string | deal amount

## Last 24h Market Summary

```shell
  {id: 12345, method: 'today.update', params: ['4294967329','4294967297']}
```

This topic sends the rise or fall of 24-hour deals in a single or multiple markets.

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |string| true |NA|symbol id|

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
 method| string | subscribe method
 volume| string | volume currency traded for last 24 hours
 deal| string | deal currency traded for last 24 hours
 open| string | opening price
 change| string | relative change
 high| string | highest price
 last| string | same as `close`, duplicated for convenience
 low| string | lowest price


## Kline Data

```shell
  {id: 12345, method: 'kline.subscribe', params: ['4294967329',60]}
```

This topic sends the Kline data of a single market.

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |string| true |NA|symbol id|
period |int| true |NA|kline period|need to be converted into seconds。1min, 5min, 15min, 30min, 60min, 4hour, 1day, 1mon, 1week, 1year


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

  Type |Description
  ------- | -----------
  long | UTC timestamp in milliseconds,
  string | (O)pen price
  string | (H)ighest price
  string | (L)owest price
  string | (C)losing price
  string | (L)owest price
  string | (V)olume (in terms of the base currency)
  string | symbol name
  long | symbol id



## Market Depth

```shell
  {id: 12345, method: 'depth.subscribe', params: ['4294967329',10,"0.001"]}
```

This topic sends the latest market by price order book.

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |string| true |NA|symbol id|
limit |int| true |NA||
step |string| true |NA|depth aggregation degree| 0(no aggregation)/0.1/0.001/0.0001/0.00001


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
asks | Array | Current latest buy order price and order amount[[price,amount]]
bids | Array | current latest sell order price and order amount[[price,amount]]
 
 
## User Auth

```shell
  {id: 12345, method: 'server.sign', params: ['test']}
```

User appraises right,users must complete authentication before they can use subscriptions for user assets and user balances.

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true |NA|user id|



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
status | string | server status
 
 
## User Order

```shell
  {id: 12345, method: 'order.subscribe', params: ['122406567923']}
```

This topic sends user orders, only the order data after the subscription is pushed.

<aside class="warning">
must complete appraises right firstly
</aside>

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |string| true |NA|symbol id|

> Response:

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

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
id | string | order id
tid | string | transaction id in ByteTrade
user | string | user id
deal_money | string | deal money
deal_stock | string | deal stock 
price | string | order price
left | string | no deal amount
type | int | order type(limit/market)
side | int | order side(sell/buy)
amount | string | order amount
ctime | string | create time(second)
maker_fee | string | marker fee
dapp | string | dapp id
market_id | string | symbol id
 
 
## User Balance

```shell
  {id: 12345, method: 'asset.subscribe2', params: [2,3]}
```

This topic sends the changes in the balance of one or more assets of the user.

<aside class="warning">
must complete appraises right firstly
</aside>
### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
asset |int| true |NA|asset id|



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
 | string | available
 | string | frozen
 | string | pledge


## Heartbeat Detection

```shell
  {id: 12345, method: 'server.ping', params: []}
```

Websocket will disconnect by default for 1 hour. If need to continuously receive data, please keep the heartbeat.

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
userid |string| true |NA|user id|



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
status | string | server status


## Unsubscribe
And subscription type, just change "subscribe" in "method" to "unsubscribe", such as canceling the latest transaction：

```javascript
     {id: 12345, method: 'deals.unsubscribe', params: []}
```


# Transaction

## Create Order

Please use CCXT for order creation, which is more convenient and quick. The official [JS version](https://github.com/ccxt/ccxt/blob/master/examples/js/create-order-with-retry.js) is an example.

> CCXT example:

```javascript
    "use strict";
    const ccxt = require ('ccxt');
    var bytetrade = new ccxt.bytetrade(
        {
            'apiKey': '', // your account userid
            'secret': '' // your account private key
        }
    );
    const symbol = 'BTP/USDT';
    const type = 'limit';
    const side = 'buy';
    const amount = 20.5;
    const price = 0.000939;
    const params = {dappId:'Sagittarius'};
   ;(async () => {
       const res = await exchange.createOrder (symbol, type, side, amount, price, params)
   }) ()
    
```

### Params

Parameter |Data Type	| Required |Default Value| Description|Value Range
--------- | ------- | -----------| ------- | -----------| -----------
symbol |string| true |NA|symbol name|'BTC/USDT','ETH/USDT'...
type |string| true |NA|order type|'limit','market'
side |string| true |NA|order side|'sell','buy'
amount |double| true |NA|order amount|
price |double| true |NA|order price|
params |object| false |NA||

* params
 
 Parameter | Type |Description
 --------- | ------- | -----------
  dappId| string |fee reward user id

> Response:

```json

```

### Response Content

Parameter | Type |Description
--------- | ------- | -----------
info | object |
id | string | orderid 

* info
 
 Parameter | Type |Description
 --------- | ------- | -----------
  code| int |response code,0 is succeed, others are failed
                           






## Order Cancel


## Transfer


 
 
