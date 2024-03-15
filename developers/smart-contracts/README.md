---
cover: ../../.gitbook/assets/docs-banner.png
coverY: 0
---

# Smart Contracts

The Kujira blockchain is fully enabled with CosmWASM v1.0 and IBC v3 support, allowing you as a developer to build Rust-based smart contracts that interact with the home.

## Getting Started

If you are new to CosmWASM and Smart Contracts, we recommend checking out the CW-Template repo and familiarising yourself with the basic interfaces and model of CosmWASM smart contracts.&#x20;

{% embed url="https://github.com/InterWasm/cw-template" %}

When you are ready to deploy, you will need a local build of the chain core, in order to store your code on-chain and submit governance proposals to instantiate it.

```bash
git clone https://github.com/Team-Kujira/core
cd core
make install
```

### Deployment

You're now ready to store your code on-chain:

```bash
cargo run-script optimize
kujirad keys add <local-account>
# This will generate an account for you, provide you with a seed phrase which 
# you must store safely, and the associated kujira address. You will need to 
# fund this address with KUJI tokens before the next step
kujirad tx wasm store <./path/to/optimized/code.wasm> --from <local-account>
```

This will generate some logs when successfully broadcast, which contains the `code_id`:&#x20;

```yaml
logs:
- events:
  - attributes:
    - key: action
      value: /cosmwasm.wasm.v1.MsgStoreCode
    - key: module
      value: wasm
    - key: sender
      value: kujira1...
    type: message
  - attributes:
    - key: code_id
      value: "4"
    type: store_code
```

### Instantiation

Your code is now stored on-chain. You can think of it a little like a Class in an object-oriented lanaguage. We now need to create an instance of it that we can interact with.&#x20;

On Kujira, this must be done via a governance proposal, in order to maintain the quality of code and dapps running on the network.&#x20;

```bash
kujirad tx gov submit-proposal instantiate-contract 4 \
  '{"count": 0}' \
  --title "Instantiate CW-Template" \
  --description "A more detailed description of this proposal" \
  --label "CW-Template" \
  --from <local-account> \
  --admin <local-account-address> \
  --run-as <local-account-address> \
  --gas 1000000 \
  --fees 1250ukuji
```

This will create the Proposal at a funding stage. You can then visit [https://blue.kujira.app/govern](https://blue.kujira.app/govern) to fund the proposal deposit, and open it for voting.

Upon the vote passing, the contract will be instantiated and the instance of the contract will have its own address. You can find the address as so:

```bash
kujirad query wasm list-contract-by-code 4
```

You can now move on to building the UI for your newly deployed smart contract.

{% content-ref url="../dapp-front-ends/" %}
[dapp-front-ends](../dapp-front-ends/)
{% endcontent-ref %}

## Custom Modules

{% content-ref url="oracle.md" %}
[oracle.md](oracle.md)
{% endcontent-ref %}

{% content-ref url="token-factory.md" %}
[token-factory.md](token-factory.md)
{% endcontent-ref %}

{% content-ref url="scheduler.md" %}
[scheduler.md](scheduler.md)
{% endcontent-ref %}
