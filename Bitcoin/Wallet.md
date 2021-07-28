# **Wallet**
- Wallet is an application that serve as the primary user interface, controls access to user's money, managing key and user address, or a data structure used to store and manage user's keys
## **Wallet Technology Overview**
- The wallet contain keys, not coins.
- User signs transactions with the key, thereby proving they own the transactions output (coins)
- Two types of wallet:
  + _nondeterministic wallet_: the key are not related to each other (JBOK - Just a Bunch Of Keys)
  + _deterministic wallet_: all keys derived from a single master key named _seed_
### **Nondeterministic (Random) Wallets**
- In the first bitcoin wallet (Bitcoin Core), wallets were collections of randomly generated private key
- Such wallets are being replaced because they are cumbersome to manage, backup, import.
- _Disadvantage of random keys_: the more you generate, the more copies you must keep -> conflict with principle of avoiding address reuse (reduce privacy).

### **Deterministic (Seeded) Wallets**
- Keys derived from one seed through one-way hash function.
- Seed is a randomly generated number combined with other data
- Seed is sufficient to recover all derived keys, import and export.
### **HD Wallet**
- The most advanced form of deterministic wallets defined by BIP-32
- Contain keys derived in a tree structure.
- Advantages:
  + Tree structure can be used to express addtional organizational meaning.
  + Able to create a sequence of public keys without having access to -> allow HD Wallet to be used on an insecure server or in a receive-only  capacity.
### **Seeds and Mnemonic Codes (BIP-39)**
- Most bitcoin wallets use the standard defined by BIP-39, are able to im/export seeds for backup and recovery using interoperable mnemonics
