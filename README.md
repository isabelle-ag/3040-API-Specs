# 3040Crypto Wallet Management API

## Description (Zander)


## Endpoints

### Wallet Details

`/wallet-details/<wallet_id>[?crypto=<crypto_symbol>&fiat=<currency_code>]`

Provides a list of cryptocurrencies held in the specified wallet and the wallet's total value in a given fiat currency. Optionally, you can filter the response by cryptocurrency by including the `crypto` query parameter. If the `fiat` parameter is not specified, the default fiat currency is CAD. 

**Query Parameters**

`crypto` 
> Accepts values like BTC, ETH, DOGE, etc.

`fiat` 
> Accepts values like CAD, USD, AUD, etc.
> Default: CAD.

### Transaction History

`/transaction-history/<wallet_id>[?date_range=<yyyy-mm-dd,yyyy-mm-dd>]`

Given a wallet ID, returns recent transactions in reverse chronological order. Optionally, use the `date_range` query parameter to filter the results by specifying a date range; it will return all transactions of that wallet within the specified date range, including the first and last date.

**Query Parameters**

`date_range`
> Accepts date range in the format YYYY-MM-DD,YYYY-MM-DD.
> The order doesn't matter.

### Global Transactions

`/global-transactions[?date=<YYYY-MM-DD>&crypto=<crypto_symbol>]`

Return all cryptocurrency transactions that have occurred on a given day. Optionally, use the query parameters `date` and `crypto` to filter the results. If no `date` parameter is provided, the default is the current date.

**Query Parameters**

`date`
> Accepts date in the format YYYY-MM-DD.
> Default: today.

`crypto` 
> Accepts values like BTC, ETH, DOGE, etc.

## Resources

##### Wallet Object

```json
{
  "wallet_id": "123456",
  "cryptocurrencies": [
    {
      "symbol": "BTC",
      "amount": 1.5,
      "value": 75000.00,
      "fiat_currency": "CAD"
    },
    {
      "symbol": "ETH",
      "amount": 20.0,
      "value": 35000.00,
      "fiat_currency": "CAD"
    },
    {
      "symbol": "DOGE",
      "amount": 50000.0,
      "value": 15000.00,
      "fiat_currency": "CAD"
    }
  ],
  "total_value": 125000.00,
  "total_value_fiat_currency": "CAD"
}
```

##### Global Transaction

```json
{
  "transactions": [
    {
      "transaction_id": "txn_123",
      "timestamp": "2024-03-18T08:32:15Z",
      "amount": 0.5,
      "currency": "BTC",
      "type": "deposit",
      "status": "completed"
    },
    {
      "transaction_id": "txn_124",
      "timestamp": "2024-03-17T14:20:00Z",
      "amount": 25.0,
      "currency": "ETH",
      "type": "withdrawal",
      "status": "completed"
    }
  ]
}

```

## Sample Request & Response

Request for the [transaction history](#transaction-history) given the wallet ID and a date range.

```html
Request: GET /transaction-history/123456?date_range=2024-01-01,2024-03-20 HTTP/1.1
Host: api.3040crypto.com
```

```json
Response.json: {
  "transactions": [
    {
      "transaction_id": "txn_123",
      "timestamp": "2024-03-18T08:32:15Z",
      "amount": 0.5,
      "currency": "BTC",
      "type": "deposit",
      "status": "completed"
    },
    {
      "transaction_id": "txn_124",
      "timestamp": "2024-03-17T14:20:00Z",
      "amount": 25.0,
      "currency": "ETH",
      "type": "withdrawal",
      "status": "completed"
    }
  ]
}
```


