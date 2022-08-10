# Oracle Price Feeder

As a validator in the active set, you will be required to use the Oracle Price Feeder to submit prices.&#x20;

## Installation



```bash
# If you have core cloned in this directory already, you can skip this step
# Alternatively, once you have cloned oracle-price-feeder, you can change the `replace`
# directive here https://github.com/Team-Kujira/oracle-price-feeder/blob/master/go.mod#L5
git clone git@github.com:Team-Kujira/core.git


git clone git@github.com:Team-Kujira/oracle-price-feeder.git
cd oracle-price-feeder
make install
```

## Configuration

### Price Feeds

Start by copying the default configuration file. This will add price feeds for `ATOM`, `USDT` and `USDC`

This config also contains default values for `gas_price` and `gas_adjustment`

```
cp config.example.toml config.toml
```

You should query the oracle params and check that you have all the requisite denoms configured for the vote.&#x20;

```
kujirad query oracle params
```

### Addresses & Voting Delegate

Ensure the `validator` address is set correctly to your validator: [https://github.com/Team-Kujira/oracle-price-feeder/blob/master/config.example.toml#L52](https://github.com/Team-Kujira/oracle-price-feeder/blob/master/config.example.toml#L52)

Ensure that `address` is set to the correct voter. By default this is the same as the `kujira` address for your validator key, however it's likely that you'll want to set a delegate so that you can run this process on a separate server, with different keys [https://github.com/Team-Kujira/oracle-price-feeder/blob/master/config.example.toml#L50](https://github.com/Team-Kujira/oracle-price-feeder/blob/master/config.example.toml#L50)

To set a delegate:

```
kujirad tx oracle set-feeder kujira1243.....
```

### Keyring Backend

Depending on your infrastructure you may have a different preference for your keyring backend.&#x20;

[https://github.com/Team-Kujira/oracle-price-feeder/blob/master/config.example.toml#L55-L57](https://github.com/Team-Kujira/oracle-price-feeder/blob/master/config.example.toml#L55-L57)

#### OS

```toml
[keyring]
backend = "os"
# dir is ignored for os
dir = ""
```

#### FILE
##### Create a file keyring
```bash
kujirad keys add oracle
mkdir ~/.kujira/keyring-file
mv ~/.kujira/*.address ~/.kujira/*.info ~/.kujira/keyring-file
```
##### Set the password variable
```bash
export PRICE_FEEDER_PASS=<keyring_password>
```

##### Update config.toml
```toml
[keyring]
backend = "file"
dir = "/home/kuji/.kujira"
```

#### PASS

You may need to install `pass` first:&#x20;

[https://www.passwordstore.org](https://www.passwordstore.org)

And then set your passphrase to env&#x20;

```
export PRICE_FEEDER_PASS=...  
```

```toml
[keyring]
backend = "pass"
# dir is ignored for pass
dir = ""
```

## Running

Finally, start your price feeder

```
price-feeder config.toml
```

If everything is set up correctly, the process will start to collect prices, and shortly after will begin submitting votes:&#x20;

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



You will likely also want to set up this price feeder as a system service. This will be the same process as [setting up the chain core](./#register-the-node-as-a-service).&#x20;
