# 3040-API-Specs

### Description
This API is designed for developers who want to integrate programmatic access to 3040Crypto wallet functionalities. By using this API, developers can retrieve wallet details, transaction history, and global cryptocurrency transactions.

The 3040Crypto Wallet-Management API allows users and applications to programmatically interact with their 3040Crypto wallet data such as a wallet's total value in a given fiat currency, personal transcation history, and global transaction history.

### Endpoints

#### Wallet Details

`/wallet-details/<wallet_id>`

Provide a list of cryptocurrencies held in the specified wallet. Optionally, you can filter the response by cryptocurrency by including the `crypto` query parameter. If the `fiat` parameter is used, the response will include the wallets current value in the given currency.

**Query Parameters**

`crypto` 
> BTC, ETH, DOGE, etc

`fiat` 
> CAD, USD, AUD, etc

#### Transaction History

`/transaction-history/<wallet_id>`

Given a wallet ID, return recent transactions in reverse chronological order. Optionally, the `date_range` query parameter will return all of that wallets transactions in the date range, including the first and last date.

**Query Parameters**

`date_range`
> YYYY-MM-DD,YYYY-MM-DD

### Global Transactions

`/global-transactions`

Return all cryptocurrency transactions that have happened today. Optionally, the query parameters `date`, `date_range`, and `crypto` can be used to filter the results.

`date`
> YYYY-MM-DD

`date_range`
> YYYY-MM-DD,YYYY-MM-DD

`crypto` 
> BTC, ETH, DOGE, etc

### Resources (Anmol)

### Description (Zander)

### Sample Request & Sample Response (Seyi)
Here is a test run of a request for the transaction history given the wallet ID and a date range.

Request: GET /transaction-history/123456?date_range=2024-01-01,2024-03-20 HTTP/1.1
Host: api.3040crypto.com

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


