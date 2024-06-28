# Usefull Command

### View Key List

```bash
$HOME/nubit-node/bin/nkey list --p2p.network nubit-alphatestnet-1 --node.type light
```

### View node private key

```bash
$HOME/nubit-node/bin/nkey export my_nubit_key --unarmored-hex --unsafe --p2p.network nubit-alphatestnet-1 --node.type light
```

### View node Public Key

```bash
$HOME/nubit-node/bin/nkey list --p2p.network nubit-alphatestnet-1 --node.type light
```

### Import wallet using mnemonic

```bash
$HOME/nubit-node/bin/nkey add my_keplr_key --recover --keyring-backend test --node.type light --p2p.network nubit-alphatestnet-1
```

### Import wallet using private key

```bash
$HOME/nubit-node/bin/nkey import my_nubit_key ~/nubit-da/nubit-node/account1.private --keyring-backend test --node.type light --p2p.network nubit-alphatestnet-1
```

> <pre><code>"<a data-footnote-ref href="#user-content-fn-1">~/nubit-da/nubit-node/account1.private</a>" is your private key location
> </code></pre>

[^1]: 
