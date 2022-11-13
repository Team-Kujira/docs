# 🛠 Create a validator

## Introduction

Once your node has synced, it's time to create a validator. It can be done on a separate machine if preferred.

## Add validator wallet

1. Create the wallet and a password for the keyring. Replace `<wallet>` with any name you like, just make sure to remember it!

```bash
kujirad keys add <wallet>
```
2. Store your wallet seed and keyring password somewhere safe. Use the command below if you ever need to recover it.

```bash
kujirad keys add --recover <wallet>
```

3. Get some tokens to send the ```create-validator```tx. You can check your balance via

```shell
kujirad query bank balances kujira....
```

The next part is associating your node with your account, creating the validator

## Send the create-validator tx
- Replace `<moniker>` with your validator display name.
- Replace `<wallet>` with the name of your validator wallet.
- Set the `--commission` values to your desired commission rates.
- Modify the chain-id from `kaiyo-1` if mainnet isn't the target.

```bash
kujirad tx staking create-validator \
    --moniker=<moniker> \
    --amount=1000000ukuji \
    --pubkey=$(kujirad tendermint show-validator) \
    --from=<wallet> \
    --chain-id=kaiyo-1 \
    --commission-max-change-rate=0.02 \
    --commission-max-rate=0.15 \
    --commission-rate=0.05 \
    --min-self-delegation=1 \
    --gas=auto \
    --gas-prices=0.00125ukuji \
    --gas-adjustment=1.5
```

## Backup your keys!
It's very important to keep a secure copy of your validator's private key, 
which will allow you to recreate the validator if anything happens to your server.
Take a backup of this file: `$HOME/.kujira/config/priv_validator_key.json`.
If you restore it to a new node, it will begin signing blocks as your validator.
Be very careful! Signing from two nodes at the same time will result in a hard slash 
and jailing.
