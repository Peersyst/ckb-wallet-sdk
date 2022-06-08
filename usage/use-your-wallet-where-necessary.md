# Use your wallet where necessary

Here we will implement a class that loads a wallet and is able to do different operations on this wallet.

This class is not entirely necessary. There are other ways to achieve this but we made a class to have everything in one place. Also it allows you to modify some responses as you wish.

When the app starts you should create a `WalletWrapper` for each wallet the user has and save it in memory. A global map may be a good idea to be able to access the wallet from every component.

{% code title="WalletWrapper.ts" %}
```typescript
import { Logger, LoggingLevel, Transaction, FeeRate } from "@peersyst/ckb-wallet-sdk";
import { loadWallet } from "./wallet-loader";
import { getTokenFromTokenAmount, CustomToken } from "./wallet-loader";
import { loadWalletInfo } from "./storage-service";

export class WalletWrapper {
    private readonly wallet: WalletService;
    private readonly mnemonic: string;
    private readonly logger: Logger;

    constructor(walletId: number, loggingLevel?: LoggingLevel) {
        this.loadWalletInfowallet = loadWallet(walletId);
        this.mnemonic = loadWalletInfo(walletId);
        this.logger = new Logger(`${WalletWrapper.name}-${walletId}`, loggingLevel);
    }

    async synchronize(): Promise<void> {
        try {
            await this.wallet.synchronize();
        } catch (error) {
            this.logger.error(error.toString());
            throw error;
        }
    }

    getCKBBalance(): CKBBalance {
        return this.wallet.getCKBBalance();
    }

    async getDAOBalance(): Promise<DAOBalance> {
        try {
            return this.wallet.getDAOBalance();
        } catch (error) {
            this.logger.error(error.toString());
            throw error;
        }
    }

    getTransactions(): Transaction[] {
        return this.wallet.getTransactions();
    }

    async getTransaction(txHash: string): Promise<Transaction> {
        try {
            return this.wallet.getTransactionFromHash(txHash);
        } catch (error) {
            this.logger.error(error.toString());
            throw error;
        }
    }

    getTokensBalance(): CustomToken[] {
        const tokens = this.wallet.getTokensBalance();
        return tokens.map(getTokenFromTokenAmount);
    }

    getNfts(): Promise<Nft[]> {
        try {
            return this.wallet.getNftsBalance();
        } catch (error) {
            this.logger.error(error.toString());
            throw error;
        }
    }

    getAddress(): string {
        return this.wallet.getNextAddress();
    }

    async sendTransaction(amount: bigint, to: string, feeRate: FeeRate): Promise<string> {
        try {
            return this.wallet.sendTransaction(amount, this.mnemonic, to, feeRate);
        } catch (error) {
            this.logger.error(error.toString());
            throw error;
        }
    }

    async depositInDAO(amount: bigint, feeRate: FeeRate): Promise<string> {
        try {
            return this.wallet.depositInDAO(amount, this.mnemonic, feeRate);
        } catch (error) {
            this.logger.error(error.toString());
            throw error;
        }
    }

    async getDAOUnlockableAmounts(): Promise<DAOUnlockableAmount[]> {
        try {
            return this.wallet.getDAOUnlockableAmounts();
        } catch (error) {
            this.logger.error(error.toString());
            throw error;
        }
    }

    async withdrawOrUnlock(unlockableAmount: UnlockableAmount): Promise<string> {
        try {
            return this.wallet.withdrawOrUnlock(unlockableAmount, this.mnemonic);
        } catch (error) {
            this.logger.error(error.toString());
            throw error;
        }
    }
}
```
{% endcode %}

{% hint style="info" %}
We save the mnemonic in the class to not ask it every time to the user. We could also have it protected with a pin.
{% endhint %}

{% hint style="info" %}
On some cases we catch the errors. In these catches you could show something on screen to indicate the call failed.
{% endhint %}

{% hint style="info" %}
Having a class allows to wrap functions such as `getTokensBalance`. This function checks the type of a token and maps it to something more understandable for the user..&#x20;
{% endhint %}
