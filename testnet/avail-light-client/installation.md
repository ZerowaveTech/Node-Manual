---
description: >-
  The guide outlines how to set up an Avail light client to connect with the
  goldberg testnet. You can either:
---

# Installation

[**`availup`**](https://github.com/availproject/availup) is the recommended way of running the Avail light client for most users. `availup` is a shell wrapper that allows you to spin up your own instance of the Avail light client with a simple `curl` command.

1. to tun avail light client, just run this command:

```bash
curl -sL1 avail.sh | bash
```

2. see output:

```log
2024-03-20T10:50:25.528628Z  INFO avail_light::light_client: Processing finalized block block_number=562690 block_delay=20
2024-03-20T10:50:25.528706Z  INFO avail_light::light_client: Random cells generated: 10 block_number=562690 cells_requested=10
2024-03-20T10:50:26.069497Z  INFO avail_light::network: Cells fetched from DHT block_number=562690 cells_total=10 cells_fetched=0 cells_verified=0 fetch_elapsed=540.755792ms proof_verification_elapsed=2.208µs
2024-03-20T10:50:28.322706Z  INFO avail_light::network: Cells fetched from RPC block_number=562690 cells_total=10 cells_fetched=10 cells_verified=10 fetch_elapsed=2.232714917s proof_verification_elapsed=20.404208ms
2024-03-20T10:50:28.322987Z  INFO avail_light::light_client: Confidence factor: 99.90234375 block_number=562690 confidence=99.90234375
2024-03-20T10:50:28.323134Z  INFO avail_light::light_client: Sleeping for 14.61143875s seconds
2024-03-20T10:50:28.323154Z  INFO avail_light::api::v2: Message published to clients topic=ConfidenceAchieved published=0 failed=0
2024-03-20T10:50:28.859369Z  INFO avail_light::network::p2p::event_loop: Cell upload success rate for block 562690: 0/10. Duration: 0
2024-03-20T10:50:41.535425Z  INFO avail_light::network::rpc::subscriptions: New justification at block no.: 562692, hash: 0x3b602253298ce9bec9b5b8f0c8767f14502ccaa17a003dfba77f9d90edeaf5da
2024-03-20T10:50:41.709011Z  INFO avail_light::network::rpc::subscriptions: Header no.: 562692
2024-03-20T10:50:41.709557Z  INFO avail_light::network::rpc::subscriptions: Number of matching signatures: 5/7 for block 562692, set_id 223
2024-03-20T10:50:41.709574Z  INFO avail_light::network::rpc::subscriptions: Storing finality checkpoint at block 562692
2024-03-20T10:50:41.709908Z  INFO avail_light::network::rpc::subscriptions: Sending finalized block 562692
2024-03-20T10:50:41.709966Z  INFO avail_light::api::v2: Message published to clients topic=HeaderVerified published=0 failed=0
2024-03-20T10:50:42.936699Z  INFO avail_light::light_client: Processing finalized block block_number=562691 block_delay=20
2024-03-20T10:50:42.936761Z  INFO avail_light::light_client: Random cells generated: 10 block_number=562691 cells_requested=10
2024-03-20T10:50:43.472932Z  INFO avail_light::network: Cells fetched from DHT block_number=562691 cells_total=10 cells_fetched=0 cells_verified=0 fetch_elapsed=536.136083ms proof_verification_elapsed=3.042µs
2024-03-20T10:50:46.513570Z  INFO avail_light::network: Cells fetched from RPC block_number=562691 cells_total=10 cells_fetched=10 cells_verified=10 fetch_elapsed=3.022786041s proof_verification_elapsed=17.810542ms
2024-03-20T10:50:46.513706Z  INFO avail_light::light_client: Confidence factor: 99.90234375 block_number=562691 confidence=99.90234375
2024-03-20T10:50:46.513785Z  INFO avail_light::light_client: Sleeping for 15.195224667s seconds
2024-03-20T10:50:46.513795Z  INFO avail_light::api::v2: Message published to clients topic=ConfidenceAchieved published=0 failed=0
2024-03-20T10:50:47.056255Z  INFO avail_light::network::p2p::event_loop: Cell upload success rate for block 562691: 0/10. Duration: 0
```

3. set systemd file to auto restart the node

```bash
sudo tee /etc/systemd/system/avail.service > /dev/null <<EOF
[Unit]
Description=Avail Light Client
After=network.target
StartLimitIntervalSec=0

[Service]
User=$USER
Restart=always
RestartSec=5
ExecStart=$HOME/.avail/bin/avail-light --network goldberg --config $HOME/.avail/config/config.yml --app-id 0 --identity $HOME/.avail/identity/identity.toml
LimitNOFILE=65000

[Install]
WantedBy=multi-user.target
EOF
```

4. Running systemd

```bash
sudo systemctl daemon-reload
sudo systemctl enable avail
sudo systemctl start avail
```

5. see output log

```bash
sudo journalctl -fu avail -o cat
```

6. backup seed phrase on `$HOME/.avail/identity/identity.toml`
