# 3040-API-Specs

3040 Crypto
### Endpoints (Isabelle)
- transaction history/details
  - **Parameters:** Wallet ID, [date range]
- wallet details
    - cryptocurrency breakdown (0 parameters will give all cryptocurrencies)
    - **Parameters:** Wallet ID, [cryptocurrency], [real currency]
- crypto transactions (0 parameters = today or give date)
  - **Parameters:** [Date], [cryptocurrency]

### Resources (Anmol)

### Description (Zander)

### Sample Request & Sample Response (Seyi)
Here is a test run of a request for the transaction history given the wallet ID and a date range.

Request: GET /transaction-history?wallet_id=123456&date_range=2024-01-01,2024-03-20 HTTP/1.1
Host: api.3040crypto.com

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



[Note: This was collaboratively written]
