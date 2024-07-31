# Create Validator

```bash
symphonyd tx staking create-validator \
--amount=92000note \
--moniker="[your-moniker]" \
--identity="[your-identity]" \
--details="[your-details]" \
--website="[your-website]" \
--pubkey=$(emped tendermint show-validator) \
--chain-id=empe-testnet-2 \
--commission-rate="0.10" \
--commission-max-rate="0.20" \
--commission-max-change-rate="0.01" \
--min-self-delegation="1000000" \
--from=wallet \
--gas="auto" \
--fees=800note \
-y
```

{% hint style="info" %}
change all `your-moniker, your-identity, your-details, your-website` with anything name and detail you want
{% endhint %}
