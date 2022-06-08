# Instantiate a connection service

Once your nervos node is up and running we can begin our development by instatiating the [ConnectionService](connectionservice.md):

```typescript
import { ConnectionService, Environments, Logger } from "@peersyst/ckb-wallet-sdk";

const rpcUrl = "http://localhost:8117/rpc";
const indexerUrl = "http://localhost:8117/indexer";

const connectionService = new ConnectionService(rpcUrl, indexerUrl, Environments.Testnet);
connectionService.getBlockchainInfo().then((blockchainInfo) => {
    Logger.info(blockchainInfo);
});
```

Running this code will print the blockchain info of the node you are connected to as long as the node is running correctly.

If your node is from Mainnet use `Environments.Mainnet` to indicate the network of the node.

The connectionService instance will be used to create your wallet instance. It can be reused for other wallets. It has some rpc related functions. Usually you won't need to use them but you have more specific documentation [here](connectionservice.md).
