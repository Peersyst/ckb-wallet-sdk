# CKB methods

In this chapter we will see the ckb related methods. This includes the creating ckb transactions and getting ckb balance.

### Relevant types

```typescript
export enum FeeRate {
    SLOW = 1000,
    NORMAL = 100000,
    FAST = 10000000,
}

export interface CKBBalance {
    totalBalance: number;
    occupiedBalance: number;
    freeBalance: number;
}
```

### Methods

```typescript
// Sends a transaction from a single account
// Returns the transaction hash
async sendTransactionSingleAccount(
    amount: bigint,
    mnemo: string,
    to: string,
    accountId: number,
    feeRate: FeeRate = FeeRate.NORMAL,
): Promise<string>;

// Sends a transaction from all the accounts in the wallet
// Returns the transaction hash
async sendTransaction(
    amount: bigint,
    mnemo: string,
    to: string,
    feeRate: FeeRate = FeeRate.NORMAL,
): Promise<string>;

// Gets the ckb balance of a single account
async getCKBBalanceFromAccount(
    accountId = 0,
    addressType: AddressType = AddressType.Receiving,
): Promise<CKBBalance>;

// Get the ckb balance of the wallet
// Should be synchronized first
getCKBBalance(): CKBBalance;
```
