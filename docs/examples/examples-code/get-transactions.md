# Get transactions

Here we can see how to get all the transactions from a wallet.

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

        const transactions = wallet.getTransactions();
        Logger.info(transactions);
        Logger.info(transactions.length);
    } catch (error) {
        Logger.error(`${error.name}: ${error.message}`);
    }
};

main();
```

{% hint style="info" %}
The wallet we set as example has lots of transactions and the first synchronization may take some minutes.
{% endhint %}
