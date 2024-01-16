# Installation

## Overview

An **archive node** is responsible for preserving the historical records of block transactions. Typically, this type of node is utilized as an **RPC (Remote Procedure Call)** endpoint. The role of RPC in our network is indispensable as it bridges the gap between users, decentralized applications (dApps), and the blockchain, leveraging WebSocket and HTTP endpoints for this connection. For instance, in our network, the public endpoints deploy archive nodes to facilitate seamless access to BEVM chains for all users.

It is advisable for **DApp** developers to set up their own dedicated RPC archival node. This approach not only allows them to fetch the blockchain data they require but also reduces their reliance on public infrastructures, which may suffer from slower response times and restricted access due to heavy usage and rate limits.

## Docker Installation

### install Docker on VPS

```
curl -fsSL https://get.docker.com -o get-docker.sh
```

run the shell&#x20;

```
sudo sh get-docker.sh
```

### Mapping Host for Store Data

```
cd /var/lib
```

create new directory

```
mkdir node_bevm_test_storage
```

### Fetch Docker Image

```
sudo docker pull btclayer2/bevm:v0.1.1
```

### Run Program

```docker
 sudo docker run -d -v /var/lib/node_bevm_test_storage:/root/.local/share/bevm btclayer2/bevm:v0.1.1 bevm "--chain=testnet" "--name=your_node_name" "--pruning=archive" --telemetry-url "wss://telemetry.bevm.io/submit 0"
```

{% hint style="info" %}
replace "--name:your\_own\_name" with evm address to join incentives testnet
{% endhint %}

## Telmetry Check

Check your node in this link

{% embed url="https://telemetry.bevm.io/" %}
