# Tips

### Disk utilization

To help manage the disk size you can prune the blocks being kept. for this I use prime numbers pick your own in `app.toml`

```
pruning = "custom"

# These are applied if and only if the pruning strategy is custom.
pruning-keep-recent = "809"
pruning-keep-every = "0"
pruning-interval = "43"
```

You should also check what you are indexing

```
index-events = ["tx.hash", "tx.height"]
```

### Adding more peers

You should modify `/etc/security/limits.conf` and add

```
*                soft    nofile          65535
*                hard    nofile          65535
```

You can then modify the config.toml to increase connections. This may cost you more in ingress/egress charges.

```
max_open_connections = 1900
max_num_inbound_peers = 50
max_num_outbound_peers = 50
```
