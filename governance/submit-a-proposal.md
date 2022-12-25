---
description: Submit a community pool spend proposal
---

# 🗄 Submit a Governance Proposal

As a member of the Kujira community, you have the opportunity to submit proposals for consideration by the network. One type of proposal is a community pool spend proposal, which involves requesting funds from the community pool for a specific purpose.

To submit a community pool spend proposal, you will need to provide a JSON file with the proposal details and an initial deposit. Here is an example of the command to use:

Example:

`$ kujirad tx gov submit-proposal community-pool-spend <path/to/proposal.json> --from=<key_or_address>`

Where proposal.json contains the following information:

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

There are several options and flags that can be used with this command, including --account-number, --broadcast-mode, --dry-run, --fee-account, --fees, --from, --gas, --gas-adjustment, --gas-prices, --generate-only, --keyring-backend, --keyring-dir, --ledger, --node, --note, --offline, --output, --sequence, --sign-mode, --timeout-height, and --yes.

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

Once a proposal is submitted, there is a 24-hour deposit window during which a threshold of 10,000 KUJI must be reached from the proposer's wallet or any other community member's wallet in order for the proposal to be deposited on-chain and the voting period (48 hours) to begin. The KUJI tokens deposited must be liquid (not staked) and will be returned to the wallet after the threshold is met. If the threshold is not met during the deposit period, the deposited tokens will be burned.

Users can support proposals they believe in by depositing the required amount through the UI on https://blue.kujira.app/govern. Simply navigate to the proposal and use the deposit feature to contribute.
