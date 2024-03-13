---
description: Submit a community pool spend proposal
---

# Submit a Governance Proposal

As a member of the Kujira community, you have the opportunity to submit proposals for consideration by the network. One type of proposal is a community pool spend proposal, which involves requesting funds from the community pool for a specific purpose.

To submit a community pool spend proposal, you will need to provide a JSON file with the proposal details and an initial deposit. Here is an example of the command to use:

Example:

`$ kujirad tx gov submit-proposal <path/to/proposal.json> --from=<key_or_address>`

Where proposal.json contains the following information:

```
{
 "messages": [
  {
   "@type": "/cosmos.distribution.v1beta1.MsgCommunityPoolSpend",
   "authority": "kujira10d07y265gmmuvt4z0w9aw880jnsr700jt23ame",
   "recipient": "kujira<address_of_receipient>",
   "amount": [{"denom": "ukuji", "amount": "<amount_without_decimals>"}]
  }
 ],
 "metadata": "ipfs://<HAHSH>",
 "deposit": "100000000factory/kujira1qk00h5atutpsv900x202pxx42npjr9thg58dnqpa72f2p7m2luase444a7/uusk",
 "title": "<title>",
 "summary": "<discription>"
}

```

`kujirad tx gov submit-proposal [proposal-file] [flags]`

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

It is best to use the Kujira Discord forum to discuss governance related proposals and matters in advance. This helps crowd-fund proposals, get the wider community engaged in voting, receive valuable community feedback, and gauge community sentiment ahead of proposal submission.&#x20;

To submit a proposal you need an initial deposit of 100 [USK](../dapps-and-infrastructure/usk-stablecoin.md). After that there is a 24-hour window during which a threshold of 500 USK must be reached from the proposer's wallet or any other community members' wallets in order for the proposal to be deposited on-chain and the voting period (48 hours) to begin. Any deposited USK will be returned to the original wallets after the threshold is met. If the threshold is not met during the deposit period, the deposited tokens will be burned.

Users can support proposals they believe in by depositing the required amount through the UI on [https://blue.kujira.app/govern](https://blue.kujira.app/govern). Simply navigate to the proposal and use the deposit feature to contribute.
