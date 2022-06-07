# Get DAO unlockable amounts

Here we can see how to get DAO unlockable amounts. An unlockable amount is either a deposit in the dao or a withdraw not yet unlocked. Both types have and approximated optimal time to unlock and the current compensation amount.

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

        const unlockableAmounts = await wallet.getDAOUnlockableAmounts();
        Logger.info(unlockableAmounts);
    } catch (error) {
        Logger.error(`${error.name}: ${error.message}`);
    }
};

main();
```

{% hint style="info" %}
Unlockable amounts are used to either withdraw and unlock from the DAO. To see the full documentation on the type go [here](../../services-documentation/walletservice/dao-methods.md).
{% endhint %}
