---
title: ClankApp API Documentation

toc_footers:
  - <a href='https://clankapp.com/api'>Get your free Api Key here</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the ClankApp API! You can use our API for free in order to get some infos about crypto whales accross 20+ blockchains.
Remember that this api are completly free to use so, in exchange, we demand a mention and a link to https://clankapp.com.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication && Rate Limits

## Api Key

In order to use our API's, you need an Api Key that you can request for free here: <a href="https://clankapp.com/api" target="_blank">ClankApp API</a>.

> Just use 'api_key' http get parameter to your http request.

```shell
https://api.clankapp.com/<ENDPOINT>?api_key=<YOURAPIKEY>
```


> Make sure to replace `<YOURAPIKEY>` with your API key.

## Rates limits

You are limited to **10 calls/minute**. Please don't abuse.

If you need more calls, contact us on twitter at [@ClankApp](https://twitter.com/ClankApp) or at hello@clankapp.com

# Blockchains

## Get All Blockchains

```shell
GET https://api.clankapp.com/v1/blockchain/list?api_key=<YOURAPIKEY>
```

> The above request returns JSON structured like this:

```json
{
    "btc": "bitcoin",
    "bch": "bitcoin-cash",
    "eth": "ethereum",
    "bsv": "bitcoin-sv",
    "ltc": "litecoin",
    ...
}
```

This endpoint show all blockchains available on ClankApp. Stay tuned, some new blockchains come sometimes :P

### HTTP Request

`GET https://api.clankapp.com/v1/blockchain/list?api_key=<YOURAPIKEY>`

# Transactions

## Get a specific transaction

```shell
GET https://api.clankapp.com/v2/tx/btc/ac6f1a0b388e2814f2e2036c7c81524cfae7e3432a8e503fe5d07ebb453ee310?api_key=<YOURAPIKEY>
```

> The above request returns JSON structured like this:

```json
{
    "tx": {
        "unique_machine_id": "NjYwNDc3NTk0MTgzMzUy",
        "blockchain": "bitcoin",
        "symbol": "btc",
        "transaction_type": "transfer",
        "hash": "ac6f1a0b388e2814f2e2036c7c81524cfae7e3432a8e503fe5d07ebb453ee310",
        "from_address": "Multiple Addresses",
        "to_address": "3JZq4atUahhuA9rLhXLMhhTo133J9rF97j",
        "timestamp": 1607422608,
        "amount": 19489.124,
        "amount_usd": 374138000,
        "from_owner": "multiple addresses",
        "to_owner": "bitfinex",
        "format_amount": "19,489.124",
        "format_amount_without_digit": "19,489",
        "format_amount_usd": "374,138,000",
        "date": "2020-12-08T10:16:48",
        "indexed_at": "2020-12-08T10:16:23",
    },
    "explorers": [
        {
            "name": "Blockchair",
            "description": "Blockchair is the most private search engine for Bitcoin, Ethereum, Ripple, Bitcoin Cash, Litecoin, Bitcoin SV, Stellar, Dash, Dogecoin and Groestlcoin.",
            "uri": "https://blockchair.com/bitcoin/transaction/ac6f1a0b388e2814f2e2036c7c81524cfae7e3432a8e503fe5d07ebb453ee310?from=clankapp.com",
            "id": "blockchair"
        },
        {
            "name": "BTC.com",
            "description": "A bitcoin explorer since 3 year ago.",
            "uri": "https://btc.com/ac6f1a0b388e2814f2e2036c7c81524cfae7e3432a8e503fe5d07ebb453ee310?from=clankapp.com",
            "id": "btc_com"
        },
        {
            "name": "Blockchain.com",
            "description": "The most popular and trusted block explorer and crypto transaction search engine.",
            "uri": "https://www.blockchain.com/btc/tx/ac6f1a0b388e2814f2e2036c7c81524cfae7e3432a8e503fe5d07ebb453ee310?from=clankapp.com",
            "id": "blockchain_com"
        }
    ],
    "outputs": null
}
```

This endpoint show datas of a specific transaction.

### HTTP Request

`GET https://api.clankapp.com/v2/tx/{symbol}/{hash}?api_key=<YOURAPIKEY>`

### URL Parameters

Parameter | Required | Description
--------- | ------- | -----------
symbol | true | The symbol of the asset, example: `btc`for bitcoin
hash | true | The transaction hash, example: `ac6f1a0b388e2814f2e2036c7c81524cfae7e3432a8e503fe5d07ebb453ee310`

<aside class="notice">
In addition, you can add the `?uuid=unique_machine_id` in order to limit the call to a single output only. Indeed, a transactions can have multiple outputs.
</aside>

### Result fields

Parameter | Nullable | Description
--------- | ----------- | -----------
tx | false | Object with all transaction data.
explorers | true | Array<Object> of others explorers who list this transaction.
outputs | true | Sometimes, a transaction can have multiple outputs.

## Transactions explorer / feed

```shell
GET https://api.clankapp.com/v2/explorer/tx?s_amount_usd=desc&size=5&%3E_date=2020-12-01T21:46:45&api_key=<YOURAPIKEY>
```

> The above request returns last 5 transactions with date greater than 2020-12-01T21:46:45 in a structured JSON.

```json
{
    "context": {
        "execution_time": 6,
        "total": 18347,
        "from": 0,
        "size": 5,
        "prev": null,
        "next": 5
    },
    "data": [
        {
            "unique_machine_id": "NjYwNDc3NTk0MTgzMzUy",
            "blockchain": "bitcoin",
            "symbol": "btc",
            "transaction_type": "transfer",
            "hash": "ac6f1a0b388e2814f2e2036c7c81524cfae7e3432a8e503fe5d07ebb453ee310",
            "from_address": "Multiple Addresses",
            "to_address": "3JZq4atUahhuA9rLhXLMhhTo133J9rF97j",
            "timestamp": 1607422608,
            "amount": 19489.124,
            "amount_usd": 374138000,
            "from_owner": "multiple addresses",
            "to_owner": "bitfinex",
            "format_amount": "19,489.124",
            "format_amount_without_digit": "19,489",
            "format_amount_usd": "374,138,000",
            "date": "2020-12-08T10:16:48",
            "indexed_at": "2020-12-08T10:16:23",
            "_score": null
        },
        ...
    ]
}
```

The main endpoint of our API, the explorer / feed call.

With this endpoint, you can browse across all of our database with lot of fitlers.

### HTTP Request

`GET https://api.clankapp.com/v2/explorer/tx?api_key=<YOURAPIKEY>`

### GET Parameters

Parameter | Prefix | Type | Description
--------- | ----------- | ----------- | -----------
s_**field** | s_ | Sort | Sort the result with `asc`or `desc` value.
[> or <]_**field** | [> or <]_ |Greater or smaller operator | Work only for `date`, `amount`, `amount_usd`.
t_**field** | t_ | Exact term match | Used for strict filter like exact match on string fields.
m_**field** | m_ | Term match | Used for match filtering on string fields.

<aside class="notice">
Remplace **field** by a transaction field, example `hash`.
</aside>

### Feed examples endpoint

- Get last 5 crypto whales for bitcoin:

`GET https://api.clankapp.com/v2/explorer/tx?s_date=desc&t_blockchain=bitcoin&size=5&api_token=9f72e2bd5cad61ee88566038739b98bc&api_key=<YOURAPIKEY>`

- Get last 10 biggest transaction send by bittrex:

`GET https://api.clankapp.com/v2/explorer/tx?t_blockchain=ethereum&>_amount_usd=1000000&t_from_owner=bittrex&s_date=desc&size=10&api_key=<YOURAPIKEY`
