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
- _Disadvantage of random keys_: the more you generate, the more copies you must keep &#8594; conflict with principle of avoiding address reuse (reduce privacy).

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
### **Wallet Best Practice**
- The common standards:
  + Mnemonic code words, based on BIP-39
  + HD wallets, based on BIP-32
  + Multipurpose HD wallet structure, based on BIP-43
  + Multicurrency and multiaccount wallets, based on BIP-44
### **Wallet Technology Details**
#### Mnemonic Code Word (BIP-39)
- Word sequences that represent (encode) a random number used as a seed
- Sufficient to recreate the seed as well as recreate the wallet and all derived keys 
- 12 to 24 words
- Easy to read &#8594; Easy to backup
- Different from Brainwallets: Brainwallets consists of words chosen by user, wheareas mnemonic words are created randomly
- Generating mnemonic: 
  1. Create a random sequences (entropy) of 128 and 256 bits
  2. Create a checksum of random sequence by taking the first (entropy-length/32) bits of its SHA256
  3. Add the checksum to the end of the random sequence 
  4. Divide the sequence into sections of 11 bits
  5. Map each 11-bit value to a word from the predefined 2048 words 
  6. &#8594; mnemonic sequence
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0506.png) 
- From mnemonic to seed:
  + The key-stretching (PBKDF2) function take two parameter: the mnemonic and the _salt_ (make it difficult to build a lookup table enabling a brute-force attack)
  7. The first parameter: _mnemonic_ from step 6
  8. The second parameter: composed of string constant "mnemonic" ++ optional user-supplied passphrased string.
  9. PBKDF2 stretch the mnemonic and salt parameters using 2048 rounds of hashing with the HMAC-SHA512 algorithm, producing 512-bit value as seed
