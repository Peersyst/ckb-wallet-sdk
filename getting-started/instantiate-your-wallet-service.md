# Instantiate your wallet service

Once we have instantiated the connection service the next step is to instantiate a WalletService for each wallet in each network we want to work with.

To create the service you need a mnemonic. This mnemonic can be generated or imported.&#x20;

## Create new wallet with a generated mnemonic

If, for example, you would want to create a mnemonic on mainnet you could do:

```typescript
import { ConnectionService, Environments, Logger, WalletService } from "@peersyst/ckb-wallet-sdk";

const rpcUrl = "http://localhost:8117/rpc";
const indexerUrl = "http://localhost:8117/indexer";

const mainnetConnectionService = new ConnectionService(rpcUrl, indexerUrl, Environments.Mainnet);
const myMnemonic = WalletService.createNewMnemonic();
Logger.info(myMnemonic);
const myWallet = new WalletService(mainnetConnectionService, myMnemonic);
Logger.info(myWallet.getNextAddress());
```

{% hint style="info" %}
WalletService does not save the mnemonic nor the private key. If you generate a new mnemonic make sure to save it!
{% endhint %}

At this point you can already use myWallet to get your address, send transactions or view your balance (which will be 0 as it is a newly created wallet!).

## Import a wallet from an existing mnemonic

If you already have your mnemonic you will not need to generate a new one. You can import the wallet as follows:

```typescript
import { ConnectionService, Environments, Logger, WalletService } from "@peersyst/ckb-wallet-sdk";

const rpcUrl = "http://localhost:8117/rpc";
const indexerUrl = "http://localhost:8117/indexer";

const mainnetConnectionService = new ConnectionService(rpcUrl, indexerUrl, Environments.Mainnet);
const myWallet = new WalletService(mainnetConnectionService, myMnemonic);
myWallet.synchronize().then(() => {
    Logger.info(myWallet.getBalance());
}
```

{% hint style="info" %}
Synchronizing is very important to view what your wallet has. There are some related functionalities with synchronizing such as saving the wallet state and having callbacks each time a wallet synchronizes.
{% endhint %}

## Importing and creating multiple wallets

To create multiple testnet or mainnet wallets you just need one ConnectionService for each network. For example:

```typescript
import { ConnectionService, Environments, Logger, WalletService } from "@peersyst/ckb-wallet-sdk";

// Create mainnet connection service
const mainRpcUrl = "http://localhost:8117/rpc";
const mainIndexerUrl = "http://localhost:8117/indexer";
const mainnetConnectionService = new ConnectionService(mainRpcUrl, mainIndexerUrl, Environments.Mainnet);

// Create testnet connection service
const testRpcUrl = "http://localhost:8118/rpc";
const testIndexerUrl = "http://localhost:8118/indexer";
const testnetConnectionService = new ConnectionService(testRpcUrl, testIndexerUrl, Environments.Testnet);

// Create wallets
const newMnemonic = WalletService.createNewMnemonic();
const importMnemonic = "private zero ..."
const newWalletMain = new WalletService(mainnetConnectionService, newMnemonic);
const newWalletTest = new WalletService(testnetConnectionService, newMnemonic);
const oldWalletMain = new WalletService(mainnetConnectionService, importMnemonic);
const oldWalletTest = new WalletService(testnetConnectionService, importMnemonic);
```
