---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the ByteTrade API! You can use our API to access ByteTrade API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```


> Make sure to replace `meowmeowmeow` with your API key.

ByteTrade uses API keys to allow access to the API. You can register a new ByteTrade API key at our [developer portal](http://example.com/developers).

ByteTrade expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

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




## Delete a Specific Kitten

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```


> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

