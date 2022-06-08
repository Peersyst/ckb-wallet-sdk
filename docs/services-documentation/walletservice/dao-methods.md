# DAO methods

In this chapter we have all the methods related to DAO in the WalletService.

### Relevant types

```typescript
export enum FeeRate {
    SLOW = 1000,
    NORMAL = 100000,
    FAST = 10000000,
}

export interface DAOStatistics {
    maximumWithdraw: bigint;
    daoEarliestSince: bigint;
}

export interface DAOBalance {
    daoDeposit: number;
    daoCompensation: number;
}

export interface DAOUnlockableAmount {
    type: "deposit" | "withdraw";
    amount: bigint;
    compensation: bigint;
    unlockable: boolean;
    remainingCycleMinutes: number;
    remainingEpochs: number;
    txHash: string;
}

export enum DAOCellType {
    DEPOSIT = "deposit",
    WITHDRAW = "withdraw",
    ALL = "all",
}
```

### Methods

```typescript
// Deposits in the DAO from a single account
// Returns the hash of the transaction
async depositInDAOSingleAccount(
    amount: bigint,
    mnemo: string,
    accountId = 0,
    feeRate: FeeRate = FeeRate.NORMAL,
): Promise<string>;

// Deposits in DAO from all the accounts with enough balance
// Returns the hash of the transaction
async depositInDAO(
    amount: bigint,
    mnemo: string,
    feeRate: FeeRate = FeeRate.NORMAL,
): Promise<string>;

// Gets DAO unlockable amounts from a single account
async getDAOUnlockableAmountsFromAccount(
    accountId = 0,
    addressType: AddressType = AddressType.Receiving,
): Promise<DAOUnlockableAmount[]>;

// Gets DAO unlockable amounts from the whole wallet
// Should be synchronized first
async getDAOUnlockableAmounts(): Promise<DAOUnlockableAmount[]>;

// Withdraws or unlocks an unlockable amount
// Returns the hash of the transaction
async withdrawOrUnlock(
    unlockableAmount: DAOUnlockableAmount,
    mnemonic: string,
    feeRate: FeeRate = FeeRate.NORMAL,
): Promise<string>;

// Gets DAO statistic from a single account
async getDAOStatisticsFromAccount(
    accountId = 0,
    addressType: AddressType = AddressType.Receiving,
): Promise<DAOStatistics>;

// Gets DAO statistic from the whole wallet
// Should be synchronized first
async getDAOStatistics(): Promise<DAOStatistics>;

// Get DAO balance from a single account
async getDAOBalanceFromAccount(
    accountId = 0,
    addressType: AddressType = AddressType.Receiving,
): Promise<DAOBalance>;

// Get DAO balance from the whole wallet
// Should be synchronized first
async getDAOBalance(): Promise<DAOBalance>;
```
