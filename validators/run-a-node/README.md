# 🐎 Run a Node

This guide assumes you're running on Ubuntu 22.04 LTS - the commands will probably work just fine on 20.04 LTS or Debian.&#x20;

## Basic machine setup

1. SSH into your node&#x20;
2. Update your machine (Answer yes / ok to the prompts)

```
sudo apt update && sudo apt dist-upgrade -y
```

1. Install required tools

```
sudo apt install build-essential git unzip curl wget
```

## Prepare environment

Create the `kuji` user and switch to it

```
sudo useradd -m kuji
sudo su -s /bin/bash -l kuji
```

### Install Golang

1. Download `go` 1.20.x

```
# remove old go version
sudo rm -rvf /usr/local/go/

# download recent go version
wget https://golang.org/dl/go1.20.8.linux-amd64.tar.gz

# install go
sudo tar -C /usr/local -xzf go1.20.8.linux-amd64.tar.gz

# remove unneeded installer
rm go1.20.8.linux-amd64.tar.gz

# source go
cat <<EOF >> ~/.profile
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
EOF
source ~/.profile
go version
```

## Now we build!

1. Download the project code and checkout to testnet branch

```bash
git clone https://github.com/Team-Kujira/core $HOME/kujira-core
cd $HOME/kujira-core
git checkout v0.9.1
```

1. Build and install `kujirad` (using the `kuji` user created above)

```
make install
```

1. Verify your binary is working

```
kujirad version
```

## Running the node

If the build succeeds, you should now have the `kujirad` cli in your path (of the `kuji` user).

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

## Join the network

Now we can initialize the node and join the network.

1. Initialize node's configuration files

```shell
export CHAIN_ID=kaiyo-1 # mainnet
export CHAIN_ID=harpoon-4 # testnet
export MONIKER_NAME="<moniker name>"
```

```
kujirad init "${MONIKER_NAME}" --chain-id ${CHAIN_ID}
```

Replace the `<moniker name>` with your desired validator name.

1. Fetch the genesis `genesis.json` file

```
wget https://raw.githubusercontent.com/Team-Kujira/networks/master/testnet/harpoon-4.json -O $HOME/.kujira/config/genesis.json
```

1. Download the `addrbook.json` file

```
wget https://raw.githubusercontent.com/Team-Kujira/networks/master/testnet/addrbook.json -O $HOME/.kujira/config/addrbook.json
```

Fix your gas fee settings in `$HOME/.kujira/config/app.toml`

```bash
sed -i "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.00119ukuji,0.00150factory\/kujira1qk00h5atutpsv900x202pxx42npjr9thg58dnqpa72f2p7m2luase444a7\/uusk,0.00150ibc\/295548A78785A1007F232DE286149A6FF512F180AF5657780FC89C009E2C348F,0.000125ibc\/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2,0.00126ibc\/47BD209179859CDE4A2806763D7189B6E6FE13A17880FE2B42DE1E6C1E329E23,0.00652ibc\/3607EB5B5E64DD1C0E12E07F077FF470D5BC4706AFCBC98FE1BA960E5AE4CE07,617283951ibc\/F3AA7EF362EC5E791FE78A0F4CCC69FEE1F9A7485EB1A8CAB3F6601C00522F10,0.000288ibc\/EFF323CC632EC4F747C61BCE238A758EFDB7699C3226565F7C20DA06509D59A5,0.000125ibc\/DA59C009A0B3B95E0549E6BF7B075C8239285989FF457A8EDDBB56F10B2A6986,0.00137ibc\/A358D7F19237777AF6D8AD0E0F53268F8B18AE8A53ED318095C14D6D7F3B2DB5,0.0488ibc\/4F393C3FCA4190C0A6756CE7F6D897D5D1BE57D6CCB80D0BC87393566A7B6602,78492936ibc\/004EBF085BBED1029326D56BE8A2E67C08CECE670A94AC1947DF413EF5130EB2,964351ibc\/1B38805B1C75352B28169284F96DF56BDEBD9E8FAC005BDCC8CF0378C82AA8E7\"/;" $HOME/.kujira/config/app.toml
```

Where these individual prices are as follows:

```
0.00119ukuji
0.00150factory/kujira1qk00h5atutpsv900x202pxx42npjr9thg58dnqpa72f2p7m2luase444a7/uusk
0.00150ibc/295548A78785A1007F232DE286149A6FF512F180AF5657780FC89C009E2C348F
0.000125ibc/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2
0.00126ibc/47BD209179859CDE4A2806763D7189B6E6FE13A17880FE2B42DE1E6C1E329E23
0.00652ibc/3607EB5B5E64DD1C0E12E07F077FF470D5BC4706AFCBC98FE1BA960E5AE4CE07
617283951ibc/F3AA7EF362EC5E791FE78A0F4CCC69FEE1F9A7485EB1A8CAB3F6601C00522F10
0.000288ibc/EFF323CC632EC4F747C61BCE238A758EFDB7699C3226565F7C20DA06509D59A5
0.000125ibc/DA59C009A0B3B95E0549E6BF7B075C8239285989FF457A8EDDBB56F10B2A6986
0.00137ibc/A358D7F19237777AF6D8AD0E0F53268F8B18AE8A53ED318095C14D6D7F3B2DB5
0.0488ibc/4F393C3FCA4190C0A6756CE7F6D897D5D1BE57D6CCB80D0BC87393566A7B6602
78492936ibc/004EBF085BBED1029326D56BE8A2E67C08CECE670A94AC1947DF413EF5130EB2
964351ibc/1B38805B1C75352B28169284F96DF56BDEBD9E8FAC005BDCC8CF0378C82AA8E7 
```

And update the commit times in `$HOME/.kujira/config/config.toml`

```bash
sed -i "s/^timeout_commit *=.*/timeout_commit = \"1500ms\"/;" $HOME/.kujira/config/config.toml
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

1. Reload your systemctl and enable the service:

```
sudo systemctl daemon-reload
sudo systemctl enable kujirad
```

1. And finally start the service:

```
sudo systemctl start kujirad
```

1. Check the status of the service:

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

1. Check `kujirad` service logs

```
journalctl -u kujirad -f -o cat
```

And the sync status (make sure `jq` is installed)

```
kujirad status 2>&1 | jq .SyncInfo
```

## Create the validator

Once your node has synced, it's time to create a validator. It can be done on a separate machine if preferred.

Create a key that will be the validators key.

```
kujirad keys add <wallet name>
```

Replace the `<wallet name>` with your desired validator wallet name.

Copy the seed phrase and put it somewhere safe.

You will need to make note of the address `kujira...` and use that in the faucet to get some coins. You can check your balance via

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
kujirad tx staking create-validator \
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

Please remember to also back up `$HOME/.kujira/config/priv_validator_key.json`. If you lose this, you are toast.

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
