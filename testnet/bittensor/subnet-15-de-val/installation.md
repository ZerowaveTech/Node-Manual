# Installation

## Requirement

#### Hardware

<table><thead><tr><th width="211">Operating System</th><th>Memory</th><th>CPU</th><th>Disk</th><th>Bandwith </th></tr></thead><tbody><tr><td>Ubuntu 22.x</td><td>8 GB</td><td>4 core </td><td>120 GB</td><td>100 Mbps</td></tr></tbody></table>

#### Software

* ensure you have installed **Python3.10** or higher
* **NodeJS  v20.x or higher** with **pm2**

**Account**

* OPENAI API KEY **Paid Account**

## Install

#### Install Poetry

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

#### Clone Github De-Val directory

```bash
git clone https://github.com/deval-core/De-Val.git
cd De-Val
```

#### Create `.env` file

```bash
echo "OPENAI_API_KEY=<your_key_here>" > .env
```

#### Install all dependencies

```
poetry install
poetry shell
```

#### Create Wallet

after creating new coldkey and hotkey you can register your coldkey and hotkey to network

```bash
btcli wallet new_coldkey --wallet.name [wallet-name]
btcli wallet new_hotkey --wallet.name [wallet-name] --wallet.hotkey [wallet-hotkey]
```

send some fund to your coldkey. and register to network, it needed approximately **0.17 TAO**

```bash
btcli subnet register --subtensor.network finney --netuid 15 --wallet.name [wallet-name] --wallet.hotkey [wallet-hotkey]
```

#### Running Miner

```bash
pm2 start neurons/miners/openai_miner.py --name de-val-miner -- --netuid 15 --subtensor.network 15 --wallet.name [wallet-name] --wallet.hotkey [wallet-hotkey] --logging.debug --axon.port 8091
```

after that check your miner with **pm2 logs** also check on [taostats.io](https://taostats.io/subnets/15/metagraph)
