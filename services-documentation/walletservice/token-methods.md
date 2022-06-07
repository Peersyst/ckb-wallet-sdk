# Token methods

Here we will view the token related methods. Some of the methods right now are deprecated and should not be used outside testnet.

### Relevant types

```typescript
export interface TokenType {
    args: string;
    codeHash: string;
    hashType: string;
}

export interface TokenAmount {
    type: TokenType;
    amount: number;
}

export declare enum AddressType {
    Receiving = 0,
    Change = 1
}

export enum FeeRate {
    SLOW = 1000,
    NORMAL = 100000,
    FAST = 10000000,
}
```

### Token methods

```typescript
// Gets the token balance from a single account
async getTokensBalanceFromAccount(
    accountId = 0,
    addressType: AddressType = AddressType.Receiving,
): Promise<TokenAmount[]>;

// Get the token balance of the whole wallet
// Should be synchronized first
getTokensBalance(): TokenAmount[];
```

### Deprecated methods

{% hint style="warning" %}
These methods should be only used in testnet
{% endhint %}

```typescript
// Deprecated in accounts
// Issue a new token from a specific account
// Returns transaction hash
async issueTokens(
    amount: number,
    mnemo: string,
    accountId = 0,
    feeRate: FeeRate = FeeRate.NORMAL,
): Promise<string>;

// Deprecated in accounts
// Transfer a token with where its type has args token (4th param)
// Amount is the number of token to transfer. Minumum cell size required.
// Returns transaction hash
async transferTokens(
    amount: number,
    mnemo: string,
    to: string,
    token: string,
    accountId = 0,
    feeRate: FeeRate = FeeRate.NORMAL,
): Promise<string>;
```
