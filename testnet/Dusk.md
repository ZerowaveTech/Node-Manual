<p align="center">
    <img height="100" height="auto" src="https://user-images.githubusercontent.com/56349947/205318364-965663f3-f9e4-4010-9e82-d4f5d29e9f4e.svg">
</p>
<h1 align='center'>Dusk Network</h1>
<p align='center'>Dusk Network is technology for securities. An open source and secure blockchain (DLT) infrastructure that businesses use to tokenize financial instruments and automate costly processes</p>
<p align='center'>
    <a href="https://dusk.network/">About Dusk Network</a>
</p>
<div align="center">
    <a href="https://discord.com/invite/dusknetwork" target="_blank"><img src="https://user-images.githubusercontent.com/50621007/176236430-53b0f4de-41ff-41f7-92a1-4233890a90c8.png" width="30"></a>
    <a href="https://t.me/DuskNetwork" target="_blank"><img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30" margin="5px"></a>
    <a href="https://twitter.com/duskfoundation" target="_blank"><img src="https://user-images.githubusercontent.com/56349947/205331052-6d4d4216-3529-490c-a1b9-8c3618aac8e2.png" width="30"></a>
</div>

# General Information

Tesnet Infomation :
> [Announcement](https://dusk.network/news/dusk-network-to-launch-rolling-incentivized-testnet-activities)

Official Guide Installation :
> [Guide](https://dusk.network/pages/incentivized-testnet)

Network Explorer :
>[Explorer](https://explorer.dusk.network/)

# Requirement
To run node you must have meet a requirement:
## Minimum Hardware Requirement
|   CPU  | Memory | Disk  | Bandwith |
|--------|--------|-------|----------|
| 1 Core |  1 GB  | 25 GB | 100 Mbps |
## Software Requirement
- OS    : Ubuntu 22.04

# Manual Setup
For Install Manually Follow This Step

## Wallet Install
- Download CLI Wallet
```
wget https://github.com/dusk-network/wallet-cli/releases/download/v0.13.0/ruskwallet0.13.0-linux-x64-libssl3.tar.gz
tar -xvf tar -xf ruskwallet0.13.0-linux-x64-libssl3.tar.gz && mv ruskwallet0.13.0-linux-x64-libssl3 ruskwallet
cd ruskwallet
chmod +x rusk-wallet && ./rusk-wallet
```
- Create Wallet and Backup recovery phrase
<img src="https://lh5.googleusercontent.com/LtZ72tI1L_RXl29lAjxZzWMpuaF5xRqwmxm8EKkM4uhKi5MvbTjE2CNszKOVqS3r9RyU4uGnkIgRpEIKWuBJC_lwW9cpzkaEtwvG8uKag5cI0l-wevrZIABQqNkkaspP5XdcUKilDhB94UAFkcNdzRn0MFSdud2-MlhtLvJG49FD93jYSOnhLxaxWldRlw">
<img src="https://lh6.googleusercontent.com/zLBOd2yxH80CzL9-q-a_ELaKv9tlEMexSumGG4CCX4mMsNDCgk1bOe4Ppp1H7uzyg5ThSk6k2bK98UaJE2oWpAP_6ApO9uuRU7Y_5oK8wctrBexckRk_K871sFaqe75NFyHNHDRfBHt9heqzDffxtPME3DoLxopCdvSdxQAZ1wXr5Ffr1dzzHhL_yr6VNw">
- Select Address
<img src="https://lh6.googleusercontent.com/i-40brTLabk5nhxAThM_Q5iXe4SimGfdPnOKDvHbH7gUV_r4Zkn-i6Qm-O821eW80aRgWZhkUSTJwvgCnrC8KDf0oCrlHTMWvN4VYNRjJhdQp7PfwjG1j6kM6gbklom_aSt3sHAsi3p5dcNntZVEFNHC05UXlMcy3Y3ojXrD8gmfZi_fkXkVoVpL950EKw">
- Export provisioner key-pair and fill password to protect the file
<img src="https://lh4.googleusercontent.com/b-HsbMRGnDWnAVh4-NodBi8-0evB5jC_LhOLcQbsMrszWMqDKbZ03TD9lWGM651TzsxrZNFZ5yDBu5MAEdH5THulUM8cKAZ_T4UebAUU6JAb_fkXIxI_9FYJkpnvkwuyqKe6ISZqR2Gd8esi0Rl6zFywt-ZAK3S1ZiCogKWEt8wNevK0Clikq-lp_HcLTA">
and show these two file `.key & .cpk` when export success, backup the file in save place
<img src="https://lh6.googleusercontent.com/dPBSfyqf8GrS1MSi2DykX0tlGl1OR4cJmN6UYU2xs327QacO4YzROpunm2Lbnhe52q2jQOsCvrY6fCpa1xB33DZuPBFmMHZ5l66pYSZWKBFvVf2Ud1icA_wdbPxm9oXilvntXtassOoh2fZQLhP0sOxs5GxYnhWm-v8l4in-x-r5yhYMpknZSMt3Y-BLCQ">

<p align="center">
    <a href="https://forms.gle/3h4wDbab9f6bZ68L8" target="_blank">Fill the form to get Faucet</a>
</p>

## Node Install
### 1. Update Package
```
sudo apt update && sudo apt upgrade -y 
```
### 2. Open Port
```
ufw allow 22
ufw allow 9000:9005/udp
ufw allow 8585
ufw enable
```
### 3. Set Up a Node
```
curl --proto '=https' --tlsv1.2 -sSf https://dusk-infra.ams3.digitaloceanspaces.com/rusk/itn-installer.sh | sh
```
- copy file `.key` to `/opt/dusk/conf/`
```
cd $HOME/.dusk/rusk-wallet
cp *.key /opt/dusk/conf/consensus.keys
```
- set password
```
echo 'DUSK_CONSENSUS_KEYS_PASS=YourPassword' > /opt/dusk/services/dusk.conf
```
`YourPassword` - change with your own password when do export provisioner key

### Start the Node
```
service rusk start
service dusk start
```
## Stake Token
- open wallet
```
cd $HOME/ruskwallet
./rusk-wallet --state http://127.0.0.1:8585
```
- access your wallet and fill password
- stake your token, `minimum stake is 1002 tDUSK`
<img src="https://lh6.googleusercontent.com/jDFCInEU9bdWyrQiltb98eYnCsz9Wlu2CDicUFBRpp1jKnsyaPY_J04I6UJILQetwoZwzACEX9vw5AXqjUyrgNh-RhWnhW05PbVKannSbWITEt9FcADUdijBiNj_LhyeWk658oFZj61kj9p5TAh05FwfE1Dp9Du5RtjlINyg1L67cV9zIQ9Qd5d9Zx53SA">
<img src="https://lh3.googleusercontent.com/rtMSw_UzEEWeqsw8T6C5j9_ljdRlrC5fFVW8SI24I6Tf5fRkWADGipUK12f9DJSPTgPx42o5nDg5KJu3d505CU9jpf4H5dnftEktAPYjW16vtE_JmLfte5VEtE_RCzM13NIH1Fzk7v101mFp-_BJb7v3toANega9Rlejfw72Sb-ANBAXUlS0WiYn5oqV9g">
- check transaction on explorer
<img src="https://lh5.googleusercontent.com/60c0e1iFW-sHDQSbtDSGKOuLH_r4nNFGsLsZKAJCkkvG9qLtGyB632LjhC6nCHCOnwcWYT5vBvkW4KMy3slQZUoCxAl-BmfEvl7sCVeVwaqP9U7I5QBqNnUUzEiF_i4NkP-HNcZsFEjiuEWi4wt18IP-PovxxCsbn17KuJ2gGtvQ-WuKFqGEcZKBMHj-YA">

# Usefull Command
#### Check Progress Sync
```
tail -100 /var/log/dusk.log | grep 'Accepted'
```