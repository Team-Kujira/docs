# Run a Node

This guide assumes you're running on Ubuntu 22.04 LTS - the commands will probably work just fine on 20.04 LTS or Debian.

## Basic machine setup

1. SSH into your node
2. Update your machine (Answer yes / ok to the prompts)

```
sudo apt update && sudo apt dist-upgrade -y
```

3. Install required tools

```
sudo apt install build-essential git unzip curl wget
```

## Prepare environment

Best practice is to run node software on an isolated unprivileged user. We'll create the ```kuji``` user in this guide; if your username is different change it wherever it appears. 

```
sudo useradd -m -s /bin/bash kuji
```

### Install Golang

Download `go` and extract go 1.18.5

```
# remove old go version

sudo rm -rvf /usr/local/go/

# download and install recent go version

curl -fsSL https://golang.org/dl/go1.18.5.linux-amd64.tar.gz | sudo tar -xzC /usr/local

# remove unneeded installer
rm go1.18.5.linux-amd64.tar.gz

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

## Build node binary

1. Login as ```kuji```(skip if you already did)

```
sudo su -l kuji
```

2. Download the project code and checkout to mainnet branch

```bash
git clone https://github.com/Team-Kujira/core $HOME/kujira-core
cd $HOME/kujira-core
git checkout v0.7.1
make install
```

3. Verify your binary is working

```
kujirad version #should output v0.7.1
```

## Configure chain

This section is written for mainnet (kaiyo-1); modify the ID, genesis, and seeds as needed.

1. Login as kuji (skip if you're already logged in).

```
sudo su -l kuji
```

2. Initialize config files and dirs. Replace <moniker> with a public name for your node.

```
kujirad init --chain-id kaiyo-1 <moniker>
```
3. Download the kaiyo-1 genesis.json.

```
curl -fsSL -o $HOME/.kujira/config/genesis.json https://raw.githubusercontent.com/Team-Kujira/networks/master/mainnet/kaiyo-1.json
```
4. Set the chain-id. This will save it in client.toml so you won't need --chain-id again.

```
kujirad config chain-id kaiyo-1
```

5. Set some defaults in config.toml and app.toml.

```
sed -i 's/^timeout_commit =.*/timeout_commit = "1500ms"/' $HOME/.kujira/config/config.toml
sed -i "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.00119ukuji,0.00150ibc\/295548A78785A1007F232DE286149A6FF512F180AF5657780FC89C009E2C348F,0.000125ibc\/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2,0.00126ibc\/47BD209179859CDE4A2806763D7189B6E6FE13A17880FE2B42DE1E6C1E329E23,0.00652ibc\/3607EB5B5E64DD1C0E12E07F077FF470D5BC4706AFCBC98FE1BA960E5AE4CE07,617283951ibc\/F3AA7EF362EC5E791FE78A0F4CCC69FEE1F9A7485EB1A8CAB3F6601C00522F10,0.000288ibc\/EFF323CC632EC4F747C61BCE238A758EFDB7699C3226565F7C20DA06509D59A5,5ibc\/DA59C009A0B3B95E0549E6BF7B075C8239285989FF457A8EDDBB56F10B2A6986,0.00137ibc\/A358D7F19237777AF6D8AD0E0F53268F8B18AE8A53ED318095C14D6D7F3B2DB5,0.0488ibc\/4F393C3FCA4190C0A6756CE7F6D897D5D1BE57D6CCB80D0BC87393566A7B6602,78492936ibc\/004EBF085BBED1029326D56BE8A2E67C08CECE670A94AC1947DF413EF5130EB2,964351ibc\/1B38805B1C75352B28169284F96DF56BDEBD9E8FAC005BDCC8CF0378C82AA8E7\"/;" $HOME/.kujira/config/app.toml
```

6. (Optional) Configure some seeds. This will help your node find peers.

```
sed -i 's/^seeds =.*/seeds = "[email protected]rg:31897,[email protected]:11856"/' $HOME/.kujira/config/config.toml
```

## Start the node

The node is now ready to go.

1. (Optional) [State-sync](/validators/run-a-node/state-sync.md) if you want a head start over syncing from scratch.

2. Start syncing blocks

```bash
kujirad start
```

And then watch a fair amount of log messages while your node is catching up. After making sure that it works, it's time to install it as a system level service so it always starts with the machine.

## Register the node as a service

A systemd service will keep `kujirad` running in the background and restart it if it stops.

1. Create the service file with `sudo` using your favorite text editor in `/etc/systemd/system/kujirad.service `.

```
[Unit]
Description=kujirad
After=network.target

[Service]
Type=simple
User=kuji
ExecStart=/home/kuji/go/bin/kujirad start
Restart=on-abort
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target  
```

2. Reload `systemd` to pick up the new service.
```bash
sudo systemctl daemon-reload
```
3. Start the service.
```bash
sudo systemctl start kujirad
```
4. Tail your service logs.
```bash
sudo journalctl -fu kujirad
```
5. (Optional) Enable the service. This will set it to start on every boot.
```bash
sudo systemctl enable kujirad
```
