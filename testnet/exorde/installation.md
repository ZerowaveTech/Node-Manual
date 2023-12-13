# Installation

## Manual Setup

For install manually follow this step

### 1. Set Variabels

```
WALLET_ADDRESS=<Metamask-Wallet-Address>
```

`Metamask-Wallet-Address`- change with your metamas address

```
echo export EXORDE_WALLET=${WALLET_ADDRESS} >> $HOME/.bash_profile
source $HOME/.bash_profile
```

### 2. Update Package

```
cd $HOME
sudo apt update && sudo apt upgrade -y
```

### 3. Install Prerequisites Tools

```
sudo apt install curl build-essential git wget npm jq make gcc tmux -y && apt purge docker docker-engine docker.io containerd docker-compose -y
```

```
rm /usr/bin/docker-compose /usr/local/bin/docker-compose
curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh
systemctl restart docker
curl -SL https://github.com/docker/compose/releases/download/v2.5.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker --version
```

### 4. Setup Docker Image

#### 4.1 Clone repository

```
git clone https://github.com/exorde-labs/ExordeModuleCLI.git
```

#### 4.2 Build Docker Image

```
cd ExordeModuleCLI
docker build -t exorde-cli .
```

### Run Node

```
docker run -d --restart unless-stopped --pull always --name Exorde exordelabs/exorde-cli -m $EXORDE_WALLET -l 4
```
