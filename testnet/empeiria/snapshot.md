---
description: thanks to indonde for snapshot
---

# Snapshot

```bash
sudo apt update
sudo apt-get install snapd lz4 -y

# Stop the service and reset the data
sudo systemctl stop emped
cp $HOME/.empe-chain/data/priv_validator_state.json $HOME/.empe-chain/priv_validator_state.json.backup
rm -rf $HOME/.empe-chain/data

# Stop the service and reset the data
sudo systemctl stop emped
cp $HOME/.empe-chain/data/priv_validator_state.json $HOME/.empe-chain/priv_validator_state.json.backup
rm -rf $HOME/.empe-chain/data

# Restart chain
sudo systemctl start emped && sudo journalctl -u emped -f -o cat
```
