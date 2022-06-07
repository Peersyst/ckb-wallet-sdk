# Nft methods

Here we can see the Nft related methods in the wallet service.

### Relevant types

```typescript
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
```

### Methods

```typescript
// Gets all nfts from a single account
async getNftsBalanceFromAccount(
    accountId = 0,
    addressType: AddressType = AddressType.Receiving,
): Promise<Nft[]>;

// Gets the nfts from the whole wallet
// Should be synchronized first
async getNftsBalance(): Promise<Nft[]>;
```
