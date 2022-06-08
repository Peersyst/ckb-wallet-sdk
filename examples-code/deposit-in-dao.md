# Deposit in DAO

This example shows how to deposit any amount of CKB in the DAO. You will be able to see the DAO balance once the transaction is committed and the wallet synchronized.

```typescript
import { ConnectionService, Environments, WalletService, Logger } from "../src";

const ckbUrl = "http://localhost:8117/rpc";
const indexerUrl = "http://localhost:8117/indexer";
const mnemonic = "private pond zero popular fashion omit february obscure pattern city camp pistol";
const amount = BigInt(500 * 10 ** 8);

const main = async () => {
    try {
        const connectionService = new ConnectionService(ckbUrl, indexerUrl, Environments.Testnet);
        const wallet = new WalletService(connectionService, mnemonic);

        const txHash = await wallet.depositInDAO(amount, mnemonic);
        Logger.info(txHash);

        // You can view DAO balance with
        const daoBalance = await wallet.getDAOBalance();
        Logger.info(daoBalance);
    } catch (error) {
        Logger.error(`${error.name}: ${error.message}`);
    }
};

main();
```

{% hint style="warning" %}
Once you deposit in the DAO you can withdraw at any time, however once withdrawn it does not earn you any money.
{% endhint %}

{% hint style="info" %}
The DAO goes in cycles of approximately 30 days. This means that if you withdraw in day 1 or 31 you may have to wait another 29 days to unlock. It is best to withdraw in the end of the cycle but not too late because you may get caught in the next cycle!
{% endhint %}
