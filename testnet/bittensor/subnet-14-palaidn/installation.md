# Installation

## Requirement

#### Hardware

<table><thead><tr><th width="211">Operating System</th><th>Memory</th><th>CPU</th><th>Disk</th><th>Bandwith </th></tr></thead><tbody><tr><td>Ubuntu 22.x</td><td>8 GB</td><td>4 core </td><td>120 GB</td><td>100 Mbps</td></tr></tbody></table>

#### Software

* ensure you have installed **Python3.12** or higher
* **NodeJS  v20.x or higher** with **pm2**

#### Account

1. [Paypange](https://paypangea.com/) -> API KEY
2. [Alchemy](https://alchemy.com) -> API KEY

## Installation

#### Clone Palaidn Directory

```bash
git clone https://github.com/palaidn/palaidn_subnet.git
cd palaidn_subnet
```

#### Create Virtual Environment

```bash
python3 -m venv palaidn
source palaidn/bin/activate
```

#### Install all dependencies

```bash
python3 -m pip install -e .
```

#### Create ColdKey and Hotkey

```bash
btcli wallet new_coldkey --wallet.name [your-name]
btcli wallet new_hotkey --wallet.name [coldkey-name] --wallet.hotkey [hotkey-name]
```

{% hint style="danger" %}
**save output mnemonic and send some TAO to your coldkey.**&#x20;
{% endhint %}

#### Register to Palaidn subnet

{% hint style="warning" %}
ensure your have fund about 0.04 in your coldkey
{% endhint %}

```bash
btcli subnet register --netuid 14 --wallet.name [your-coldkey-name] --wallet.hotkey [hotkey-name]
```

#### Setup Config Miner

```
mkdir config
vi config/miner.json
```

press i in your keyboard

Paste config below

```json
{
    "networks": [
        {
            "name": "ethereum",
            "category": ["external", "erc20", "erc721", "erc1155"]
        },
        {
            "name": "polygon",
            "category": ["erc20", "erc721", "erc1155", "specialnft"]
        }
    ]
}
```

close vi with press **esc** and **:wq**

#### Running the miner script

```
bash ./scripts/start_miner.sh
```

Fill with :

* Your Alchemy API KEY
* PayPangea API KEY
* Network Finney
* Wallet Name
* Wallet Hotkey
* Axon Port Default 8091

ensure your miner has started and check logs with **pm2 logs** and check your miner UID in [taostat](https://taostats.io/subnets/14/metagraph)
