# Snapshot

```bash
sudo apt update
sudo apt-get install snapd lz4 -y

#stop symphony node
sudo systemctl stop emped
cp $HOME/.symphonyd/data/priv_validator_state.json $HOME/.symphonyd/priv_validator_state.json.backup
rm -rf $HOME/.symphonyd/data

#download snapshot
curl -L https://snapshots.indonode.net/symphony/symphony-latest.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.symphonyd
mv $HOME/.symphonyd/priv_validator_state.json.backup $HOME/.symphonyd/data/priv_validator_state.json

# Restart chain
sudo systemctl start symphonyd && sudo journalctl -u symphonyd -f -o cat
```
