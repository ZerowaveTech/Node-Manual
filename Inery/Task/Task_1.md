<p align="center">
    <img  href="inery.io" height="50" height="auto" src="https://user-images.githubusercontent.com/38981255/184088981-3f7376ae-7039-4915-98f5-16c3637ccea3.PNG"">
</p>

<h1 align="center">TASK 1</h1>
<h2 align="center">Running Master Node</h2>


## Update 
```
sudo apt update && sudo apt upgrade -y
```

## Install Prerequisites Tools
```
sudo apt-get install -y make bzip2 automake libbz2-dev libssl-dev doxygen graphviz libgmp3-dev \
autotools-dev libicu-dev python2.7 python2.7-dev python3 python3-dev \
autoconf libtool curl zlib1g-dev sudo ruby libusb-1.0-0-dev \
libcurl4-gnutls-dev pkg-config patch llvm-7-dev clang-7 vim-common jq libncurses5
```

## Clone Inery Github
```
git clone https://github.com/inery-blockchain/inery-node
```

## Update Permission File
```
cd inery-node/inery.setup && chmod +x ine.py
./ine.py --export
cd; source .bashrc; cd -
```

## Setting File config.json
```
cd tools
nano config.json
```
> for azure user use commmand `hostname -i` and change `PEER_ADDRESS` with that 
<div align="center">
    <img src="https://user-images.githubusercontent.com/103183907/193441655-6f3ee6b7-8133-4d84-a846-67311cd5d706.png">
</div>

## Synchronize Node
```
cd ..
screen -R inery
./ine.py --master && cd master.node/blockchain && tail -f nodine.log
```
> after log its running close screen with `CTRL + A + D` and it will take time 2-3 hours depend on block high the chain

After node is synchronize, continue to next step

## Synchronize Wallet in Dashboard
```
cline wallet create -n <USERNAME> -f file.txt
cline wallet import --private-key <PRIVATE_KEY>-n <USERNAME>
cline system regproducer <USERNAME> <PUBLIC_KEY> 0.0.0.0:9010
cline system makeprod approve <USERNAME> <USERNAME>
```

`<USERNAME>`    = fill with your username
`<PRIVATE_KEY>` = fill with your private key
`<PUBLIC_KEY>`  = fill with your public key

#### Check Username on Explorer

if username show in here task 1 is done

<img src="https://user-images.githubusercontent.com/103183907/193442131-35fda1c6-181f-4aa6-9827-749abc304966.png">