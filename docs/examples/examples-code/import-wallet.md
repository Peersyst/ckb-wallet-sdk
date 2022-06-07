# Import wallet

In this example we can see that we define a callback for the fourth parameter of the constructor of WalletService. This callback will be called when a synchronization finishes. You could also set up a fifth parameter which would be another callback called when a synchronization starts.

The third parameter (null in the example) corresponds of the WalletState. This is useful when you do not want to do full synchronization every time as it saves the state of the wallet at a given point so the next synchronization takes less time.

```typescript
import { ConnectionService, Environments, WalletService, Logger, WalletState } from "../src";

const ckbUrl = "http://localhost:8117/rpc";
const indexerUrl = "http://localhost:8117/indexer";
const mnemonic = "private pond zero popular fashion omit february obscure pattern city camp pistol";

const main = async () => {
    try {
        const connectionService = new ConnectionService(ckbUrl, indexerUrl, Environments.Testnet);

        // The third parameter given in the constructor is a callback called when a synchronize finishes
        const wallet = new WalletService(connectionService, mnemonic, null, async (walletState: WalletState) => {
            Logger.info("Got wallet State:");
            Logger.info(walletState);
        });

        await wallet.synchronize();
        const accounts = wallet.getAccountIndexes();
        Logger.info(accounts);
        const addresses = wallet.getAllAddresses();
        Logger.info(addresses);
        const newAddress = wallet.getNextAddress();
        Logger.info(newAddress);
    } catch (error) {
        Logger.error(`${error.name}: ${error.message}`);
    }
};

main();
```

{% hint style="info" %}
The mnemonic provided here is the one we used to test and contains lots of transactions. This also means that the synchronization will last a lot. If you want you can create a new wallet and send you ckb through the [faucet](https://faucet.nervos.org/).
{% endhint %}
