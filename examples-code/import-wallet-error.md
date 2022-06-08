# Import wallet error

This example show what happens when you enter an incorrect mnemonic.

```typescript
import { ConnectionService, Environments, WalletService, Logger } from "../src";

const ckbUrl = "http://localhost:8117/rpc";
const indexerUrl = "http://localhost:8117/indexer";
const mnemonic = "private pond zero popular fashion pistol";

const main = async () => {
    try {
        const connectionService = new ConnectionService(ckbUrl, indexerUrl, Environments.Testnet);
        new WalletService(connectionService, mnemonic);
    } catch (error) {
        Logger.error(`${error.name}: ${error.message}`);
    }
};

main();
```

{% hint style="info" %}
It is a good practice to surround the creation of a WalletService with a try catch block. This way you can act accordingly if the mnemonic is incorrect.
{% endhint %}

{% hint style="info" %}
WalletService contains a static function called validateMnemonic which returns a boolean. This way you can be sure your mnemonic is correct before creating the service. In some situations this may be preferred.
{% endhint %}
