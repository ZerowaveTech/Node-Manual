# Installation

## Manual Setup

For install manually follow this step

### 1. Choose installation method

<table><thead><tr><th width="364">Install Method</th><th>Manual</th></tr></thead><tbody><tr><td>Docker</td><td><a href="dockerinstall.md">click here</a></td></tr><tr><td>Source Code</td><td><a href="sourceinstall.md">Click here</a></td></tr></tbody></table>

### 2. Send Address to Rover\_Bot for join waitlist

> [Rover Bot](https://t.me/thepowerio\_bot)

`start bot` - and follow step by step until you get into waitlist

> Format send to rover bot `http://YourDomain:YourPortNumber/api/node/status`

Wait until receive personal token to join tea Ceremony

### 3. Join Tea Ceremony

Before start Tea Ceremony must open port `1800`,`1443`,`1080` and install latest version of erlang

```
ufw allow 22
ufw allow 1800
ufw allow 1443
ufw allow 1080
ufw allow 80
ufw enable
```

Download Tea Client

```
cd $HOME
mkdir teaclient && cd teaclient
wget https://tea.thepower.io/teaclient
chmod +x teaclient
./teaclient -n <nickname> <chain token>.<personal token>
```

* 'nickname' change with your nickname
* 'chain token' get from dev it will publish in announcement channel[Telegram Announcement](https://t.me/thepowerio\))
* 'personal token' get from rover bot [Rover Bot](https://t.me/thepowerio\_bot\))

It wil generate 2 file `node.config and genesis.txt` in your folder when you run tea client

> if you got the file continue to next step

### 4. Setup SSL Certificate

```
sudo -i
apt-get install socat
curl https://get.acme.sh | sh -s email=youractiveemail
```

`youractiveemail` - fill with your email

* close terminal
* login again to your vps
* install SSL

```
source $HOME/.bashrc
acme.sh --server letsencrypt --issue --standalone  -d your_node.example.com
acme.sh --install-cert -d your_node.example.com \
--cert-file /opt/thepower/db/cert/your_node.example.com.crt \
--key-file /opt/thepower/db/cert/your_node.example.com.key \
--ca-file /opt/thepower/db/cert/your_node.example.com.crt.ca.crt
acme.sh --info -d your_node.example.com
```

`your_node.example.com` - change with hostname you get from file `node.config`

### 5. Run Node

#### 5.1 Docker Run

Make directory and move file `node.config & genesis.txt` to working directory

```
cd /opt/thepower
mkdir {db,log}
cp $HOME/teaclient/node.config /opt/thepower/node.config
cp $HOME/teaclient/genesis.txt /opt/thepower/genesis.txt
```

Start Docker

```
docker run -d \
--name tpnode \
--restart unless-stopped \
--mount type=bind,source="$(pwd)"/db,target=/opt/thepower/db \
--mount type=bind,source="$(pwd)"/log,target=/opt/thepower/log \
--mount type=bind,source="$(pwd)"/node.config,target=/opt/thepower/node.config \
--mount type=bind,source="$(pwd)"/genesis.txt,target=/opt/thepower/genesis.txt \
-p port:port \
-p 1080:1080 \
-p 1443:1443 \
thepowerio/tpnode
```

`port` must change with port in use in your chain it store in file `node.config` in the end every ip address other node

`your_node.example.com` - change with your hostname

#### 5.2 Source Code Run

Make directory and move file `node.config & genesis.txt` to working directory

```
cd /opt/thepower
mkdir {db,log}
cp $HOME/teaclient/node.config /opt/thepower/node.config
cp $HOME/teaclient/genesis.txt /opt/thepower/genesis.txt
```

Make Service

```
sudo tee /etc/systemd/system/tpnode.service > /dev/null <<EOF
[Unit]
Description=tpnode service
Requires=network.target
After=network.target

[Service]
Type=forking
ExecStart=/opt/thepower/bin/thepower start
ExecStop=/opt/thepower/bin/thepower stop
User=root
Group=root
Restart=on-failure

[Install]
WantedBy=multi-user.target
EOF
```

Start Node

```
systemctl daemon-reload
systemctl enable tpnode
systemctl start tpnode
```

After node successfull launch, send your hostname to Rover Bot

## Usefull Command

*
