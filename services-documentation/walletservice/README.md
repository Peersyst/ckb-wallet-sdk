# WalletService

The WalletService is the heart of our sdk. Almost everything should be done through instances of this class.

To not have too much information together we have split this service in different parts. Here we will only view the constructor and the synchronization.&#x20;

### Relevant types

```typescript
export interface addressMapI {
    [key: string]: string;
}

export interface cellMapI {
    [key: string]: Cell[];
}

export interface transactionMapI {
    [key: string]: Transaction[];
}

export interface WalletState {
    addressMap: addressMapI;
    firstRIndexWithoutTxs: number;
    firstCIndexWithoutTxs: number;
    lastHashBlock: string;
    accountCellsMap: cellMapI;
    accountTransactionMap: transactionMapI;
}
```

### Constructor and synchronization

```typescript
// The connectionService and a mnemonic are mandatory
// walletState is useful if you will close the instance and want to sync from a given state
// onSync method is called when sync finished. Useful to persist current state
// onSyncStart is called when a synchronization start
// It throws an error when mnemonic is invalid
constructor(
    connectionService: ConnectionService,
    mnemo: string,
    walletState?: WalletState,
    onSync?: (walletState: WalletState) => Promise<void>,
    onSyncStart?: () => void,
);

// Gets current wallet state
getWalletState(): WalletState;

// Synchronizes and returns new wallet state
// Calls onSyncStart at start and and onSync when finishes
async synchronize(): Promise<WalletState>;
```
