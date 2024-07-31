# Installation

## Prerequisite

### Install Go

{% content-ref url="../../packages/go.md" %}
[go.md](../../packages/go.md)
{% endcontent-ref %}

### Faucet

[here](https://testnet.ping.pub/symphony/faucet)

## Install

### Get the binary

```bash
cd $HOME
rm -rf symphony
git clone https://github.com/Orchestra-Labs/symphony
cd symphony
git checkout v0.2.1
make build
```

### Set Bash

```bash
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bashrc
```

### Initialization

```bash
# Set Configuration for your node
symphonyd init [Your-node-name] --chain-in symphony-testnet-2
symphonyd config chain-id symphony-testnet-2
symphonyd config keyring-backend file
```

{% hint style="info" %}
change `[Your-node-name]` with your name you like
{% endhint %}

### Configuration

{% code overflow="wrap" %}
```bash
# Add Genesis File and Addrbook
curl -Ls https://snapshots.indonode.net/symphony/genesis.json > $HOME/.symphonyd/config/genesis.json
curl -Ls https://snapshots.indonode.net/symphony/addrbook.json > $HOME/.symphonyd/config/addrbook.json

#set seed
sed -i -e "s|^seeds *=.*|seeds = \"d1d43cc7c7aef715957289fd96a114ecaa7ba756@testnet-seeds.nodex.one:24810\"|" $HOME/.symphonyd/config/config.toml

#set gas price
sed -i -e "s|^minimum-gas-prices *=.*|minimum-gas-prices = \"0note\"|" $HOME/.symphonyd/config/app.toml

#set prune
sed -i \
  -e 's|^pruning *=.*|pruning = "custom"|' \
  -e 's|^pruning-keep-recent *=.*|pruning-keep-recent = "100"|' \
  -e 's|^pruning-keep-every *=.*|pruning-keep-every = "0"|' \
  -e 's|^pruning-interval *=.*|pruning-interval = "19"|' \
  $HOME/.symphonyd/config/app.toml
  
#set custom port
sed -i -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:24858\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:24857\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:24860\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:24856\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":24866\"%" $HOME/.symphonyd/config/config.toml
sed -i -e "s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:24817\"%; s%^address = \":8080\"%address = \":24880\"%; s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:24890\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:24891\"%; s%:8545%:24845%; s%:8546%:24846%; s%:6065%:24865%" $HOME/.symphonyd/config/app.toml
```
{% endcode %}

## Running node

```bash
sudo tee /etc/systemd/system/symphony.service > /dev/null << EOF
[Unit]
Description=symphony node service
After=network-online.target
 
[Service]
User=$USER
ExecStart=$(which symphony) start
Restart=on-failure
RestartSec=10
LimitNOFILE=65535
Environment="DAEMON_HOME=$HOME/.symphonyd"
Environment="DAEMON_NAME=symphonyd"
Environment="UNSAFE_SKIP_BACKUP=true"
 
[Install]
WantedBy=multi-user.target
EOF
```

```bash
sudo systemctl daemon-reload
sudo systemctl enable symphony
sudo systemctl start symphony && sudo journalctl -fu symphony -o cat
```

## Add Wallet

```bash
symphonyd add keys wallet
```
