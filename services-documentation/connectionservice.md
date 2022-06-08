# ConnectionService

The connection service is the one necessary to communicate with the node and to make any kind of call to it. Most of the methods are used by other services but there are few that may be useful for you app.

### Relevant Types

```typescript
export enum Environments {
    Mainnet = "mainnet",
    Testnet = "testnet",
}

export type HexString = string;
export type Hexadecimal = string;
export type Hash = HexString;
export type HexNumber = Hexadecimal;
export type PackedSince = string;
export type PackedDao = string;
export type Address = string;

export interface ChainInfo {
  chain: string;
  median_time: HexNumber;
  epoch: HexNumber;
  difficulty: HexNumber;
  is_initial_block_download: boolean;
  alerts: AlertMessage[];
}

export interface AlertMessage {
  id: HexNumber;
  priority: HexNumber;
  notice_until: HexNumber;
  message: string;
}

export interface Header {
  timestamp: HexNumber;
  number: HexNumber;
  epoch: HexNumber;
  compact_target: HexNumber;
  dao: Hash;
  hash: Hash;
  nonce: HexNumber;
  parent_hash: Hash;
  proposals_hash: Hash;
  transactions_root: Hash;
  extra_hash: Hash;
  version: HexNumber;
}

export interface CellWithStatus {
  cell: {
    data: {
      content: HexString;
      hash: Hash;
    };
    output: Output;
  } | null;
  status: "live" | "unknown";
}

export interface TransactionWithStatus {
  transaction: Transaction;
  tx_status: TxStatus;
}

export interface TxStatus {
  block_hash?: Hash;
  status: string;
}

export interface Transaction {
  cell_deps: CellDep[];
  hash?: Hash;
  header_deps: Hash[];
  inputs: Input[];
  outputs: Output[];
  outputs_data: HexString[];
  version: HexNumber;
  witnesses: HexString[];
}

export interface Input {
  previous_output: OutPoint;
  since: PackedSince;
}

export interface OutPoint {
  tx_hash: Hash;
  index: HexNumber;
}

export interface Output {
  capacity: HexString;
  lock: Script;
  type?: Script;
}

export interface Script {
  code_hash: Hash;
  hash_type: HashType;
  args: HexString;
}

export type HashType = "type" | "data" | "data1";
```

### Static methods

```typescript
// Providing an environment and address returns a boolean indicating:
// true address is Blake160, Blake160Multisig, ACP, Onepass
// false address is of another kind or invalid
static isAddress(network: Environments, address: string): boolean;
```

{% hint style="info" %}
This is probably the most useful method in this service for anyone using the sdk.
{% endhint %}

### Constructor and class methods

{% hint style="info" %}
We have omitted some of the methods for simplicity and because they should not be used outside of its context.
{% endhint %}

```typescript
// ckbUrl is the url of the node rpc
// indexerUrl is the url of the node indexer
// env is the environment of the node
constructor(ckbUrl: string, indexerUrl: string, env: Environments);

// Returns info of the blockchain connected by the rpc
async getBlockchainInfo(): Promise<ChainInfo>;

// Gets latest block header in the blockchain
async getCurrentBlockHeader(): Promise<Header>;

// Gets a block header from its hash
async getBlockHeaderFromHash(blockHash: string): Promise<Header>;

// Get a block header from its hex number
async getBlockHeaderFromNumber(blockNumber: string): Promise<Header>;

// Gets a cell by its out point
async getCell(outPoint: OutPoint): Promise<CellWithStatus>;

// Gets a transaction with status from a hash
// Useful for when the transaction is still not committed
// For transactions that fave not finished you should set useMap = false to not receive the same!
async getTransactionFromHash(transactionHash: string, useMap = true): Promise<TransactionWithStatus>;

// Get current environment
getEnvironment(): Environments;

// Gets rpc. Useful if you want to use methods not implemented here
// Check @ckb-lumos rpc class implementation for all the methods
getRPC(): RPC;

// Gets indexer. Useful if you want to use methods not implemented here
// Check @ckb-lumos indexer class implementation for all the methods
getIndexer(): IndexerType;

// Get current ckb url
getCKBUrl(): string;

// Get current indexer url
getIndexerUrl(): string;

// Generates an address from a lock script
getAddressFromLock(lock: Script): string;

// Gets the locks script from an address
getLockFromAddress(address: string): Script;

// Providing an address returns a boolean indicating:
// true address is Blake160, Blake160Multisig, ACP, Onepass
// false address is of another kind or invalid
isAddress(address: string): boolean;
```

{% hint style="warning" %}
The method `getTransactionFromHash` can be used but returns a different type of transaction. Better use the [WalletService](walletservice/common-methods.md#methods) option as it is the same type as `getTransactions`.&#x20;
{% endhint %}
