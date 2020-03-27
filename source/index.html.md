---
title: BitExchange API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://www.byte-trade.com'>Exchange</a>
  - <a href='https://explorer.byte-trade.com'>Explorer</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the ByteTrade API! You can use our API to access ByteTrade API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.


# APIs

## 交易品种信息

```shell
curl "https://api-v2.byte-trade.com/currencies"
```

> The above command returns JSON structured like this:



This endpoint retrieves a specific kitten.


### HTTP Request

`GET https://api-v2.bytetrade.com/currencies`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.


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

### 响应数据

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




## 交易市场信息

```shell
curl "https://api-v2.byte-trade.com/symbols"
```

> The above command returns JSON structured like this:



This endpoint retrieves a specific kitten.


### HTTP Request

`GET https://api-v2.bytetrade.com/symbols`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.


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

### 响应数据

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


