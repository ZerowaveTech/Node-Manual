<p align="center">
    <img  href="inery.io" height="50" height="auto" src="https://user-images.githubusercontent.com/38981255/184088981-3f7376ae-7039-4915-98f5-16c3637ccea3.PNG"">
</p>

<h1 align="center">TASK 2</h1>
<h2 align="center">Make own currency and transfer to someone</h2>

## Before Start Unlock Wallet First
```
cline wallet unlock -n <WALLET_NAME>
```

> if you follow my tutorial from task 1 `Wallet_Name` = `Username`

## Get Token abi and wasm File
```
cline get code inery.token -c token.wasm -a token.abi --wasm
```

## Set wasm Code to Account
```
cline set code -j <YOUR_USERNAME> token.wasm
```

## Set abi Code
```
cline set abi <YOUR_USERNAME> token.abi
```

## Create Token
```
cline push action inery.token create '["<YOUR_USERNAME>", "100000.0000 <YOUR_TOKENNAME>" , "creating my first tokens"]' -p <YOUR_USERNAME>
```

## Issues New Token
```
cline push action inery.token issue '["<YOUR_USERNAME>", "10000.0000 <YOUR_TOKENNAME>", "Issuing some <YOUR_TOKENNAME> token"]' -p <YOUR_USERNAME>
```

NOTE : TO COMPLETE ON TASK 2 YOU MUST TRANSFER YOUR TOKEN TO 10 DIFFERENT ACCOUNT, YOU CAN CHECK ACCOUNT NAME <a href="https://explorer.inery.io/" target="_blank">HERE</a>

## Transfer Token 
```
cline push action inery.token transfer '["<YOUR_USERNAME>", "<RECEIVER>", "1.0000 <YOUR_TOKENNAME>", "Here Is 1 <YOUR_TOKENNAME> for you bro "]' -p <YOUR_USERNAME>
```

> Repeat that until you done transfer your token to 10 different account included inery account
