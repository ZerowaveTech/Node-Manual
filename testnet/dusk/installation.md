# Installation

## Manual Setup

For Install Manually Follow This Step

### Wallet Install

* Download CLI Wallet

```
wget https://github.com/dusk-network/wallet-cli/releases/download/v0.13.0/ruskwallet0.13.0-linux-x64-libssl3.tar.gz
tar -xvf tar -xf ruskwallet0.13.0-linux-x64-libssl3.tar.gz && mv ruskwallet0.13.0-linux-x64-libssl3 ruskwallet
cd ruskwallet
chmod +x rusk-wallet && ./rusk-wallet
```

* Create Wallet and Backup recovery phrase ![](https://lh5.googleusercontent.com/LtZ72tI1L\_RXl29lAjxZzWMpuaF5xRqwmxm8EKkM4uhKi5MvbTjE2CNszKOVqS3r9RyU4uGnkIgRpEIKWuBJC\_lwW9cpzkaEtwvG8uKag5cI0l-wevrZIABQqNkkaspP5XdcUKilDhB94UAFkcNdzRn0MFSdud2-MlhtLvJG49FD93jYSOnhLxaxWldRlw)

![](https://lh6.googleusercontent.com/zLBOd2yxH80CzL9-q-a\_ELaKv9tlEMexSumGG4CCX4mMsNDCgk1bOe4Ppp1H7uzyg5ThSk6k2bK98UaJE2oWpAP\_6ApO9uuRU7Y\_5oK8wctrBexckRk\_K871sFaqe75NFyHNHDRfBHt9heqzDffxtPME3DoLxopCdvSdxQAZ1wXr5Ffr1dzzHhL\_yr6VNw) - Select Address ![](https://lh6.googleusercontent.com/i-40brTLabk5nhxAThM\_Q5iXe4SimGfdPnOKDvHbH7gUV\_r4Zkn-i6Qm-O821eW80aRgWZhkUSTJwvgCnrC8KDf0oCrlHTMWvN4VYNRjJhdQp7PfwjG1j6kM6gbklom\_aSt3sHAsi3p5dcNntZVEFNHC05UXlMcy3Y3ojXrD8gmfZi\_fkXkVoVpL950EKw) - Export provisioner key-pair and fill password to protect the file ![](https://lh4.googleusercontent.com/b-HsbMRGnDWnAVh4-NodBi8-0evB5jC\_LhOLcQbsMrszWMqDKbZ03TD9lWGM651TzsxrZNFZ5yDBu5MAEdH5THulUM8cKAZ\_T4UebAUU6JAb\_fkXIxI\_9FYJkpnvkwuyqKe6ISZqR2Gd8esi0Rl6zFywt-ZAK3S1ZiCogKWEt8wNevK0Clikq-lp\_HcLTA) and show these two file \`.key & .cpk\` when export success, backup the file in save place ![](https://lh6.googleusercontent.com/dPBSfyqf8GrS1MSi2DykX0tlGl1OR4cJmN6UYU2xs327QacO4YzROpunm2Lbnhe52q2jQOsCvrY6fCpa1xB33DZuPBFmMHZ5l66pYSZWKBFvVf2Ud1icA\_wdbPxm9oXilvntXtassOoh2fZQLhP0sOxs5GxYnhWm-v8l4in-x-r5yhYMpknZSMt3Y-BLCQ)

[Fill the form to get Faucet](https://forms.gle/3h4wDbab9f6bZ68L8)

### Node Install

#### 1. Update Package

```
sudo apt update && sudo apt upgrade -y 
```

#### 2. Open Port

```
ufw allow 22
ufw allow 9000:9005/udp
ufw allow 8585
ufw enable
```

#### 3. Set Up a Node

```
curl --proto '=https' --tlsv1.2 -sSf https://dusk-infra.ams3.digitaloceanspaces.com/rusk/itn-installer.sh | sh
```

* copy file `.key` to `/opt/dusk/conf/`

```
cd $HOME/.dusk/rusk-wallet
cp *.key /opt/dusk/conf/consensus.keys
```

* set password

```
echo 'DUSK_CONSENSUS_KEYS_PASS=YourPassword' > /opt/dusk/services/dusk.conf
```

`YourPassword` - change with your own password when do export provisioner key

#### Start the Node

```
service rusk start
service dusk start
```

### Stake Token

* open wallet

```
cd $HOME/ruskwallet
./rusk-wallet --state http://127.0.0.1:8585
```

* access your wallet and fill password
* stake your token, `minimum stake is 1002 tDUSK` ![](https://lh6.googleusercontent.com/jDFCInEU9bdWyrQiltb98eYnCsz9Wlu2CDicUFBRpp1jKnsyaPY\_J04I6UJILQetwoZwzACEX9vw5AXqjUyrgNh-RhWnhW05PbVKannSbWITEt9FcADUdijBiNj\_LhyeWk658oFZj61kj9p5TAh05FwfE1Dp9Du5RtjlINyg1L67cV9zIQ9Qd5d9Zx53SA)

![](https://lh3.googleusercontent.com/rtMSw\_UzEEWeqsw8T6C5j9\_ljdRlrC5fFVW8SI24I6Tf5fRkWADGipUK12f9DJSPTgPx42o5nDg5KJu3d505CU9jpf4H5dnftEktAPYjW16vtE\_JmLfte5VEtE\_RCzM13NIH1Fzk7v101mFp-\_BJb7v3toANega9Rlejfw72Sb-ANBAXUlS0WiYn5oqV9g) - check transaction on explorer ![](https://lh5.googleusercontent.com/60c0e1iFW-sHDQSbtDSGKOuLH\_r4nNFGsLsZKAJCkkvG9qLtGyB632LjhC6nCHCOnwcWYT5vBvkW4KMy3slQZUoCxAl-BmfEvl7sCVeVwaqP9U7I5QBqNnUUzEiF\_i4NkP-HNcZsFEjiuEWi4wt18IP-PovxxCsbn17KuJ2gGtvQ-WuKFqGEcZKBMHj-YA)

