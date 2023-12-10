<p align="center">
    <img height="100" height="auto" src="https://user-images.githubusercontent.com/56349947/206959347-39000801-f2e7-464e-9d60-2a9e25df1306.png">
</p>
<h1 align='center'>Guide to Export Private Key</h1>

# Install Package
```
cd $HOME/testnet-public-tools/js-tools
npm install
```
# Extract Private Key
```
node extract-geth-private-key WalletAddress ../testnet-validator/ $QPASSWORD
```
`WalletAddress` - change wallet address with your address

> if success import private key to metamask