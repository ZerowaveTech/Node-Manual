<p align="center">
    <img  href="inery.io" height="100" height="auto" src="https://user-images.githubusercontent.com/56349947/206114692-7a225eb3-7640-4ccf-9b60-535c1219bd50.png">
</p>

<p align="center">Exorde is the web3 protocol that empowers developers to crawl and link all public data on the web.</p>

<p align='center'><a href="https://exorde.network/">Exorde Website</a></p>

<p align='center'>Exorde Social Media</p>
<div align="center">
    <a href="https://discord.gg/ExordeLabs" target="_blank"><img src="https://user-images.githubusercontent.com/50621007/176236430-53b0f4de-41ff-41f7-92a1-4233890a90c8.png" width="30"></a>
    <a href="http://t.me/exorde" target="_blank"><img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"></a>
    <a href="https://twitter.com/ExordeLabs" target="_blank"><img src="https://user-images.githubusercontent.com/56349947/205331052-6d4d4216-3529-490c-a1b9-8c3618aac8e2.png" width="30"></a>
</div>

# General Information

Incentive Test Information :
>[Incentive Info](https://discord.com/channels/754992505241469040/997571158109061253/1039546654996566056)

# Requirement
To run node you must have meet a requirement:
## Minimum Hardware Requirement
|   CPU  | Memory | Disk  | Bandwith |
|--------|--------|-------|----------|
| 2 Core |  4 GB  | 20 GB | 100 Mbps |
## Software Requirement
|       OS     |  Docker  |
|--------------|----------|
| Ubuntu 22.04 | 20.10.18 |

# Manual Setup
For install manually follow this step

## 1. Set Variabels
```
WALLET_ADDRESS=<Metamask-Wallet-Address>
```
`Metamask-Wallet-Address`- change with your metamas address
```
echo export EXORDE_WALLET=${WALLET_ADDRESS} >> $HOME/.bash_profile
source $HOME/.bash_profile
```
## 2. Update Package
```
cd $HOME
sudo apt update && sudo apt upgrade -y
```
## 3. Install Prerequisites Tools
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
## 4. Setup Docker Image
### 4.1 Clone repository
```
git clone https://github.com/exorde-labs/ExordeModuleCLI.git
```
### 4.2 Build Docker Image
```
cd ExordeModuleCLI
docker build -t exorde-cli .
```
## Run Node 
```
docker run -d --restart unless-stopped --pull always --name Exorde exordelabs/exorde-cli -m $EXORDE_WALLET -l 4
```
# Usefull Command
- Check node logs
```
docker logs -f Exorde
```
- Delete node
```
docker stop Exorde
docker rm Exorde
rm -rf ExordeModuleCLI
```