# Installation

## Running Light Node With One Command

running with this simple command

> Before running the command, i recommend to use screen

```bash
curl -sL1 https://nubit.sh | bash
```

{% hint style="info" %}
This code will automatically upgrade to the last version
{% endhint %}

#### after got logs _**BACKUP PUBLIC\_KEY, AUTH\_KEY**_ from logs and also _**import mnemonic to wallet**_

close log with _**ctrl+c**_

#### Back up mnemonic

```bash
cat ~/nubit-node/mnemonic.txt
```

{% hint style="info" %}
after wallet imported to _**keplr wallet**_ don't forget to claim faucet in [here](https://faucet.nubit.org/)
{% endhint %}

## Running With Screen

#### Create Screen

```bash
screen -R nubit-node
```

> you can change _**nubit-node**_ with other name

#### Exit Screen

```
CTRL + A + D
```

