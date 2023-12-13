# Usefull Command

* Check node

```
curl http://your_node.example.com:1080/api/node/status | jq
```

* Auto Updated Docker

```
docker run -d \
--name watchtower \
--restart unless-stopped \
-e WATCHTOWER_CLEANUP=true -e WATCHTOWER_TIMEOUT=60s \
-v /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower
```
