# Installation

## Manual Node Setup

for install manually follow this step

Official Documentation :

> [Run Scan Node](https://docs.forta.network/en/latest/scanner-quickstart/)

Explorer :

> https://explorer.forta.network/network

### Minimum Hardware Requirement

* CPU : 8 Core
* Ram : 16GB
* Disk : 100GB

### Things to Prepare

**1. Wallet address with fund 1 MATIC in Polygon Network to fund scanner address and used for owner address.**

**2. json-RPC url, you can get it from https://www.alchemy.com/. choose network API**

### 1. Update Packages

```
sudo apt update && sudo apt upgrade -y
```

### 2. Install Docker

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt install docker-ce
```

#### 2.1 Configure address pool

```
sudo nano /etc/docker/daemon.json
{
   "default-address-pools": [
        {
            "base":"172.17.0.0/12",
            "size":16
        },
        {
            "base":"192.168.0.0/16",
            "size":20
        },
        {
            "base":"10.99.0.0/16",
            "size":24
        }
    ]
}
sudo systemctl restart docker
```

### 3. Install Forta

```
sudo curl https://dist.forta.network/pgp.public -o /usr/share/keyrings/forta-keyring.asc -s
sudo echo 'deb [signed-by=/usr/share/keyrings/forta-keyring.asc] https://dist.forta.network/repositories/apt stable main' | sudo tee -a /etc/apt/sources.list.d/forta.list
sudo apt-get update
sudo apt-get install forta
```

#### 3.1 Initialize Forta

```
forta init --passphrase <Type_your_password>
```

> you will see scanner address, send 0.1 MATIC to this address. to see your scanner address again just run `forta account address`

#### 3.2 Update configure file

```
rm /root/.forta/config.yml
sudo tee /root/.forta/config.yml > /dev/null <<EOF
chainId: 42161

scan:
  jsonRpc:
    url: [API_url from alchemy]

trace:
  enabled: false
EOF
```

> `[API_url from alchemy]` -> fill this with API you getting from alchemy

#### 3.3 Register scanner address

```
forta register --owner-address <Metamask_address> --passphrase <your_password>

```

### 4 configure system service

```
sudo tee /lib/systemd/system/forta.service > /dev/null <<EOF
[Unit]
Description=Forta
After=network-online.target
Wants=network-online.target systemd-networkd-wait-online.service

StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
Environment="FORTA_DIR=[LINK_TO_FORTA_DIRECTORY]"
Environment="FORTA_PASSPHRASE=[YOUR_PASSPHRASE]"
Restart=on-failure
RestartSec=15s

ExecStart=/usr/bin/forta run

[Install]
WantedBy=multi-user.target
EOF
```

### 5. Start Service

```
sudo systemctl enable forta
sudo systemctl daemon-reload
sudo systemctl start forta
```

### 6. Check status

```
forta status
```

## Usefull commands

get forta scan node address

```
forta account address
```

Check scan node status

```
forta status
```

Check asociated bots

```
docker ps | grep docker-entrypoint | wc -l
```

Check scan node logs

```
journalctl -u forta -f -o cat
```

stop forta

```
systemctl stop forta
```

start forta

```
systemctl start forta
```

## Testnet rewards

Check your SLA

```
curl https://api.forta.network/stats/sla/scanner/<FORTA_SCANNER_ADDRESS>?startTime=2022-04-24T00:00:00Z | jq .statistics.avg
```

SLA Score will determine if and how much of the reward each scan node gets. During 75% or more node's running time each week:

* 100% reward: SLA ≥ 0.9
* 80% reward: SLA ≥ 0.75
* No reward: SLA < 0.75
