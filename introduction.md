# Introduction

We have included 12 different examples showing basic functionalities on how to use the sdk. If your goal is do any of these basic functionalities this section should be enough for you.

The examples we included are:

* **create-wallet:** contains the necessary functions to create a new wallet.
* **import-wallet:** contains the necessary functions to import a wallet, synchronize it and set a callback after synchronization.
* **import-wallet-error:** contains an example of what happens if you create a wallet with an incorrect mnemonic.
* **wallet-balance:** contains the functions on how to check the balance of all the accounts of the wallet or just of a single one.
* **get-transactions:** contains the code to get all the transactions from a wallet.
* **send-transaction:** contains an example on how to send CKB to another address. It also shows how to get the status of the transaction when it is still not committed.
* **get-dao-statistics:** shows how to check your DAO statistics (maximum withdraw and earliest since).
* **get-dao-unlockable-amounts:** implements the code to obtain the DAO unlockable amounts. These are the different amounts that can be either withdrawn or unlock. Returns an approximation on when can be unlocked and the current compensation.
* **deposit-in-dao:** show how to deposit an amount in the DAO.
* **unlock-from-dao:** it actually should be called withdraw or unlock from DAO. Provides the code necessary to unlock or withdraw an amount from the DAO.
* **transfer-tokens:** this example contains the necessary information to send tokens to another address. It is still a work in progress and should not be used in mainnet.
* **issue-tokens:** contains the necessary code to issue a new token. As with transfer-token it should be done only on testnet.

All of these examples can be run locally as we explain in the following chapter.
