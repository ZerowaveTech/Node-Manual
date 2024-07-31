---
description: Node Sonaric installation guide
---

# Installation

## Website

* [Leaderboard](https://tracker.sonaric.xyz/)

## Install

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/monk-io/sonaric-install/main/linux-install-sonaric.sh)"
```

> if installation succes it will start <mark style="color:green;">`sonaricd`</mark> automatically

### Check Node

```bash
sonaric node-info
```

it should return like this

```bash
 ✨ Node information loaded:
 ├─🧊 ID             12D3XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
 ├─📥 Leader         wavy-cream-yacht
 ├─🧊 Version        v1.1.0
 ...
```

### Change node name

after node successfully running, you can change your node name with this command:

```bash
sonaric node-rename -n your-node-name
```

> change `your-node-name` with your preferable name

## Backup Node

{% hint style="warning" %}
for better security and avoiding any lose, please backup your node
{% endhint %}

```bash
sonaric identity-export -o your-node-name.identity
```

> change `your-node-name` with preferable name

## Access GUI

{% code overflow="wrap" %}
```bash
ssh -L 127.0.0.1:44003:127.0.0.1:44003 -L 127.0.0.1:44004:127.0.0.1:44004 -L 127.0.0.1:44005:127.0.0.1:44005 -L 127.0.0.1:44006:127.0.0.1:44006 user@your-vps-ip
```
{% endcode %}

{% hint style="danger" %}
RUN THIS COMMAND ON YOUR LOCAL MACHINE AND ACCESS [http://localhost:44004](http://localhost:44004)

change `user@your-vps-ip` with your own
{% endhint %}
