### Extended API Documentation for All Routes
#### Base URL
The base URL for this API is `https://django-9app-production.up.railway.app/wallet`.

- **Supported Currencies**: `btc`, `eth`, `sol`, `trx`, `usdt`

#### 1. **Get Wallet Address**
- **Endpoint**: `/wallet-address/`
- **Method**: GET
- **Authorization**: Bearer Token
- **Description**: Retrieves the wallet addresses for the authenticated user.
- **Success Response**:
  - **Code**: 200 OK
  - **Content**:
    ```json
    {
      "status": "success",
      "entity": {
        "bitcoin_address": "1BoatSLRHtKNngkdXEeobR76b53LETtpyT",
        "etherum_address": "0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe",
        "solana_address": "Sol123Address",
        "tron_address": "Tron123Address",
        "usdt_address": "USDt123Address"
      },
      "message": "Wallet addresses retrieved successfully",
      "success": true
    }
    ```

#### 2. **Get Wallet Balance**
- **Endpoint**: `/wallet-balance/`
- **Method**: GET
- **Authorization**: Bearer Token
- **Description**: Fetches the balance for all cryptocurrencies in the user's wallet.
- **Success Response**:
  - **Code**: 200 OK
  - **Content**:
    ```json
    {
      "status": "success",
      "entity": {
        "btc_balance": "0.001",
        "eth_balance": "2.5",
        "sol_balance": "100.0",
        "trx_balance": "1500",
        "usdt_balance": "50"
      },
      "message": "Wallet balances retrieved successfully",
      "success": true
    }
    ```

#### 3. **Transfer Coin**
- **Endpoint**: `/transfer-coin/`
- **Method**: POST
- **Authorization**: Bearer Token
- **Description**: Transfers a specified amount of cryptocurrency to another wallet.
- **Request Body**:
  ```json
  {
    "amount": "0.002",
    "recipient": "1BoatSLRHtKNngkdXEeobR76b53LETtpyT",
    "currency": "btc"
  }
  ```
- **Success Response**:
  - **Code**: 200 OK
  - **Content**:
    ```json
    {
      "status": "success",
      "entity": {
        "transaction_id": "tx123456789",
        "status": "Success",
        "message": "Transaction successful"
      },
      "message": "Coin transferred successfully",
      "success": true
    }
    ```

#### 4. **Coin Swap**
- **Endpoint**: `/coin-swap/`
- **Method**: POST
- **Authorization**: Bearer Token
- **Description**: Swaps a specified amount of one cryptocurrency for another.
- **Request Body**:
  ```json
  {
    "amount": "0.5",
    "from_coin": "btc",
    "to_coin": "eth"
  }
  ```
- **Success Response**:
  - **Code**: 200 OK
- **Content**:
    ```json
    {
      "status": "success",
      "entity": {
        "track": "track123456789",
        "response_text": "Swap initiated successfully"
      },
      "message": "Coin swap initiated",
      "success": true
    }
    ```

#### 5. **Get Currency Price**
- **Endpoint**: `/currency-price/<str:currency>/`
- **Method**: GET
- **Authorization**: Bearer Token
- **Description**: Retrieves the latest price of a specified currency (USD or NGN).
- **URL Parameter**: `currency` (e.g., "usd" or "naira")
- **Success Response**:
  - **Code**: 200 OK
  - **Content**:
    ```json
    {
      "status": "success",
      "entity": [
        {
          "name": "Bitcoin",
          "symbol": "BTC",
          "price": "58000.00",
          "change": "200.00"
        },
        {
          "name": "Ethereum",
          "symbol": "ETH",
          "price": "1800.00",
          "change": "50.00"
        }
      ],
      "message": "Currency prices retrieved",
      "success": true
    }
    ```

#### 6. **Get Individual Currency Balance**
- **

Endpoint**: `/currency-balance/<str:currency>/`
- **Method**: GET
- **Authorization**: Bearer Token
- **Description**: Fetches the balance of a specified cryptocurrency for the authenticated user.
- **URL Parameter**: `currency` (e.g., "btc")
- **Success Response**:
  - **Code**: 200 OK
  - **Content**:
    ```json
    {
      "status": "success",
      "entity": {
        "currency": "BTC",
        "balance": "0.001"
      },
      "message": "Currency balance retrieved",
      "success": true
    }
    ```

