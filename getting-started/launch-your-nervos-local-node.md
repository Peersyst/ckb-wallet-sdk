# Launch your nervos local node

{% hint style="info" %}
To use the sdk you will need a running node in the network you want to use it. If you already have one running you can safely skip this step.
{% endhint %}

## Launch your node using Docker

We recommend using docker to run your node as it is an easy and fast way to configure it.

To create the rpc and the indexer at the same time there is an image in docker that does both at the same time. The code to launch a mainnet and testnet node in local is the following:

* Launch a mainnet node rpc and indexer:

```
docker run -d -it  -p 8117:9115  --name=ckb-mainnet-indexer  -e "CKB_NETWORK=mainnet" -v "$PWD/data":/data nervos/perkins-tent:v0.43.0
```

* Launch a testnet node rpc and indexer:

```
docker run -d -it  -p 8117:9115  --name=ckb-testnet-indexer  -e "CKB_NETWORK=testnet" -v "$PWD/data":/data nervos/perkins-tent:v0.43.0
```

To check whether your rpc is correctly running you can do:

```
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_blockchain_info",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8117/rpc
```

To check if the indexer is also up query it with:

```
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_cells",
    "params": [
        {
            "script": {
                "code_hash": "0x9bd7e06f3ecf4be0f2fcd2188b23f1b9fcc88e5d4b65a8637b17723bbda3cce8",
                "hash_type": "type",
                "args": "0x8211f1b938a107cd53b6302cc752a6fc3965638d"
            },
            "script_type": "lock"
        },
        "asc",
        "0x64"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8117/indexer
```

This documentation can be seen in the following url:

{% embed url="https://hub.docker.com/r/nervos/perkins-tent" %}
Nervos perkins tent which includes rpc and indexer
{% endembed %}

## Launching your node without Docker

If you want to launch your node without Docker we recommend following nervos official docs on how to set up your node:

{% embed url="https://docs.nervos.org/docs/basics/guides/mainnet" %}
Official guide to set up your node
{% endembed %}
