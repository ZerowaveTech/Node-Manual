# Installation

## Install Java

```bash
apt install openjdk-19-jre-headless
```

## Install Validator Node and Config

```bash
wget https://github.com/pwrlabs/PWR-Validator-Node/raw/main/validator.jar
wget https://github.com/pwrlabs/PWR-Validator-Node/raw/main/config.json
```

## Set Up Password

```bash
sudo nano password
```

{% hint style="info" %}
* set the password
* exit with `ctrl + x`
* press `y` to confirm
{% endhint %}

## Run Node

```bash
sudo java -jar validator.jar password [IP-VPS] --compression-level 0 &
```

{% hint style="info" %}
it will running in the background
{% endhint %}

> Apply become validator in PWR [discord](https://discord.gg/552K2wC4) channel

## Getting the private keys

```bash
sudo java -jar validator.jar get-private-key password
```

{% hint style="warning" %}
SAVE THE OUTPUT KEY AND IMPORT TO PWR WALLET
{% endhint %}
