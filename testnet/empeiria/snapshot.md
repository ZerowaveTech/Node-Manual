---
description: thanks to indonde for snapshot
---

# Snapshot

<pre class="language-bash"><code class="lang-bash"><strong>sudo apt update
</strong>sudo apt-get install snapd lz4 -y

# Stop the service and reset the data
sudo systemctl stop emped
cp $HOME/.empe-chain/data/priv_validator_state.json $HOME/.empe-chain/priv_validator_state.json.backup
rm -rf $HOME/.empe-chain/data

#download snapshot
url -L https://snapshots.indonode.net/empeiria/empeiria-latest.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.empe-chain
mv $HOME/.empe-chain/priv_validator_state.json.backup $HOME/.empe-chain/data/priv_validator_state.json

# Restart chain
sudo systemctl start emped &#x26;&#x26; sudo journalctl -u emped -f -o cat    
</code></pre>
