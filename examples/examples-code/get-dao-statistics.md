# Get DAO Statistics

Here we show how to get the wallet dao statistics. This statistics include the maximum withdraw amount and the earliest since.

```typescript
import { ConnectionService, Environments, WalletService, Logger } from "../src";

const ckbUrl = "http://localhost:8117/rpc";
const indexerUrl = "http://localhost:8117/indexer";
const mnemonic = "private pond zero popular fashion omit february obscure pattern city camp pistol";

const main = async () => {
    try {
        const connectionService = new ConnectionService(ckbUrl, indexerUrl, Environments.Testnet);
        const wallet = new WalletService(connectionService, mnemonic);
        await wallet.synchronize();

        const statistics = await wallet.getDAOStatistics();
        Logger.info(statistics);
    } catch (error) {
        Logger.error(`${error.name}: ${error.message}`);
    }
};

main();
```

{% hint style="info" %}
There are other methods to access information about the DAO. You can see them in the [documentation](../../services-documentation/walletservice/dao-methods.md).
{% endhint %}
