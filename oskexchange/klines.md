# Retrieving crypto trend lines from binance

Binance api

```
https://api.binance.com/
```

Binance api documentation

```
https://developers.binance.com/docs/binance-spot-api-docs/rest-api/market-data-endpoints
```

### step 1

Make a request to get coins

```
https://api.oskexchange.com/coin/list/

```

**Example response:**

```json
{
  "status": "success",
  "entity": [
    {
      "id": 1,
      "coin": "btc",
      "is_disabled": false,
      "image": null,
      "price_key": "BTC",
      "name": "Bitcoin",
      "binance_symbol": "BTCNGN",
      "price": {
        "change": 0.4171188210273743,
        "price_ngn": 146374914,
        "price_usd": 94346
      }
    },
    {
      "id": 2,
      "coin": "eth",
      "is_disabled": false,
      "image": null,
      "price_key": "ETH",
      "name": "Ethereum",
      "binance_symbol": "ETHNGN",
      "price": {
        "change": -0.6020134650302895,
        "price_ngn": 5035023,
        "price_usd": 3245.32
      }
    },
    {
      "id": 3,
      "coin": "trx",
      "is_disabled": false,
      "image": null,
      "price_key": "TRX",
      "name": "Tron",
      "binance_symbol": "TRXNGN",
      "price": {
        "change": 0.8146355984084697,
        "price_ngn": 376.96,
        "price_usd": 0.24297
      }
    },
    {
      "id": 4,
      "coin": "usdt",
      "is_disabled": false,
      "image": null,
      "price_key": "USDT",
      "name": "Tether",
      "binance_symbol": "USDNGN",
      "price": {
        "change": -0.0147446377270055,
        "price_ngn": 1550.69,
        "price_usd": 0.999701
      }
    },
    {
      "id": 5,
      "coin": "bnb",
      "is_disabled": false,
      "image": null,
      "price_key": "BNB",
      "name": "Binance",
      "binance_symbol": "BNBNGN",
      "price": {
        "change": 0.582562111403752,
        "price_ngn": 1077309,
        "price_usd": 694.38
      }
    },
    {
      "id": 6,
      "coin": "sol",
      "is_disabled": false,
      "image": null,
      "price_key": "SOL",
      "name": "Solana",
      "binance_symbol": "SOLNGN",
      "price": {
        "change": -1.7462512822361647,
        "price_ngn": 289431,
        "price_usd": 186.55
      }
    }
  ],
  "message": "Coins fetched successfully",
  "success": true
}
```

Take note of the `binance_symbol` field, this will be used to talk to binance

### step 2

Make a request to binance api

```
https://api.binance.com/api/v3/klines?symbol=ETHNGN&interval=1d&limit=40
```

**symbol**: refers to the trading pair on the Binance platform. In the url above, `ETHNGN` represents the market pair for Ethereum (ETH) against Nigerian Naira (NGN).

**interval**: Interval specifies the time frame for each candlestick or kline in the data, In this case, `1d` means each candlestick represents one day's worth of trading data

**lmit**: specifies the maximum number of candlestick (kline) data points to be returned by the API.

**Example response:**

```json
[
    [
        1609459200000,
        "346700.00000000",
        "352629.00000000",
        "337468.00000000",
        "344524.00000000",
        "474.92591000",
        1609545599999,
        "164304807.73522000",
        2812,
        "225.65423000",
        "78232298.77147000",
        "0"
    ],
    [
        1609545600000,
        "342777.00000000",
        "372000.00000000",
        "339600.00000000",
        "363492.00000000",
        "1075.74344000",
        1609631999999,
        "385899783.79637000",
        5309,
        "606.12963000",
        "217654773.70847000",
        "0"
    ],
    ...
]
```

The response is an array of arrays, where each inner array represents candlestick (kline) data for a specific time period (e.g., one day in this case).
Each item in the array represent different fields as regarding the market data for that interval

our interest is in `array[0]` and `array[3]`

**array[0]**:
This is the Start time of the candlestick in milliseconds since Unix epoch

**array[3]**:
The lowest price traded during this interval 

So if you request the data with an interval of 1d (one day) and the response shows a lowest price of 300000, you can conclude that the lowest price of ETH during that specific day was 300000 NGN.


## Generic code suggestion for getting the trend line

The aim is to get a list containing coins and their corresponding thread lines

```
1. Make request to coin list and store response in variable `result`

result = request to `https://api.oskexchange.com/coin/list/`

trend_lines = []
for i in result
    binance response = request to `api/v3/klines?symbol=[result.binance_symbol]&interval=1d&limit=40`

    coin_trend_values = []
    for j in binance_response
        interval_data = {
            "timestamp": j[0],
            "highest_price": j[3]
        }
        coin_trend_values.add(interval_data)

    coin_trend = {
        "coin": [result.coin],
        "spark_line": coin_trend_values
    }

    trend_lines.add(coin_trend)
```