#### 7. **Get USD Price**
- **Endpoint**: `/usd-price/`
- **Method**: GET
- **Authorization**: Bearer Token
- **Description**: Retrieves the latest price of all cryptocurrencies in USD.
- **Success Response**:
  - **Code**: 200 OK
  - **Content**:
    ```json
    {
      "status": "success",
      "entity": [
        {
          "name": "Bitcoin",
          "symbol": "BTC",
          "price": "58000.00",
          "change": "200.00"
        },
        {
          "name": "Ethereum",
          "symbol": "ETH",
          "price": "1800.00",
          "change": "50.00"
        }
      ],
      "message": "USD prices retrieved",
      "success": true
    }
    ```

#### 8. **Get Naira Price**
- **Endpoint**: `/naira-price/`
- **Method**: GET
- **Authorization**: Bearer Token
- **Description**: Retrieves the latest price of all cryptocurrencies in Nigerian Naira.
- **Success Response**:
  - **Code**: 200 OK
  - **Content**:
    ```json
    {
      "status": "success",
      "entity": [
        {
          "name": "Bitcoin",
          "symbol": "BTC",
          "price": "22,000,000.00",
          "change": "500,000.00"
        },
        {
          "name": "Ethereum",
          "symbol": "ETH",
          "price": "720,000.00",
          "change": "15,000.00"
        }
      ],
      "message": "Naira prices retrieved",
      "success": true
    }
    ```

#### 9. **USDT to NGN**
- **Endpoint**: `/usdt-to-ngn/`
- **Method**: POST
- **Authorization**: Bearer Token
- **Description**: Swaps USDT to Nigerian Naira based on current exchange rates.
- **Request Body**:
  ```json
  {
    "amount": "100.00"
  }
  ```
- **Success Response**:
  - **Code**: 200 OK
- **Content**:
    ```json
    {
      "status": "success",
      "entity": {
        "transaction_id": "tx789123456",
        "swapped_amount": "38,000,000.00",
        "status": "Success",
        "message": "Swap successful"
      },
      "message": "USDT to NGN swap executed",
      "success": true
    }
    ```

#### 10. **Get Exchange Estimate**
- **Endpoint**: `/exchange-estimate/`
- **Method**: POST
- **Authorization**: Bearer Token
- **Description**: Provides an estimate for a currency exchange, useful for showing users potential outcomes before they commit to a swap or transfer.
- **Request Body**:
  ```json
  {
    "from_currency": "btc",
    "to_currency": "eth",
    "amount": "0.1"
  }
  ```
- **Success Response**:
  - **Code**: 200 OK
- **Content**:
    ```json
    {
      "status": "success",
      "entity": {
        "estimated_amount": "3.5",
        "rate": "35",
        "status": "Success",
        "message": "Estimate provided"
      },
      "message": "Exchange estimate provided",
      "success": true
    }
    ```

#### 11. **Get Swap Status**
- **Endpoint**: `/swap-status/<str:transaction_id>/`
- **Method**: GET
- **Authorization**: Bearer Token
- **Description**: Provides status updates and tracking information for ongoing swaps.
- **URL Parameter**: `transaction_id` (e.g., "tx123456789")
- **Success Response**:
  - **Code**: 200 OK
- **Content**:
    ```json
    {
      "status": "success",
      "entity": {
        "transaction_id": "tx123456789",
        "status": "Completed",
        "message": "Swap completed successfully"
      },
      "message": "Swap status retrieved",
      "success": true
    }
    ```

#### 12. **Validate Currency**
- **Endpoint**: `/validate-currency/<str:currency>/`
- **Method**: GET
- **Authorization**: Bearer Token
- **Description**: Checks if the specified currency is supported by the system.
- **URL Parameter**: `currency` (e.g., "btc")
- **Success Response**:
  - **Code**: 200 OK
- **Content**:
    ```json
    {
      "status": "success",
      "entity": null,
      "message": "Currency is supported.",
      "success": true
    }
    ```
