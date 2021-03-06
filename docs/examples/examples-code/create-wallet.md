# Create wallet

As we create a new wallet we do not synchronize.

```typescript
import { ConnectionService, Environments, WalletService, Logger } from "../src";

const ckbUrl = "http://localhost:8117/rpc";
const indexerUrl = "http://localhost:8117/indexer";

const main = async () => {
    try {
        const mnemonic = WalletService.createNewMnemonic();
        Logger.info(mnemonic); // Your new generated mnemonic, save it

        const connectionService = new ConnectionService(ckbUrl, indexerUrl, Environments.Testnet);
        const wallet = new WalletService(connectionService, mnemonic);

        // You can have more than 1 public address per mnemonic
        const nextAddress = wallet.getNextAddress();
        Logger.info(nextAddress);

        // To get your private key you need to put you mnemonic as sdk does not keep it
        const { privateKey, address } = wallet.getAddressAndPrivateKey(mnemonic);
        Logger.info(privateKey);
        Logger.info(address);
    } catch (error) {
        Logger.error(`${error.name}: ${error.message}`);
    }
};

main();
```

{% hint style="info" %}
Get next address returns the next address where you can receive CKB. Once this address has a transaction the same call will return a new address. This method of creating a new address every time increases the security.
{% endhint %}
