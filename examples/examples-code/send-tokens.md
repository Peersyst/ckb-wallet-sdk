# Send Tokens

Here we show how to send a tokens you own. There is no need to sync before calling `transferTokens` as it synchronizes internally before making any transaction.

```typescript
import { ConnectionService, Environments, WalletService, Logger } from "../src";

const ckbUrl = "http://localhost:8117/rpc";
const indexerUrl = "http://localhost:8117/indexer";
const mnemonic = "private pond zero popular fashion omit february obscure pattern city camp pistol";
const receivingAddress = "ckt1qzda0cr08m85hc8jlnfp3zer7xulejywt49kt2rr0vthywaa50xwsqflx85grt0mnny6qsqwfxwkkvud4x3gwqgq2d0su";
const quantity = 10;
const token = "0x099472fc82e74d050d524ba32f8efc05d4a53800f4ab0bf88be9c3383586339a";

const main = async () => {
    try {
        const connectionService = new ConnectionService(ckbUrl, indexerUrl, Environments.Testnet);
        const wallet = new WalletService(connectionService, mnemonic);

        const txHash = await wallet.transferTokens(quantity, mnemonic, receivingAddress, token);
        Logger.info(txHash);

        // This balance will be updated when we sync after the tx status is committed
        await wallet.synchronize();
        const tokensBalance = wallet.getTokensBalance();
        Logger.info(tokensBalance);
    } catch (error) {
        Logger.error(`${error.name}: ${error.message}`);
    }
};

main();
```

{% hint style="warning" %}
This method is not properly tested and should be used only on testnet.
{% endhint %}

{% hint style="info" %}
The hash in the variable token is the args value of the type of the token. Tokens are stored in cells with a type that has the codeHash of SUDT and the args value depends on who has issued the token.
{% endhint %}
