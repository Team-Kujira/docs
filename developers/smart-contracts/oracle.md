# Price Oracle

Every 30 seconds, all 75 validators in the Kujira active set are required to post a transaction containing the current price for a range of assets, aggregated from a number of sources. This creates an on-chain source of truth which can be queried from a UI front-end, the CLI and also in smart contracts.

### REST

You can fetch all exchange rates here: [https://lcd.kaiyo.kujira.setten.io/oracle/denoms/exchange\_rates](https://lcd.kaiyo.kujira.setten.io/oracle/denoms/exchange\_rates)

Or just a specific one at eg [https://lcd.kaiyo.kujira.setten.io/oracle/denoms/ATOM/exchange\_rate](https://lcd.kaiyo.kujira.setten.io/oracle/denoms/ATOM/exchange\_rate)

### CLI

```
kujirad query oracle exchange-rates
```

### CosmWASM

The kujira-rs package provides queryable bindings to fetch current exchange rates inside your smart contracts:

{% embed url="https://docs.rs/kujira/0.7.5/kujira/msg/enum.KujiraMsg.html" %}

```rust
use kujira::querier::KujiraQuerier;
use kujira::query::KujiraQuery;

pub fn query(deps: Deps<KujiraQuery>, env: Env, msg: QueryMsg) -> StdResult<Binary> {
    let q = KujiraQuerier::new(&deps.querier);
    let res = q.query_exchange_rate("ATOM".to_string())?;
    let price = res;
    Ok(to_binary(&price))
}
```

Note that the type signature for a `query` interface that uses this must be&#x20;

```rust
```
