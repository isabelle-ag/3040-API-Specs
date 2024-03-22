<h1 style="text-align:left; font-size: 50px;"><strong>3040Crypto Wallet Management API</strong></h1>

# Description
---

The 3040Crypto wallet Management API is an accessible API, designed to be used by anyone who has a wallet with 3040Crypto or who has an interest in the transactions that run through it. The two main features are wallet breakdown, which displays the amount and value of the coins a user holds, and transaction history, which will either display the transaction log for one user or for the userbase of 3040Crypto as a whole.

# Endpoints
---
### Wallet Details

`/wallet-details/<wallet_id>[?fiat=<currency_code>&crypto=<crypto_symbol>]`

`GET` Provides a list of cryptocurrencies held in the specified wallet alongside the wallet's total value in a given fiat currency. If the `fiat` parameter is omitted, it defaults to the user's fiat currency. Optionally, you can refine the response by filtering it with the `crypto` query string parameter.

`PUT` Updates the users default fiat currency.

**Query String Parameters**

`fiat` 
> Accepts values like CAD, USD, AUD, etc.
> Default: CAD.

`crypto` 
> Accepts values like BTC, ETH, DOGE, etc.

### Transaction History

`/transaction-history/<wallet_id>[?date_range=<yyyy-mm-dd,yyyy-mm-dd>]`

`GET` Given a wallet ID, returns recent transactions in reverse chronological order. Optionally, use the `date_range` query string parameter to filter the results by specifying a date range; it will return all transactions of that wallet within the specified date range, including the first and last date.

**Query String Parameters**

`date_range`
> Accepts date range in the format YYYY-MM-DD,YYYY-MM-DD.
> The order doesn't matter.

### Global Transactions

`/global-transactions[?date=<YYYY-MM-DD>&crypto=<crypto_symbol>]`

`GET` Return all cryptocurrency transactions that have occurred on a given day. Optionally, use the query string parameters `date` and `crypto` to filter the results. If no `date` parameter is provided, the default is the current date.

**Query String Parameters**

`date`
> Accepts date in the format YYYY-MM-DD.
> Default: today.

`crypto` 
> Accepts values like BTC, ETH, DOGE, etc.

# Resources
---

### Wallet

```json
{
  "wallet_id": integer, // User's wallet ID
  "cryptocurrencies": [
    {
      "symbol": string, // Cryptocurrency symbol
      "amount": float, // Amount of this cryptocurrency owned by this wallet
      "fiat_currency": string, // Symbol of fiat currency
      "value": float // Total value of this cryptocurrency in the specified fiat currency
    }
  ]
}

```

### Global Transactions

```json
{
  "transactions": [
    {
      "transaction_id": string, // Unique identifier for the transaction
      "timestamp": string, // Timestamp of the transaction in ISO 8601 format
      "amount": float, // Amount of cryptocurrency involved in the transaction
      "currency": string, // Cryptocurrency symbol
      "type": string, // Type of transaction (deposit, withdrawal)
      "status": string // Status of the transaction (completed, pending)
    }
  ]
}

```

# Sample Request & Response
---

Request for the [transaction history](#transaction-history) given the wallet ID and a date range.

```javascript
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


