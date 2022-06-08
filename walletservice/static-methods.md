# Static methods

The statics methods in the wallet service are to create a mnemonic and to validate the correctness of a mnemonic:

```typescript
// Creates a new mnemonic
static createNewMnemonic(): string;

// Validates a mnemonic
static validateMnemonic(mnemo: string): boolean;
```