![image](https://github.com/bitcoinbook/bitcoinbook/blob/develop/images/mbc2_0507.png?raw=true)

#### Optional passphrase in BIP-39
- If a passphrase is used, the stretching function produce a _different_ seed from that same mnemonic
- All passphrases are valid and correspond to different seeds
- Passphrase creates 2 important features:
  + A second factor (sometimes memorized) make mnemonic useless on its own
  + A form of plausible deniability (duress wallet) (chosen passphrase leads to a small-fund vallet to distract)
- Risk of loss
  + If no one knows the passphrase, the funds are lost forever.
  + If the owner backs up the passphrase in the same place as seed, the, there no purpose of second factor
#### Working with Mnemonic Code.
- [_python-mnemonic_](https://github.com/trezor/python-mnemonic)
- [_bitcoinjs/bip39_](https://github.com/bitcoinjs/bip39)
- [_libbitcoin/mnemonic_](https://github.com/libbitcoin/libbitcoin-system/blob/master/src/wallet/mnemonic.cpp)

### **Create an HD Wallet from the Seed**
- HD Wallets are created from a single _root seed_ (128-, 256-, 512-bit random number)
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0509.png)
- The root seed is input to the HMAC-SHA512 algorithm and the resulting hash is used to create a _master private key_ (m) and a _master chain node_ (c)
  + _m_ is used to generate a master public key by using the normal elliptic curve multiplication _m * G_
  + _c_ is used to introduce entropy in the function that generates child keys from parent keys.
#### **Private child key derivation**
- HD Wallets uses _child key derivation_ (CKD) function to derive child keys from parent keys.
- CKD functions are based on one-way hash function that combines: 
  + A parent private or public keys (ECDSA uncompressed key)
  + A seed called chain node (256 bits)
  + An index number (32 bits)
- The initial chain code seed is made from the seed, while subsequent child codes are derived from each parent chain code.
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0510.png)
#### **Using derived child key**
- Child private keys are not distinguishable from random keys (cannot find parents or siblings)
- Both the child private kets and the chain code to start a new brand and derive grandchildren

#### **Extended key**
- 2 essential ingredients to create children: the key and the chain code &#8594; extended key in combination  
- Can be used to derive children
- Represented as the concatenation of the 256-bit key and 256-bit chain code to 512 bit sequence
- 2 types
  - Extended private key = private key ++ chaincode &#8594; der ive child private key (child public key)
  - Extended public key = public key ++ chaincode &#8594; derive child public key
- The extended private key can create a complete branch, whereas the extended public key can only create a branch of public keys 
- The Base58Check used for extended keys uses a special version number that results in the prefix "xprv" and "xpub" to make them recognizable.
#### **Public child key derivation**
- 2 ways to derive child public key: child private key or parent public key
- Secure public key–only deployments: Extended public key can be used to product infinite number of public keys and bitcoin addresses, but cannot spend. Extended private key can spend.
- Application: install an extended public key on a web server which can use the public key derivation function to create new bitcoin address for every transacton. The server will not have any private keys that can be vunerable to theft
- Application: cold storage or hardware wallet, extended private key stored on a paper wallet or hardware device, the extended private key kept online. To spend funds, user can use the extended private key on an offline signing bitcoin client  
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0511.png)
#### **Hardened child key derivation**
- Potential risk: Because xpub contains the chain code, if a child private keys is known, all the private keys of all the children could be revealed. Child private key + papent chain code can deduce parent private key
- Solution:
  -  hardened derivation breaks relationship between parent public key and child chain code.
  - Hardened derivation function uses the parent private key to derive child chain code, instead of parent public key

![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0513.png)
- The resulting child private key and the chain code are completely different from what would result from the normal derivation function.
- The result branch of keys can be used to produce extended public keys that are not vulnerable
#### **Index numbers for normal and hardened derivation**
- Index from 0 to 2<sup>31</sup> - 1 are used for _only_ normal derivation.
- Index from 2<sup>31</sup> to 2<sup>32</sup> - 1 are used for _only_ hardened derivation

#### **HD wallet key identifier**
- Keys in HD wallet are identified using "path" naming convention, with each level of the tree seperated by a slash (/)

| HD path      | Key described |
| ----------- | ----------- |
| m/0      |The first (0) child private key from the master private key (m)        |
| m/0/0   | The first (0) child private key from the first child (m/0)       |
| m/0'/0 | The first (0) normal child from the first hardened child (m/0') |
| m/1/0 | The first (0) child private key from the second child (m/1) |
| M/23/17/0/0 | The first (0) child public key from the first child (M/23/17/0) from the 18th child (M/23/17) from the 24th child (M/23) |

#### **Navigating the HD wallet tree structure**
- Each parent extended key can have 4 billion children: 2 million normal and 2 million hardened &#8594; difficult to navigate.
- Two BIPs offer some proposed standard:
  - BIP-43 proposes the use of the first hardened child index as a special identifier that signifies purpose of the tree structure
  - BIP-44 proposes a multiaccount structure as "purpose" number 44'. All HD wallets following the BIP-44 structure are identified by the fact that they only used one branch of the tree
- BIP-44 specifies the structure as consisting of five predefined levels: 
_m / purpose' / coin_type' / account' / change / address_index_
  - _purpose'_ is always set to 44'
  - _coin_type_ specifies type of currency, allowing for multicurrency HD/wallets. There are 3 currencies: **Bitcoin**(m/44'/0'), **Bitcoin Testnet**(m/44& #x27;/1&#x27), **Litecoin**(m/44&#x 27;/2&#x 27;)
  - _account_ allows user to subdivide their wallets into seperate logical subaccounts
  - _change_ is an HD wallet having 2 subtrees: one for creating receiving addresses, one for creating change addresses using normal derivation to 
  
| HD path      | Key described |
| ----------- | ----------- |
| M/44&#x27;/0&#x27;/0&#x27;/0/2     |The third receiving public key for the primary bitcoin account        |
| M/44&#x27;/0&#x27;/3&#x27;/1/14   | The fifteenth change-address public key for the fourth bitcoin account    |
| m/44&#x27;/2&#x27;/0&#x27;/0/1| The second private key in the Litecoin main account, for signing transactions |

