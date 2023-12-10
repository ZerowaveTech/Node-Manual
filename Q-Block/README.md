<p align="center">
    <img height="100" height="auto" src="https://user-images.githubusercontent.com/56349947/206959347-39000801-f2e7-464e-9d60-2a9e25df1306.png">
</p>
<h1 align='center'>Q Blockchain</h1>
<p align='center'>Q is a novel blockchain that combines the benefits of a public, open and decentralized ledger with the transparency and predictability of enforceable private contracts, thereby enabling adoption by a great variety of use cases that desire decentralization but require scalability and dependability.</p>
<p align='center'>
    <a href="https://q.org">Q Blockchain Website</a>
</p>
<p align="center">Q Blockchain Social Media</p>
<div align="center">
    <a href="https://discord.gg/YTgkvJvZGD" target="_blank"><img src="https://user-images.githubusercontent.com/50621007/176236430-53b0f4de-41ff-41f7-92a1-4233890a90c8.png" width="30"></a>
    <a href="https://twitter.com/QBlockchain" target="_blank"><img src="https://user-images.githubusercontent.com/56349947/205331052-6d4d4216-3529-490c-a1b9-8c3618aac8e2.png" width="30"></a>
</div>

# General Information

- Incentive Information :
>[Incentive Info](https://medium.com/q-blockchain/q-blockchain-validator-onboarding-program-part-1-validator-incentivized-testnet-567ef6e4002e)

- Official Guide :
>[Guide](https://docs.qtestnet.org/)

- Validator Status :
>[Validator](https://stats.qtestnet.org/)

- Register incentive Testnet :
>[Register](https://itn.qdev.li/)

# Requirement
To run node you must have meet a requirement:
> base on my machine
## Minimum Hardware Requirement
|   CPU  | Memory  |  Disk  | Bandwith |
|--------|---------|--------|----------|
| 8 Core |  32 GB  | 500 GB | 100 Mbps |
## Software Requirement
- OS    : Ubuntu 20.xx

# Manual Setup Validator Node
For Install Manually Follow This Step

## Update Dependency
```
sudo apt update && sudo apt upgrade -y
```
## install Docker
>you can skip this if have docker in your machine
```
sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin
sudo apt-get install docker-compose
```
## Clone the Repository
```
git clone https://gitlab.com/q-dev/testnet-public-tools
```
move to testnet-validator directory
```
cd testnet-public-tools/testnet-validator
```
## Generate Keypair for Validator
- Set vars password
```
QPASSWORD=YourPassword
```
`YourPassword` - change with your password
- export vars to .bash_profile
```
echo "export QPASSWORD=$QPASSWORD" >> $HOME/.bash_profile
source $HOME/.bash_profile
```
- create keystore directory and pwd.txt file
```
mkdir keystore
cd keystore
echo "QPASSWORD" >> pwd.txt
```
- generate new wallet
```
cd ..
docker-compose run --rm --entrypoint "geth account new --datadir=/data --password=/data/keystore/pwd.txt" testnet-validator-node
```
>after that you will see output command that your new key was generated like this
```
Your new key was generated

Public address of the key:   0xb3FF24F818b0ff6Cc50de951bcB8f86b52287dac
Path of the secret key file: /data/keystore/UTC--2021-01-18T11-36-28.705754426Z--b3ff24f818b0ff6cc50de951bcb8f86b52287dac

- You can share your public address with anyone. Others need it to interact with you.
- You must NEVER share the secret key with anyone! The key controls access to your funds!
- You must BACKUP your key file! Without the key, it's impossible to access account funds!
- You must REMEMBER your password! Without the password, it's impossible to decrypt the key!
```
## Get Faucet
 <p align="center">
    <a target="_blank" href="https://faucet.qtestnet.org/">Claim Faucet</a>
 <p>

## Configure Setup
### Edit .env file
```
cp .env.example .env
nano .env
```
>Output like this
```
# docker image for q client
QCLIENT_IMAGE=qblockchain/q-client:1.2.1

# your q address here (without leading 0x)
ADDRESS=b3FF24F818b0ff6Cc50de951bcB8f86b52287DAc

# your public IP address here
IP=193.19.228.94

# the port you want to use for p2p communication (default is 30313)
EXT_PORT=30313

# extra bootnode you want to use
BOOTNODE1_ADDR=enode://c610793186e4f719c1ace0983459c6ec7984d676e4a323681a1cbc8a67f506d1eccc4e164e53c2929019ed0e5cfc1bc800662d6fb47c36e978ab94c417031ac8@79.125.97.227:30304
BOOTNODE2_ADDR=enode://8eff01a7e5a66c5630cbd22149e069bbf8a8a22370cef61b232179e21ba8c7b74d40e8ee5aa62c54d145f7fc671b851e5ccbfe124fce75944cf1b06e29c55c80@79.125.97.227:30305
BOOTNODE3_ADDR=enode://7a8ade64b79961a7752daedc4104ca4b79f1a67a10ea5c9721e7115d820dbe7599fe9e03c9c315081ccf6a2afb0b6652ee4965e38f066fe5bf129abd6d26df58@79.125.97.227:30306
```
- change docker image from 1.2.1 to 1.2.2 on this line like this
```
# docker image for q client
QCLIENT_IMAGE=qblockchain/q-client:1.2.1
```
- put your public address on this line without 0x like this
```
# your q address here (without leading 0x)
ADDRESS=b3FF24F818b0ff6Cc50de951bcB8f86b52287DAc
```
after edit out from nano and save `ctrl + x` `y` and `enter`
### Edit config.json file
```
nano config.json
```
>output like this
```
    {
      "address": "b3FF24F818b0ff6Cc50de951bcB8f86b52287DAc",
      "password": "supersecurepassword",
      "keystoreDirectory": "/data",
      "rpc": "https://rpc.qtestnet.org"
    }
```
- change address without 0x in address line
- change password with your password on password line
## Put Validator to Stake
```
docker run --rm -v $PWD:/data -v $PWD/config.json:/build/config.json qblockchain/js-interface:testnet validators.js
```
## Register to Website
<p align="center">
    <a target="_blank" href="https://itn.qdev.li/">Register Here</a>
</p>

>fill out the form, after successfull you should receive your own validator name like `--ethstats=ITN-testvalidatorname:qstats-testnet@stats.qtestnet.org` or just `ITN-YourValidatorName`

### Configure Docker
```
nano docker-compose.yaml
```
>output like this
```
testnet-validator-node:
  image: $QCLIENT_IMAGE
  entrypoint: ["geth", "--ethstats=<Your_Validator_Name>:<Testnet_access_key>@stats.qtestnet.org", "--datadir=/data", ...]
```
- then change `--ethstats` with your own from register website

## Run Application
```
docker-compose up -d
```

# Usefull Command
- check logs:
```
docker-compose logs -f
```
- stop application
```
docker-compose down
```
- export private key
[Export](./Export_PrivKey.md)
