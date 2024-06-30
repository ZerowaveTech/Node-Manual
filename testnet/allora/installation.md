# Installation

## Overview

This document creates a setup where the worker node is supported by a side node providing inferences. They communicate through an endpoint so the worker will request inferences to the side node (the Inference Server). This makes an ultra-light worker node.

## Website

* [Dashboard](https://app.allora.network/points/overview) -> Connect Keplr Wallet&#x20;
* [Faucet](https://faucet.edgenet.allora.network/) -> get faucet from here
* [Chain Explorer](https://explorer.edgenet.allora.network/wallet/suggest)

## Install Requirement Packages

### Update Package

```bash
sudo apt update -y && sudo apt upgrade -y
sudo apt install ca-certificates zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev curl git wget make jq build-essential pkg-config lsb-release libssl-dev libreadline-dev libffi-dev gcc screen unzip lz4 -y
```

### Install Docker

[docker.md](../../packages/docker.md "mention")

### Install Go

[go.md](../../packages/go.md "mention")

## Install Allora CLI

{% hint style="info" %}
This for create wallet or import wallet
{% endhint %}

```bash
git clone https://github.com/allora-network/allora-chain.git
cd allora-chain && make all
allorad version
```

### Import Wallet

{% hint style="info" %}
must have keplr wallet and create on there, backup mnemonic on keplr
{% endhint %}

```bash
alorad keys add wallet --recover
```

> change `wallet`  name as your preference

{% hint style="danger" %}
Before continue to next step make sure your wallet have balance from [faucet](installation.md#website)
{% endhint %}

## Install Node Worker

```bash
git clone https://github.com/allora-network/basic-coin-prediction-node
cd basic-coin-prediction-node
mkdir worker-data
mkdir head-data
sudo chmod -R 777 worker-data
sudo chmod -R 777 head-data
```

### Create Head-Key

```bash
sudo docker run -it --entrypoint=bash -v ./head-data:/data alloranetwork/allora-inference-base:latest -c "mkdir -p /data/keys && (cd /data/keys && allora-keys)"
```

```basic
sudo docker run -it --entrypoint=bash -v ./worker-data:/data alloranetwork/allora-inference-base:latest -c "mkdir -p /data/keys && (cd /data/keys && allora-keys)"
```

### Back-Up head-id

```bash
cat ~/basic-coin-prediction-node/head-data/keys/identity
```

## Run Worker Node

{% hint style="info" %}
make sure you have `head-id` and `mnemonic` which have balance uAllo
{% endhint %}

```bash
rm -rf docker-compose.yml && vi docker-compose.yml
```

Paste your `head-id` and `mnemonic` on worker-basic-eth-prod

{% hint style="danger" %}
delete \[\[]]
{% endhint %}

```docker
version: '3'

services:
  inference:
    container_name: inference-basic-eth-pred
    build:
      context: .
    command: python -u /app/app.py
    ports:
      - "8000:8000"
    networks:
      eth-model-local:
        aliases:
          - inference
        ipv4_address: 172.22.0.4
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8000/inference/ETH"]
      interval: 10s
      timeout: 5s
      retries: 12
    volumes:
      - ./inference-data:/app/data
  
  updater:
    container_name: updater-basic-eth-pred
    build: .
    environment:
      - INFERENCE_API_ADDRESS=http://inference:8000
    command: >
      sh -c "
      while true; do
        python -u /app/update_app.py;
        sleep 24h;
      done
      "
    depends_on:
      inference:
        condition: service_healthy
    networks:
      eth-model-local:
        aliases:
          - updater
        ipv4_address: 172.22.0.5
  
  head:
    container_name: head-basic-eth-pred
    image: alloranetwork/allora-inference-base-head:latest
    environment:
      - HOME=/data
    entrypoint:
      - "/bin/bash"
      - "-c"
      - |
        if [ ! -f /data/keys/priv.bin ]; then
          echo "Generating new private keys..."
          mkdir -p /data/keys
          cd /data/keys
          allora-keys
        fi
        allora-node --role=head --peer-db=/data/peerdb --function-db=/data/function-db  \
          --runtime-path=/app/runtime --runtime-cli=bls-runtime --workspace=/data/workspace \
          --private-key=/data/keys/priv.bin --log-level=debug --port=9010 --rest-api=:6000 \
          --boot-nodes=/dns4/head-0-p2p.v2.testnet.allora.network/tcp/32130/p2p/12D3KooWGKY4z2iNkDMERh5ZD8NBoAX6oWzkDnQboBRGFTpoKNDF
    ports:
      - "6000:6000"
    volumes:
      - ./head-data:/data
    working_dir: /data
    networks:
      eth-model-local:
        aliases:
          - head
        ipv4_address: 172.22.0.100

  worker:
    container_name: worker-basic-eth-pred
    environment:
      - INFERENCE_API_ADDRESS=http://inference:8000
      - HOME=/data
    build:
      context: .
      dockerfile: Dockerfile_b7s
    entrypoint:
      - "/bin/bash"
      - "-c"
      - |
        if [ ! -f /data/keys/priv.bin ]; then
          echo "Generating new private keys..."
          mkdir -p /data/keys
          cd /data/keys
          allora-keys
        fi
        # Change boot-nodes below to the key advertised by your head
        allora-node --role=worker --peer-db=/data/peerdb --function-db=/data/function-db \
          --runtime-path=/app/runtime --runtime-cli=bls-runtime --workspace=/data/workspace \
          --private-key=/data/keys/priv.bin --log-level=debug --port=9011 \
          --boot-nodes=/ip4/172.22.0.100/tcp/9010/p2p/[[head-id]] \
          --topic=1 --allora-chain-worker-mode=worker \
          --allora-chain-key-name=zerowave-wallet \
          --allora-chain-restore-mnemonic='[[ MNEMONIC ]]' \
          --allora-chain-topic-id=1 \
          --allora-node-rpc-address=https://allora-rpc.edgenet.allora.network/ 
    volumes:
      - ./worker-data:/data
    working_dir: /data
    depends_on:
      - inference
      - head
    networks:
      eth-model-local:
        aliases:
          - worker
        ipv4_address: 172.22.0.10


  
networks:
  eth-model-local:
    driver: bridge
    ipam:
      config:
        - subnet: 172.22.0.0/24

volumes:
  inference-data:
  worker-data:
  head-data:
```

```bash
docker compose up --build -d
```

{% hint style="danger" %}
check your docker must running not exited
{% endhint %}

### Check Running Node

```bash
curl --location 'http://localhost:6000/api/v1/functions/execute' \
--header 'Content-Type: application/json' \
--data '{
    "function_id": "bafybeigpiwl3o73zvvl6dxdqu7zqcub5mhg65jiky2xqb4rdhfmikswzqm",
    "method": "allora-inference-function.wasm",
    "parameters": null,
    "topic": "1",
    "config": {
        "env_vars": [
            {
                "name": "BLS_REQUEST_PATH",
                "value": "/api"
            },
            {
                "name": "ALLORA_ARG_PARAMS",
                "value": "ETH"
            }
        ],
        "number_of_nodes": -1,
        "timeout": 2
    }
}'
```

**Response**&#x20;

```json
{
  "code": "200",
  "request_id": "03001a39-4387-467c-aba1-c0e1d0d44f59",
  "results": [
    {
      "result": {
        "stdout": "{\"value\":\"2564.021586281073\"}",
        "stderr": "",
        "exit_code": 0
      },
      "peers": [
        "12D3KooWG8dHctRt6ctakJfG5masTnLaKM6xkudoR5BxLDRSrgVt"
      ],
      "frequency": 100
    }
  ],
  "cluster": {
    "peers": [
      "12D3KooWG8dHctRt6ctakJfG5masTnLaKM6xkudoR5BxLDRSrgVt"
    ]
  }
}
```
