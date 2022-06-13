# KUJI testnet

This guide assumes you're running on Ubuntu 22.04 LTS - the commands will probably work just fine on 20.04 LTS or Debian.

## Basic machine setup

1. SSH into your node
2. Update your machine (Answer yes / ok to the prompts)
```
sudo apt update && sudo apt dist-upgrade -y
```
1. Install required tools
```
sudo apt install build-essential git unzip curl wget
```

### Install Golang

1. Download `go` 1.18.x
```
wget https://go.dev/dl/go1.18.2.linux-amd64.tar.gz
```
2. Extract the runtime
```
sudo tar -C /usr/local -xzf go1.18.2.linux-amd64.tar.gz
```

## Prepare testnet environment

1. Create the `kuji` user and switch to it
```
sudo useradd -m kuji
sudo su -s /bin/bash -l kuji
```
2. Add go to your path (add these lines to `~/.profile` or `~/.bashrc`)
```
export PATH=$PATH:/usr/local/go/bin
export PATH=$PATH:$(go env GOPATH)/bin
```
3. Run `source ~/.profile` and/or `source ~/.bashrc`

## Now we build!

1. Download the project code and checkout to testnet branch
```bash
git clone https://github.com/Team-Kujira/core $HOME/kujira-core
cd $HOME/kujira-core
git checkout v0.4.0
```
2. Build and install `kujirad` (using the `kuji` user created above)
```
make install
```
3. Verify your binary is working
```
kujirad version
```

## Running the node

If the build succeed you should now have the `kujirad` cli in your path (of the `kuji` user).

Try invoking with `kujirad` and you should see output like

```
Stargate CosmosHub App

Usage:
  kujirad [command]

Available Commands:
  add-genesis-account Add a genesis account to genesis.json
  collect-gentxs      Collect genesis txs and output a genesis.json file
  config              Create or query an application CLI configuration file
  debug               Tool for helping with debugging your application
  export              Export state to JSON
  gentx               Generate a genesis tx carrying a self delegation
  help                Help about any command
....
```

## Join the testnet

Now we can initialize the node and join the network.
1. Initialize node's configuration files
```
export CHAIN_ID=harpoon-4
export MONIKER_NAME="<moniker name>"
```
```
kujirad init "${MONIKER_NAME}" --chain-id ${CHAIN_ID}
```

Replace the `<moniker name>` with your desired validator name.

2. Fetch the genesis `genesis.json` file
```
wget https://raw.githubusercontent.com/Team-Kujira/networks/master/testnet/harpoon-4.json -O $HOME/.kujira/config/genesis.json
```
3. Download the `addrbook.json` file
```
wget https://raw.githubusercontent.com/Team-Kujira/networks/master/testnet/addrbook.json -O $HOME/.kujira/config/addrbook.json
```

Now start the node
```bash
$ kujirad start

kuji@fsn1-kuji-testnet-01:~$ kujirad start
12:22PM INF starting node with ABCI Tendermint in-process
12:22PM INF Starting multiAppConn service impl=multiAppConn module=proxy
12:22PM INF Starting localClient service connection=query impl=localClient module=abci-client
12:22PM INF Starting localClient service connection=snapshot impl=localClient module=abci-client
12:22PM INF Starting localClient service connection=mempool impl=localClient module=abci-client
12:22PM INF Starting localClient service connection=consensus impl=localClient module=abci-client
```

And then watch a whole bunch of log messages while your node is catching up. After making sure that it works, it's time to install it as a system level service so it always starts with the machine.

## Register the node as a service

Drop out of the `kuji` user if you're still in that terminal session. Write `exit` or type `ctrl+d` on your keyboard.

1. Create a service definition file in `/etc/systemd/system/kujirad.service`. Example file that fits with our `kuijrad` install and `kuji` runtime user

```
[Unit]
Description=Kujira Daemon
After=network.target

[Service]
Type=simple
User=kuji
ExecStart=/home/kuji/go/bin/kujirad start --log_level error 
Restart=on-abort
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target  
```

2. Reload your systemctl and enable the service:
```
sudo systemctl daemon-reload
sudo systemctl enable kujirad
```

3. And finally start the service:
```
sudo systemctl start kujirad
```

4. Check the status of the service:
```
systemctl status kujirad.service
```

It should return something like
```
● kujirad.service - Kujira Daemon
     Loaded: loaded (/etc/systemd/system/kujirad.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2022-05-24 12:34:26 UTC; 5s ago
   Main PID: 18490 (kujirad)
      Tasks: 11 (limit: 4541)
     Memory: 65.4M
        CPU: 4.430s
     CGroup: /system.slice/kujirad.service
             └─18490 /home/kuji/go/bin/kujirad start
...
```

5. Check `kujirad` service logs
```
journalctl -u kujirad -f -o cat
```
And the sync status (make sure `jq` is installed)
```
kujirad status 2>&1 | jq .SyncInfo
```

## Create the validator

Once your node has synced, it's time to create a validator.
It can be done on a seperate machine if preferred.

Create a key that will be the validators key.
```
kujirad keys add <wallet name>
```
Replace the `<wallet name>` with your desired validator wallet name.

Copy the seed phrase and put it somewhere safe.

You will need to make note of the address `kujira...` and use that in the faucet to get some coins.
You can check your balance via
```
kujirad query bank balances kujira....
```

The next part is associating your node with your account, creating the validator
```
export PUBKEY=$(kujirad tendermint show-validator)
export CHAIN_ID=harpoon-4
export MONIKER_NAME="<your moniker>"
```
```
kujirad tx staking create-validator
--moniker="${MONIKER_NAME}" \
--amount=1000000ukuji \
--gas-prices=1ukuji \
--pubkey=$PUBKEY \
--from=validator \
--yes \
--node=tcp://localhost:26657 \
--chain-id=${CHAIN_ID} \
--commission-max-change-rate=0.01 \
--commission-max-rate=0.20 \
--commission-rate=0.10 \
--min-self-delegation=1
```
Now your node should be present
```
kujirad query staking validator $(kujirad keys show $KUJIRA_WALLET_ADDRESS --bech val -a)
```
or JSON output
```
kujirad query staking validators --limit 1000000 -o json | jq '.validators[] | select(.description.moniker=="${MONIKER_NAME}")'
```
Please remember to also back up `$HOME/.kujira/config/priv_validator_key.json`.
If you lose this, you are toast.


## Tips
### Disk utilization
To help manage the disk size you can prune the blocks being kept. for this I use prime numbers pick your own in `app.toml`
```
pruning = "custom"

# These are applied if and only if the pruning strategy is custom.
pruning-keep-recent = "809"
pruning-keep-every = "0"
pruning-interval = "43"
```
You should also check what you are indexing
```
index-events = ["tx.hash", "tx.height"]
```
### Adding more peers
You should modify `/etc/security/limits.conf` and add
```
*                soft    nofile          65535
*                hard    nofile          65535
```
You can then modify the config.toml to increase connections. This may cost you more in ingress/egress charges.
```
max_open_connections = 1900
max_num_inbound_peers = 50
max_num_outbound_peers = 50
```
