---
description: Submit a community pool spend proposal
---

# Submit a Proposal

Submit a community pool spend proposal along with an initial deposit. The proposal details must be supplied via a JSON file.

Example:

`$ kujirad tx gov submit-proposal community-pool-spend <path/to/proposal.json> --from=<key_or_address>`

Where proposal.json contains:

```
{
  "title": "Community Pool Spend",
  "description": "Protocol Launch Application",
  "recipient": "kujira1s5afhd6gxevu37mkqcvvsj8qeylhn0rz46zdlq",
  "amount": "10000000ukuji",
  "deposit": "10000000ukuji"
}
```

`kujirad tx gov submit-proposal community-pool-spend [proposal-file] [flags]`

### Options

```
  -a, --account-number uint      The account number of the signing account (offline mode only)
  -b, --broadcast-mode string    Transaction broadcasting mode (sync|async|block) (default "sync")
      --dry-run                  ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it
      --fee-account string       Fee account pays fees for the transaction instead of deducting from the signer
      --fees string              Fees to pay along with transaction; eg: 10uatom
      --from string              Name or address of private key with which to sign
      --gas string               gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically (default 200000)
      --gas-adjustment float     adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored  (default 1)
      --gas-prices string        Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom)
      --generate-only            Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase is not accessible)
  -h, --help                     help for community-pool-spend
      --keyring-backend string   Select keyring's backend (os|file|kwallet|pass|test|memory) (default "os")
      --keyring-dir string       The client Keyring directory; if omitted, the default 'home' directory will be used
      --ledger                   Use a connected Ledger device
      --node string              <host>:<port> to tendermint rpc interface for this chain (default "tcp://localhost:26657")
      --note string              Note to add a description to the transaction (previously --memo)
      --offline                  Offline mode (does not allow any online functionality
  -o, --output string            Output format (text|json) (default "json")
  -s, --sequence uint            The sequence number of the signing account (offline mode only)
      --sign-mode string         Choose sign mode (direct|amino-json), this is an advanced feature
      --timeout-height uint      Set a block timeout height to prevent the tx from being committed past a certain height
  -y, --yes                      Skip tx broadcasting prompt confirmation
```
Once a proposal is submitted, there is a deposit window of 24h. in which a threshold of 10.000 KUJI needs to be reached from the proposer's or any community member's wallet for the proposal to be deposited on chain and start the voting period (48h.) 

There UI on https://blue.kujira.app/govern under each proposal allows users to support the ones they believe in with the deposit amount required.

The KUJI tokens deposited need to be liquid (not staked) and are returned to each wallet after the 10.000 KUJI threshold is reached. If the 10.000 KUJI threshold is not met during the 24h. deposit period, the deposited tokens are burned. 
