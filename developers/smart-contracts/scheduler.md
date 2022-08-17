# Scheduler

The on-chain scheduler allows you to hook automated contract execution into the end of every N-th block. These are instantiated via governance, as they add computational load and gas costs to every block, so must be managed.&#x20;

Current scheduled tasks can be queried via [https://lcd.kaiyo.kujira.setten.io/kujira/scheduler/hook](https://lcd.kaiyo.kujira.setten.io/kujira/scheduler/hook) or `kujirad query scheduler list-hooks`

And a proposal for hook can be submitted as so

```bash
kujirad tx gov submit-proposal create-hook <contract-addr> <executor-addr> \
  '{"count": 0}' \
  <frequency> \ # i.e. every Nth block 
  1000ukuji \ # funds to provide with each execution
  --title "Instantiate CW-Template" \
  --description "A more detailed description of this proposal" \
  --from <local-account> \
  --fees 250ukuji
```

