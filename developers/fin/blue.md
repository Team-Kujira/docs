# Token Factory

The Token Factory allows you to create your own native denoms, as recognised by the Cosmos SDK Bank Module.&#x20;

This allows your protocol to issue its own token, without needing to support the CW20 standard. It means that all tokens on the Kujira network are compatible as gas-fee payments, and can be collected as protocol revenue and distributed to KUJI stakers.&#x20;

### CLI

Create a denom

```
kujirad tx denom create-denom mydenom
```

Mint it

```
kujirad tx denom mint 10000factory/kujira12345/mydenom kujira123...
```

and Burn it

```
kujirad tx denom burn 10000factory/kujira12345/mydenom 
```

### CosmWASM Bindings

These commands can also be issued via your smart contracts. Please refer to the bindings published in kujira-rs:&#x20;

{% embed url="https://docs.rs/kujira/0.7.5/kujira/msg/enum.KujiraMsg.html" %}

#### Creation

In order for the contract to be able to mint and burn a denom, it will need to be created by the contract itself, often upon instantation:&#x20;

```rust
use kujira::msg::{DenomMsg, KujiraMsg};

#[cfg_attr(not(feature = "library"), entry_point)]
pub fn instantiate(
    deps: DepsMut<KujiraQuery>,
    env: Env,
    _info: MessageInfo,
    msg: InstantiateMsg,
) -> Result<Response<KujiraMsg>, ContractError> {
    let addr = env.contract.address;
    let denom = format!("factory/{addr}/{denom}");
    let config = Config::new(msg.owner, denom);
    
    CONFIG.save(deps.storage, &config)?;
    Ok(Response::default()
        .add_message(DenomMsg::Create {
            subdenom: msg.denom,
        }))
}
```

#### Minting & Burning

Now your contract is the owner of the denom, we can mint and burn tokens. Here is an example contract whose purpose is to provide a permissioned list of addresses that can mint and burn, instead of just the admin:

```rust
#[cfg_attr(not(feature = "library"), entry_point)]
pub fn execute(
    deps: DepsMut<KujiraQuery>,
    _env: Env,
    info: MessageInfo,
    msg: ExecuteMsg,
) -> Result<Response<KujiraMsg>, ContractError> {
    let mut c = CONFIG.load(deps.storage)?;
    match msg {
        ExecuteMsg::Burn {} => {
            let amt = amount(&c.denom, info.funds)?;
            c.validate_permitted(info.sender)?;

            Ok(Response::default()
                .add_attributes(vec![attr("action", "burn"), attr("amount", amt)])
                .add_message(CosmosMsg::Custom(KujiraMsg::Denom(DenomMsg::Burn {
                    denom: c.denom,
                    amount: amt,
                }))))
        }
        ExecuteMsg::Mint { amount, recipient } => {
            c.validate_permitted(info.sender)?;
            Ok(Response::default()
                .add_attributes(vec![attr("action", "mint"), attr("amount", amount)])
                .add_message(CosmosMsg::Custom(KujiraMsg::Denom(DenomMsg::Mint {
                    denom: c.denom,
                    amount,
                    recipient,
                }))))
        }
        ExecuteMsg::Permit { address } => {
            c.validate_owner(info.sender)?;
            c.permit(address.clone());
            CONFIG.save(deps.storage, &c)?;
            Ok(Response::default()
                .add_attributes(vec![attr("action", "permit"), attr("address", address)]))
        }
    }
}
```
