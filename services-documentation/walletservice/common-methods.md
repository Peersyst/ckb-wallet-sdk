# Common methods

Here we will show all functions that are common in wallets. This includes addresses, transactions and balances.

### Relevant types

```typescript
export declare enum AddressType {
    Receiving = 0,
    Change = 1
}

export enum AddressScriptType {
    SECP256K1_BLAKE160 = "SECP256K1_BLAKE160",
    SUDT = "SUDT",
    DAO = "DAO",
}

export interface Balance {
    ckb: CKBBalance;
    tokens: TokenAmount[];
    nfts: Nft[];
    dao: DAOBalance;
}

export interface CKBBalance {
    totalBalance: number;
    occupiedBalance: number;
    freeBalance: number;
}

export interface TokenType {
    args: string;
    codeHash: string;
    hashType: string;
}

export interface TokenAmount {
    type: TokenType;
    amount: number;
}

export interface Nft {
    tokenId: string;
    tokenUri: string;
    nftName: string;
    nftSymbol?: string;
    data?: any;
    nftExtraData?: string;
    issued?: number;
    total?: number;
}

export interface DAOBalance {
    daoDeposit: number;
    daoCompensation: number;
}

export interface ScriptType {
    args: string;
    codeHash: string;
    hashType: string;
}

export interface DataRow {
    quantity: number;
    address: string;
    type?: ScriptType;
    data?: number;
}

export interface Transaction {
    status: TransactionStatus;
    transactionHash: string;
    inputs: DataRow[];
    outputs: DataRow[];
    type: TransactionType;
    scriptType?: ScriptType;
    amount: number;
    blockHash?: string;
    blockNumber?: number;
    timestamp?: Date;
}

export enum TransactionStatus {
    PENDING = "pending",
    PROPOSED = "proposed",
    COMMITTED = "committed",
    REJECTED = "rejected",
}

export enum TransactionType {
    SEND_CKB = "send_ckb",
    RECEIVE_CKB = "receive_ckb",
    SEND_TOKEN = "send_token",
    RECEIVE_TOKEN = "receive_token",
    SEND_NFT = "send_nft",
    RECEIVE_NFT = "receive_nft",
    DEPOSIT_DAO = "deposit_dao",
    WITHDRAW_DAO = "withdraw_dao",
    UNLOCK_DAO = "unlock_dao",
    SMART_CONTRACT_SEND = "smart_contract_send",
    SMART_CONTRACT_RECEIVE = "smart_contract_receive",
}

export enum FeeRate {
    SLOW = 1000,
    NORMAL = 100000,
    FAST = 10000000,
}
```

### Methods

```typescript
// Returns next receive address without any transactions
getNextAddress(): string;

// Gets lock from a specific accountId, addressType and script type
getLock(accountId = 0, addressType: AddressType, script: AddressScriptType = AddressScriptType.SECP256K1_BLAKE160): Script;
    
// Gets address from a specific accountId, addressType and script type
getAddress(accountId = 0, addressType: AddressType, script: AddressScriptType = AddressScriptType.SECP256K1_BLAKE160): string;

// Gets all addresses with at least one transactions¡
getAllAddresses(): string[];

// Gets balance from a single account
async getBalanceFromAccount(accountId = 0, addressType: AddressType = AddressType.Receiving): Promise<Balance>;

// Gets wallet total balance
async getBalance(): Promise<Balance>;

// Gets all transactions from a single account
async getTransactionsFromAccount(accountId = 0, addressType: AddressType = AddressType.Receiving): Promise<Transaction[]>;

// Gets all transactions of the wallet
getTransactions(): Transaction[];

// Get a transaction from hash
// Useful from uncommitted transactions
async getTransactionFromHash(txHash: string): Promise<Transaction>;
```
