# Create a validator

Once your node has synced, it's time to create a validator. It can be done on a separate machine if preferred.

Create a key that will be the validators key.

```
kujirad keys add <wallet name>
```

Replace the `<wallet name>` with your desired validator wallet name.

Copy the seed phrase and put it somewhere safe.

You will need to make note of the address `kujira...` and use that in the faucet to get some coins. You can check your balance via

```shell
kujirad query bank balances kujira....
```

The next part is associating your node with your account, creating the validator

```shell
# Ensure you have your CHAIN_ID and MONIKER_NAME set
export PUBKEY=$(kujirad tendermint show-validator)
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

