# Oracle Price Feeder

As a validator in the active set, you will be required to use the Oracle Price Feeder to submit prices.

## Installation

```bash
git clone git@github.com:Team-Kujira/oracle-price-feeder.git
cd oracle-price-feeder
make install
```

## Configuration

### Price Feeds

Start by copying the default configuration file. This will add price feeds for `ATOM` (the first exchange rate supported by the price-feeder).

This config also contains default values for `gas_price` and `gas_adjustment`

```
cp config.example.toml config.toml
```

### Currency Pairs

```
[[currency_pairs]]
base = "ATOM"
providers = [
  "binance",
  "kraken",
  "coinbase",
]
quote = "USD"
```

**NOTE:** It is important that currency pairs in this config exactly match those in the currently configured whitelist for the chain:

* Testnet: [harpoon-4](https://lcd.harpoon.kujira.setten.io/oracle/params)
* Mainnet: [kaiyo-1](https://lcd.kaiyo.kujira.setten.io/oracle/params)

You can also query the oracle params using `kujirad`

```
kujirad query oracle params
```

### Provider Endpoints

It is possible to overwrite default provider endpoints (e.g. to point to an alternate mirror) by specifying them in `[[provider_endpoints]]`.

#### Example for Binance.US

```
[[provider_endpoints]]
name = "binance"
rest = "https://api.binance.us"
websocket = "stream.binance.us:9443"
```

### Addresses & Voting Delegate

The price-feeder submits transactions on behalf of your validator that contain prices of specified denoms. The feeder account will need enough funding to pay for gas for these automatic vote transactions perpetually. Due to how this is performed by price-feeder, it's highly recommended to use a delegate feeder account rather than the validator account as the feeder wallet key is potentially more exposed.

```
[account]
address = "kujira...." # feeder wallet address
chain_id = "<harpoon-4/kaiyo-1>"
validator = "kujiravaloper...." # validator address
prefix = "kujira"
```

Ensure the `validator` address is set to [your validator address.](https://github.com/Team-Kujira/oracle-price-feeder/blob/master/config.example.toml#L52)

Ensure that `address` is set to the address of [your feeder wallet](https://github.com/Team-Kujira/oracle-price-feeder/blob/master/config.example.toml#L50). By default this is the same as the `kujira` address for your validator key, however it's likely that you'll want to set a delegate feeder account to your validator so that you can run price-feeder on a separate user account or separate server, with different keys.

To set a delegate:

```
kujirad tx oracle set-feeder kujira1243.....
```

### Keyring Backend

Depending on your infrastructure you may have a different preference for your keyring backend. If you are running price-feeder on a separate account or separate server, you can experiment with different keyring backends without any risk to your running validator - however, you risk corrupting your validator keys if you are not using a separate account or server for price-feeder (again, this configuration is not recommended)

[https://github.com/Team-Kujira/oracle-price-feeder/blob/master/config.example.toml#L55-L57](https://github.com/Team-Kujira/oracle-price-feeder/blob/master/config.example.toml#L55-L57)

#### OS

```toml
[keyring]
backend = "os"
# dir is ignored for os
dir = "/home/kuji/.kujira"
```

#### FILE

**Create a file keyring**

```bash
kujirad keys add oracle
mkdir ~/.kujira/keyring-file
mv ~/.kujira/*.address ~/.kujira/*.info ~/.kujira/keyring-file
```

**Set the password variable**

```bash
export PRICE_FEEDER_PASS=<keyring_password>
```

**Update config.toml**

```toml
[keyring]
backend = "file"
dir = "/home/kuji/.kujira"
```

#### PASS

You may need to install `pass` first:

[https://www.passwordstore.org](https://www.passwordstore.org)

And then set your passphrase to env

```
export PRICE_FEEDER_PASS=...  
```

```toml
[keyring]
backend = "pass"
# dir is ignored for pass
dir = "/home/kuji/.kujira"
```

### RPC Endpoints

If price-feeder is running on the same server as your node and your node is using default ports, the default RPC configuration should work.

If you are running a different node configuration, you may need to edit these RPC settings to match your infrastructure.

```
[rpc]
grpc_endpoint = "localhost:9090"
rpc_timeout = "100ms"
tmrpc_endpoint = "http://localhost:26657"
```

### Telemtry & Prometheus

Telemetry is provided by the [Cosmos SDK Telemetry module](https://github.com/cosmos/cosmos-sdk/blob/main/docs/core/telemetry.md). To query metrics from a running price-feeder, pipe the output into jq

`curl "http://localhost:7171/api/v1/metrics" | jq`

To publish price-feeder metrics in prometheus format, the config.toml must include the `prometheus_retention` flag

Example Telemetry configuration block with Prometheus format enabled:

```
[telemetry]
enable_hostname = true
enable_hostname_label = true
enable_service_label = true
enabled = true
global_labels = [["chain-id", "harpoon-4"]]
service_name = "price-feeder"
type = "prometheus"
prometheus_retention = 120
```

Example scrape\_config in Prometheus:

```
scrape_configs:
  - job_name: price-feeder
    metrics_path: '/api/v1/metrics'
    params:
      format: ['prometheus']
    static_configs:
      - targets:
          - <price-feeder-IP-addr>:7171
        labels: {}
```

## Running

Finally, start your price feeder

```
price-feeder config.toml
```

If everything is set up correctly, the process will start to collect prices, and shortly after will begin submitting votes:

```
12:25PM INF skipping until next voting period current_vote_period=6403 module=oracle previous_vote_period=6403 vote_period=14
12:25PM INF broadcasting vote exchange_rates=11.517155694978280323ATOM,1.000110504829617895USDT feeder=kujira... module=oracle validator=kujiravaloper...
121ukuji
12:25PM INF successfully broadcasted tx module=oracle_client tx_code=0 tx_hash=31C6C40EA72850CE650A0D6B776533D2A631C1E2763F30BB13F7576E047D3F5F tx_height=0
12:25PM INF broadcasting pre-vote feeder=kujira... hash=63b56da8141d7cd357de9a32f46bdef9220436cd module=oracle validator=kujiravaloper...
98ukuji
12:25PM INF successfully broadcasted tx module=oracle_client tx_code=0 tx_hash=067C973A32AD172F10F7BDFC85CD7407B11E65C77B6E2E1AE2488B1F6B94BC9B tx_height=0
12:25PM INF skipping until next voting period current_vote_period=6404 module=oracle previous_vote_period=6404 vote_period=14
```

You will likely also want to set up this price feeder as a system service. This will be the same process as [setting up the chain core](./#register-the-node-as-a-service).

Example systemd service using `file` keyring backend

```
[Unit]
Description=Price Feeder
After=network-online.target

[Service]
User=MYUSER
ExecStart=/home/MYUSER/go/bin/price-feeder /home/MYUSER/oracle-price-feeder/config.toml --log-level=debug
WorkingDirectory=/home/MYUSER/.kujira/keyring-file
Restart=always
StartLimitInterval=0
RestartSec=3

[Install]
WantedBy=multi-user.target

[Service]
LimitNOFILE=65535
Environment="PRICE_FEEDER_PASS=MYPASSWORD"
```
