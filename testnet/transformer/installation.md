# Installation

## Manual Node Setup

for install manually follow this step by step

Official Documentation :

> [Run TFSC Node](https://tfsc.io/doc/learn/run-rpc-node)

Chain Explorer :

> https://explorer.tfsc.io/

### 1. Update

```
sudo apt update && sudo apt upgrade -y 
```

### 2. Open Port

To interact with other must open this port

```
ufw allow 22
ufw allow 41516
ufw allow 41517
ufw allow 41506
ufw enable
```

### 3. Download Program

check the lastest version in here https://tfsc.io/doc/learn/tfsc-update

```
mkdir tfsc &&  cd tfsc
wget <link_program>
chmod +x <program_name>
./<program_name>
```

it will generate 3 file: data.db, config.json, cert

> please backup cert folder in save place because it contain private key address

#### 3.1 Edit file config.json

```
nano config.json
```

you will see like this and edit with your own validator name and your ip address ![](https://user-images.githubusercontent.com/56349947/204071826-647c5629-cb4a-4cb3-a824-e30f01c7ec50.jpg)

### 4. Run the Program

```
screen -R tfsc
./<program_name> -m
```

> to minimize the screen `CTRL + A + D` if you want to enter the screen again use this command `screen -r tfsc`

Wait for faucet is landing and you can stake in your own address and invest in other address

#### Program prompt box

![](https://user-images.githubusercontent.com/56349947/204071953-6daa04e9-a6c9-4cbb-b76a-c6c08557ef3a.png)

**Function Menu**

<table><thead><tr><th>Number</th><th width="227.33333333333331">Menu</th><th>Function</th></tr></thead><tbody><tr><td>1</td><td>Transaction</td><td>Transfer Token to Other Address</td></tr><tr><td>2</td><td>Stake</td><td>Stake Token</td></tr><tr><td>3</td><td>Unstake</td><td>Unstake your stake token</td></tr><tr><td>4</td><td>Invest</td><td>Invest to choosen validator</td></tr><tr><td>5</td><td>Disinvest</td><td>Withdraw invested token</td></tr><tr><td>6</td><td>Bonus</td><td>Claim bonus daily when run node</td></tr><tr><td>7</td><td>PrintAccountInfo</td><td>Show Account information</td></tr><tr><td>0</td><td>Exit</td><td>Close the program</td></tr></tbody></table>
