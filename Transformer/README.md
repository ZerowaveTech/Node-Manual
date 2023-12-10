<p align="center">
    <img height="100" height="auto" src="https://user-images.githubusercontent.com/56349947/204070407-2f8b5904-f15d-4c5a-93fc-fed42906cd82.png">
</p>
<p align="center">The Transformers achieved performance breakthroughs on a highly decentralized basis, with the web always open and nodes free to operate.</p>

# Requirement
To run node on this chain you must have meet a requirement :
## Minimum Hardware Requirement
- CPU       : 8 Core
- Memory    : 16 GB
- Disk      : 500 GB
- Bandwith  : 10 Mbps 

## Software Requirement
- OS    : Ubuntu 22.04 Desktop

# Manual Node Setup

for install manually follow this step by step

Official Documentation :
> [Run TFSC Node](https://tfsc.io/doc/learn/run-rpc-node)

Chain Explorer :
> https://explorer.tfsc.io/

## 1. Update 
```
sudo apt update && sudo apt upgrade -y 
```

## 2. Open Port
To interact with other must open this port 

```
ufw allow 22
ufw allow 41516
ufw allow 41517
ufw allow 41506
ufw enable
```
## 3. Download Program
check the lastest version in here <a target="_blank">https://tfsc.io/doc/learn/tfsc-update</a>
```
mkdir tfsc &&  cd tfsc
wget <link_program>
chmod +x <program_name>
./<program_name>
```
it will generate 3 file: data.db, config.json, cert 
> please backup cert folder in save place because it contain private key address
### 3.1 Edit file config.json
```
nano config.json
```
you will see like this and edit with your own validator name and your ip address 
<img src="https://user-images.githubusercontent.com/56349947/204071826-647c5629-cb4a-4cb3-a824-e30f01c7ec50.jpg">

## 4. Run the Program
```
screen -R tfsc
./<program_name> -m
``` 
> to minimize the screen `CTRL + A + D` if you want to enter the screen again use this command `screen -r tfsc`

Wait for faucet is landing and you can stake in your own address and invest in other address
### Program prompt box
<img src="https://user-images.githubusercontent.com/56349947/204071953-6daa04e9-a6c9-4cbb-b76a-c6c08557ef3a.png">

#### Function Menu
| Number |       Menu       |           Function              |
|--------|------------------|---------------------------------|
|    1   | Transaction      | Transfer Token to Other Address |
|    2   | Stake            | Stake Token                     |
|    3   | Unstake          | Unstake your stake token        |
|    4   | Invest           | Invest to choosen validator     |
|    5   | Disinvest        | Withdraw invested token         |
|    6   | Bonus            | Claim bonus daily when run node |
|    7   | PrintAccountInfo | Show Account information        |
|    0   | Exit             | Close the program               |
