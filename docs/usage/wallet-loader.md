# Wallet loader

In this section we will make a wallet loader that uses a storage service. The storage service will be used to save and load the wallet state.

We will show two different ways to achieve this.

### Calling `getWalletService`

{% code title="wallet-loader.ts" %}
```typescript
import { WalletService, Environments } from "@peersyst/ckb-wallet-sdk";
import { mainnetConnection, testnetConnection } from "./network-connections";
import { saveWalletState, loadWalletInfo } from "./storage-service";

export function loadWallet(walletId: number): WalletService {
    const { mnemonic, walletState, environment } = loadWalletInfo(walletId);
    
    if (environment === Environments.Mainnet) {
        const wallet = new WalletService(mainnetConnection, mnemonic, walletState);
        return wallet;
    }
    const wallet = new WalletService(testnetConnection, mnemonic, walletState);
    return wallet;
}

export function saveWallet(walletId: number, wallet: WalletService): void {
    const walletState = wallet.getWalletState();
    saveWalletState(walletId, walletState);
}
```
{% endcode %}

{% hint style="info" %}
The function `saveWallet` should be called when the app closes.
{% endhint %}

### With `onSync`

{% code title="wallet-loader.ts" %}
```typescript
import { WalletService, Environments, WalletState, Logger } from "@peersyst/ckb-wallet-sdk";
import { mainnetConnection, testnetConnection } from "./network-connections";
import { saveWalletState, loadWalletInfo } from "./storage-service";

export function loadWallet(walletId: number): WalletService {
    const { mnemonic, walletState, environment } = loadWalletInfo(walletId);
    const onSync = (walletFState: WalletState) => {
        Logger.log("New wallet state");
        saveWalletState(walletId, walletFState);
    };
    const onSyncStarts = () => {
        Logger.log("Synchronization started");
    };
    
    if (environment === Environments.Mainnet) {
        const wallet = new WalletService(mainnetConnection, mnemonic, walletState, onSync, onSyncStarts);
        return wallet;
    }
    const wallet = new WalletService(testnetConnection, mnemonic, walletState, onSync, onSyncStarts);
    return wallet;
}
```
{% endcode %}

{% hint style="info" %}
Latest wallet state will be saved automatically after every synchronization.
{% endhint %}

{% hint style="info" %}
`OnSyncStarts` is called every time a synchronization starts. May be useful on apps to show the user a synchronization is executing.
{% endhint %}
