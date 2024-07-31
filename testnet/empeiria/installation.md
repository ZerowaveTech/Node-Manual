---
description: Installation guide for empeiria network
---

# Installation

## Prerequisite

### Install Go

{% content-ref url="../../packages/go.md" %}
[go.md](../../packages/go.md)
{% endcontent-ref %}

### Faucet Token

1. You can get from telegram group validator and chat Admin
2. [Faucet Website](https://faucet-testnet.empe.io/)

## Install

### Get the binary

```bash
mkdir -p ~/go/bin
curl -LO https://github.com/empe-io/empe-chain-releases/raw/master/v0.1.0/emped_linux_amd64.tar.gz
tar -xvf emped_linux_amd64.tar.gz
sudo mv emped ~/go/bin
chmod u+x ~/go/bin/emped
```

### Initilization

```bash
emped init [Your-node-name] --chain-id empe-testnet-2
emped config chain-id empe-testnet-2
emped config keyring-backend test
```

{% hint style="info" %}
change `[Your-node-name]` with your name you like
{% endhint %}

### Configuration

{% hint style="info" %}
you can change `PORT` with number anything you want
{% endhint %}

{% code overflow="wrap" %}
```bash
PORT=20
emped config node tcp://localhost:${PORT}657

# change port configuration
sed -i -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:${PORT}658\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:${PORT}657\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:${PORT}060\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:${PORT}656\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":${PORT}660\"%" $HOME/.empe-chain/config/config.toml
sed -i -e "s%^address = \"tcp://localhost:1317\"%address = \"tcp://localhost:${PORT}317\"%; s%^address = \":8080\"%address = \":${PORT}080\"%; s%^address = \"localhost:9090\"%address = \"localhost:${PORT}090\"%; s%^address = \"localhost:9091\"%address = \"localhost:${PORT}091\"%" $HOME/.empe-chain/config/app.toml

# add genesis file and address book
wget -O $HOME/.empe-chain/config/genesis.json https://raw.githubusercontent.com/empe-io/empe-chains/master/testnet-2/genesis.json
wget -O $HOME/.empe-chain/config/addrbook.json https://raw.githubusercontent.com/vinjan23/Testnet.Guide/main/Empeiria/addrbook.json

# configure peers and seed
peers="7419cc5bafc3c9c49b18ec67e3263344cbcc30f2@49.13.215.45:43656,91fb8e75a4b92589211d47d5a9ce934d32733043@116.202.48.104:26656,771b5350519d6081784f70d9be692e76b635529a@188.245.88.126:43656,06bd2afb77d94d2f3c5fe8abbdabb4499ca95793@65.21.97.150:40656,5406f64d38f433cca31c2f6e96d5619fa92be5b5@168.119.179.250:26656,e941537fbe6d86c9bf58aeb880e3212dc3f82086@84.247.141.94:656,94529b5e044f208d1869980f456a53fcef8fb321@14.167.155.13:43656,829207ca2cf7debb16787a79c9fc1aa94e9b55ea@116.203.238.65:43656,080d9cc12e08fb64dd0f4528d0da4a84d5d9428e@37.27.83.234:26656,9e120e5cb5822fbb224d5c1ae2c7f0149b80fc99@45.67.216.220:43656"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.empe-chain/config/config.toml
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0uempe\"/" $HOME/.empe-chain/config/app.toml

#set pruning 
sed -i \
-e 's|^pruning *=.*|pruning = "custom"|' \
-e 's|^pruning-keep-recent *=.*|pruning-keep-recent = "100"|' \
-e 's|^pruning-keep-every *=.*|pruning-keep-every = "2000"|' \
-e 's|^pruning-interval *=.*|pruning-interval = "10"|' \
$HOME/.empe-chain/config/app.toml

# add indexer
sed -i 's|^indexer *=.*|indexer = "null"|' $HOME/.empe-chain/config/config.toml
```
{% endcode %}

## Running Node

```bash
# Set Service file
sudo tee /etc/systemd/system/emped.service > /dev/null <<EOF
[Unit]
Description=empe testnet node
After=network-online.target
[Service]
User=$USER
ExecStart=$(which emped) start
Restart=always
RestartSec=3
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
EOF
sudo systemctl daemon-reload
sudo systemctl enable emped
```

```bash
sudo systemctl start emped && sudo journalctl -fu emped -o cat
```

## Add Wallet

```bash
emped keys add wallet
```

{% hint style="danger" %}
BACKUP OUTPUT COMMAND AND IMPORT TO KEPLR
{% endhint %}
