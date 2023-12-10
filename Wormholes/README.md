<p align="center">
    <img height="100" height="auto" src="https://user-images.githubusercontent.com/56349947/207211955-0ad7f3d4-13c5-4ed3-8907-0f770077cf76.png">
</p>
<h1 align='center'>WormholesChain</h1>
<p align='center'>WormholesChain solves the blockchain trilemma, which entails a necessary tradeoff between scalability, security, and decentralization, by building the technology to achieve the ideal balance between these three metrics, creating a highly scalable and secure blockchain system that doesn't sacrifice decentralization.</p>
<p align='center'>
    <a href="https://www.wormholes.com/">WormholesChain Website</a>
</p>
<p align="center">WormholesChain Social Media</p>
<div align="center">
    <a href="https://discord.com/invite/N4ksH6tqRX" target="_blank"><img src="https://user-images.githubusercontent.com/50621007/176236430-53b0f4de-41ff-41f7-92a1-4233890a90c8.png" width="30"></a>
    <a href="https://twitter.com/WormholesChain" target="_blank"><img src="https://user-images.githubusercontent.com/56349947/205331052-6d4d4216-3529-490c-a1b9-8c3618aac8e2.png" width="30"></a>
    <a href="https://t.me/wormholes_chain" target="_blank"><img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"></a>
</div>

# General Information

- Official Guide 
>[Guide](https://www.wormholes.com/docs/install/run/index.html)

- Explorer 
>[Explorer](https://www.wormholesscan.com/#/)

- Wallet 
>[Wallet](https://www.limino.com/)

# Requirement
To run node you must have meet a requirement:

## Minimum Hardware Requirement
|   CPU  | Memory |  Disk  | Bandwith |
|--------|--------|--------|----------|
| 4 Core |  8 GB  | 500 GB | 100 Mbps |

## Software Requirement
- OS    : Ubuntu 20.xx

# Manual Setup Validator Node
For Install Manually Follow This Step

>Before run make sure you create wallet first and have 70k balance to became validator.

## Update Dependency
```
sudo apt update && sudo apt upgrade -y
```
## install Docker
>you can skip this if have docker in your machine
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
## Auto Install Script
```
mkdir wormholes && cd wormholes
wget -O wormholes_install.sh https://docker.wormholes.com/wormholes_install.sh && sudo bash wormholes_install.sh
```
- Enter Private Key from Limino wallet, it should show consistent Private Key without 0x

# Usefull Command
## Monitor Node 
```
screen -R wormholes
wget -0 CheckWorm.sh https://raw.githubusercontent.com/MNFaizi/nodeBlock_manual/main/Wormholes/CheckWorm.sh
chmod +x CheckWorm.sh
./CheckWorm.sh
```
## Check Account Balance
```
curl -X POST -H 'Content-Type:application/json' --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["Address","pending"],"id":1}' http://127.0.0.1:8545
```
`Address` - change with your own