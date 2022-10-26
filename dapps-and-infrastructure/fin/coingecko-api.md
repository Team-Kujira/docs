# 🔘 Coingecko API

This documents the REST endpoints to query live data from the FIN markets for our Coingecko integration.

### GET \`[https://api.kujira.app/api/coingecko/pairs](https://api.kujira.app/api/coingecko/pairs)\`

#### Query options

None

#### Sample Response

```json
{
  "pairs": [
    {
      "base": "KUJI",
      "pool_id": "kujira14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9sl4e867",
      "target": "axlUSDC",
      "ticker_id": "KUJI_axlUSDC"
    }
  ]
}
```

### GET \`[https://api.kujira.app/api/coingecko/orderbook](https://api.kujira.app/api/coingecko/orderbook)\`

#### Query Options

* \*`ticker_id` eg `ticker_id=KUJI_axlUSDC`
* `depth` eg `depth=200` - total number of prices retrieved (equal number either side of the spread)

#### Sample Reponse

```
{
  "tickers": [
    {
      "ask": "0.3950",
      "base_currency": "KUJI",
      "base_volume": "2091945.3229",
      "bid": "0.3900",
      "high": "1.4755",
      "last_price": "0.3900",
      "low": "0.2910",
      "pool_id": "kujira14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9sl4e867",
      "target_currency": "axlUSDC",
      "target_volume": "868587.7620",
      "ticker_id": "KUJI_axlUSDC"
    }
  ]
}
```

### GET \`[https://api.kujira.app/api/coingecko/tickers](https://api.kujira.app/api/coingecko/tickers)\`

#### Query Options&#x20;

None

#### Sample Response

```
{
  "tickers": [
    {
      "ask": "0.3950",
      "base_currency": "KUJI",
      "base_volume": "2091945.3229",
      "bid": "0.3900",
      "high": "1.4755",
      "last_price": "0.3900",
      "low": "0.2910",
      "pool_id": "kujira14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9sl4e867",
      "target_currency": "axlUSDC",
      "target_volume": "868587.7620",
      "ticker_id": "KUJI_axlUSDC"
    } 
  ]
}
```

