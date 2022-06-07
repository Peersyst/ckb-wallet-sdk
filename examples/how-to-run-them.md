# How to run them

The first thing that should be done is to clone or fork the package. For example:

```
git clone git@github.com:Peersyst/ckb-wallet-sdk.git
```

The next step is to modify the node urls or mnemonic or other parameters of the example you want to run. All examples have some definitions of variables before the function main. These should be the ones to modify. For example:

```typescript
import { ConnectionService, Environments, WalletService, Logger, WalletState } from "../src";

const ckbUrl = "http://localhost:8117/rpc";
const indexerUrl = "http://localhost:8117/indexer";
const mnemonic = "private pond zero popular fashion omit february obscure pattern city camp pistol";

// Main function
...
```

Once the example is set-up as you wish you can run it with the following code:

```
npm run example --name=<example-name>
```

If the example you want to run is named create-wallet.ts you should execute:

```
npm run example --name=create-wallet
```
