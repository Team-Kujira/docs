# KUJI testnet

This guide assumes you're running on Ubuntu 22.04 LTS - the commands will probably work just fine on 20.04 LTS or Debian.

Download the zip file from Discord, and ensure that you have `ssh` and `scp` available on your own machine.

## Basic Machine setup

1. ssh into your node
2. update your machine `sudo apt update && sudo apt dist-upgrade -y`. Answer yes / ok to the prompts
3. install required tools tools `sudo apt install build-essential git unzip curl wget`

### Golang and ignite

First off we install go 1.18.x

1. `wget https://go.dev/dl/go1.18.2.linux-amd64.tar.gz`
2. extract the runtime `sudo tar -C /usr/local -xzf go1.18.2.linux-amd64.tar.gz`
3. Add go to your path

```
export PATH=$PATH:/usr/local/go/bin
export PATH=$PATH:$(go env GOPATH)/bin
```

1. get the ignite cli `curl https://get.ignite.com/cli! | bash` (chek out their site: https://docs.ignite.com/)
2. check that ignite works `ignite version` - should produce output like

```
Ignite CLI version:	v0.21.2
Ignite CLI build date:	2022-05-16T18:58:45Z
Ignite CLI source hash:	83cee38e68fe3dd7cdf48a1a7881ac553a281042
...
```

## Get the zip to the machine

From your local machine you need copy the downloaded zip onto the server. Use `scp` for this:

```bash
scp kujira-core.zip <user>@<ip or host>:/tmp
```

Replacing the `<user>` with your linux machine's user and the `<ip or host>` with the provisioned IP from your cloud provider

## Get the testnet up and running

Now we're back on the server. First off we add a new non-root user that can run the network

```
sudo useradd -m kuji
```

And we assume the user

```
sudo su -l kuji
```

Time to unzip and prep the source code

1. `mv /tmp/kujira-core.zip $HOME`
2. `cd $HOME && unzip kujira-core.zip && mv kujira-core kujira-core-bundle`
3. `mkdir kujira-core`
4. `cd kujira-core && git init && git remote add bundle ../kujira-core-bundle/kujira-core.bundle && git pull bundle master`

## Now we build!

Time to ignite the build sequence

1. Ensure go is in our path (also add it to the end of your `.bashrc` file)

```
export PATH=$PATH:/usr/local/go/bin
export PATH=$PATH:$(go env GOPATH)/bin
```

1. `ignite chain build`

A successful build produces output like

```
Cosmos SDK's version is: stargate - v0.45.4


🛠️  Building proto...
📦 Installing dependencies...
🛠️  Building the blockchain...
🗃  Installed. Use with: kujirad
```

## Running the test net

If the build succeed you should now have the `kujirad` cli in your path.

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

## Join the test net

Now we can initialize and join the network

1. Initialize

```
export CHAIN_ID=harpoon-1
kujirad init <moniker name> --chain-id ${CHAIN_ID}
```

Replacing `<moniker name>` with your desired name.

1. Place the `genesis.json` file from the downloaded zip

```
cp $HOME/kujira-core-bundle/genesis.json $HOME/.kujira/config/
```

1. Place the `addressbook` from the downloaded zip

```
cp $HOME/kujira-core-bundle/addrbook.json $HOME/.kujira/config/
```

Now try to start the network

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

And then a whole bunch of log messages while your node is catching up. If this is now verified working it's time to install it as a system level service so it always starts with the machine

## Registering as a service

Drop out of the `kuji` user if you're still in that terminal session. Write `exit` or type `ctrl+d` on your keyboard

1. Create a service definition file in `/etc/systemd/system/kujirad.service`. Example file that fits with our kuijrad install and kuji runtime user:

```
[Unit]
Description=Kujira Daemon
After=network.target

[Service]
Type=simple
User=kuji
ExecStart=/home/kuji/go/bin/kujirad start --log-level error 
Restart=on-abort

[Install]
WantedBy=multi-user.target

[Service]
LimitNOFILE=65535  
```

1. Reload your systemctl `sudo systemctl daemon-reload` and enable the service `sudo systemctl enable kujirad`
2. And finally start the service with `sudo systemctl start kujirad`
3. Check the status of the service with `systemctl status kujirad.service` - it should return something like

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

Once your node is synced. it is time to make it a validator.
this can be done on a seperate machine if preferred.

create a key that will be the validators key. I have chosen the creative name of 'validator'
```
kurjiad keys add validator
```
copy the seed phrase and put it somewhere safe.
you will need to also make note of the address "kujira..." and use that in the faucet to get some coins.
you can check your balance via
```
 kujirad query bank balances kujira....
 ```

The next part is associating your node with your account, creating the validator
``` 

export PUBKEY=$( kujirad tendermint show-validator)
kujirad tx staking create-validator --moniker=*your moniker* \
 --amount=1000000ukuji \
        --gas-prices=1ukuji \
        --pubkey=$PUBKEY \
         --from=validator \
        --yes \
        --node=tcp://localhost:26657 \
        --chain-id=harpoon-1 \
        --commission-max-change-rate=0.01 \
        --commission-max-rate=0.20 \
        --commission-rate=0.10 \
        --min-self-delegation=1
```
now your node should be present. 
```
kujirad query staking validators|grep details
```
please remember to also back up  .kujira/config/priv_validator_key.json
if you lose this, you are toast.


## Tips
### disk utilization
to help manage the disk size you can prune the blocks being kept. for this I use prime numbers pick your own 
in app.toml
```
pruning = "custom"

# These are applied if and only if the pruning strategy is custom.
pruning-keep-recent = "809"
pruning-keep-every = "0"
pruning-interval = "43"
```
you should also check what you are indexing
```
index-events = ["tx.hash", "tx.height"]
```
### adding more peers.
you should modify /etc/security/limits.conf 
and add
```
*                soft    nofile          65535
*                hard    nofile          65535
```
you can then modify the config.yaml to increase connections. This may cost you more in ingress/egress charges.
```
max_open_connections = 1900
max_num_inbound_peers = 50
max_num_outbound_peers = 50
```
