# Installation

## Manual Setup Validator Node

For Install Manually Follow This Step

> Before run make sure you create wallet first and have 70k balance to became validator.

### Update Dependency

```
sudo apt update && sudo apt upgrade -y
```

### install Docker

> you can skip this if have docker in your machine

```
sudo apt-get update
sudo apt install jq
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - 
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo apt-get install docker-compose-plugin
sudo apt-get install docker-compose
```

### Auto Install Script

```
mkdir wormholes && cd wormholes
wget -O wormholes_install.sh https://docker.wormholes.com/wormholes_install.sh && sudo bash wormholes_install.sh
```

* Enter Private Key from Limino wallet, it should show consistent Private Key without 0x

## Usefull Command

### Monitor Node

```
screen -R wormholes
wget -0 CheckWorm.sh https://raw.githubusercontent.com/MNFaizi/nodeBlock_manual/main/Wormholes/CheckWorm.sh
chmod +x CheckWorm.sh
./CheckWorm.sh
```

### Check Account Balance

```
curl -X POST -H 'Content-Type:application/json' --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["Address","pending"],"id":1}' http://127.0.0.1:8545
```

`Address` - change with your own
