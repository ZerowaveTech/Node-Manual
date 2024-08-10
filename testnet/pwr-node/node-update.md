# Node Update

## Remove Validator, Config and Block

```bash
sudo rm -rf validator.jar config.json
```

## Install New Version

```bash
wget https://github.com/pwrlabs/PWR-Validator-Node/raw/main/validator.jar
wget https://github.com/pwrlabs/PWR-Validator-Node/raw/main/config.json
```

## Stop Old Validator

```bash
sudo pkill java
```

## Running The Node

```bash
sudo java -jar validator.jar password [IP-VPS] &
```
