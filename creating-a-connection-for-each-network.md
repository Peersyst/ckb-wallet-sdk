# Creating a connection for each network

First off we will start creating a file that will export a connection service for mainnet and another one for testnet. We will use environment variables for the urls.

{% code title="network-connections.ts" %}
```typescript
import { ConnectionService, Environments } from "@peersyst/ckb-wallet-sdk";

const mainnetConnection = new ConnectionService(
    process.env.RPC_URL_MAIN,
    process.env.INDEXER_URL_MAIN,
    Environments.Mainnet,
);

const testnetConnection = new ConnectionService(
    process.env.RPC_URL_TEST,
    process.env.INDEXER_URL_TEST,
    Environments.Testnet,
);

export { mainnetConnection, testnetConnection };
```
{% endcode %}
