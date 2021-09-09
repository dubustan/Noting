# **Ethereum Client**
- A software application that implements the Ethereum specification and communicates over the peer-to-peer network with other Ethereum clients
- Specification:
  - Ethereum: "Yellow paper" + Ethereum Improment Proposals &#8594; standard bahavior of an Ethereum client
  - Bitcoin: Bitcoin Core
- Ethereum has a greater diversity of implementations running on the network than any other blockchain
## **Ethereum Networks**
- There exist a variety of Ethereum-based networks that largely conform to the formal specification
- These networks often have features or attributes that require maintainers to make small change to support each network
- Not every version of Ethereum client software runs every Ethereum-based blockchain.
  - Parity, written in Rust
  - Geth, written in Go
  - cpp-ethereum, written in C++
  - pyethereum, written in Python
  - Mantis, written in Scala
  - Harmony, written in Java
### **Should I Run a Full Node?**
- You can do almost everything you need to do with a testnet node (which connects you to one of the smaller public test blockchains), with a local private blockchain like Ganache
### **Full node pros and cons**
- Advantages:
  - Supports the resilience and censorship resistance of Ethereum-based networks
  - Authoritatively validates all transactions
  - Can interact with any contract on the public blockchain without an intermediary
  - Can directly deploy contracts into the public blockchain without an intermediary
  - Can query (read-only) the blockchain status (accounts, contracts, etc.) offline
  - Can query the blockchain without letting a third party know the information you’re reading
- Disadvantages: 
  - Requires significant and growing hardware and bandwidth resources
  - May require several days to fully sync when first started
  - Must be maintained, upgraded, and kept online to remain synced

### **Public Testnet Advantages and Disadvantages**
- **Advantages:**
  - A testnet node needs to sync and store significantly less data compared to mainnet—about 75 GB depending on the network
  - A testnet node can sync fully in much less time.
  - Deploying contracts or making transactions requires test ether, which has no value and can be acquired for free from several "faucets."
- **Disadvantages:**
  - You can’t test security or use "real" money on a testnet; it runs on test ether.
  - There are some aspects of a public blockchain that you cannot test realistically on a testnet

### **Local Blockchain Simulation Advantages and Disadvantages**
- **Advantages:**
  - No syncing and almost no data on disk; you mine the first block yourself
  - No need to obtain test ether; Ganache is initialized with accounts that already hold ether for testing
  - No other users, just you
  - No other contracts, just the ones you deploy after you launch it unless you use the option of forking off an existing Ethereum node
- **Disadvantages:**
  - No users = It doesn’t behave the same as a public blockchain
  - You can’t test some scenarios that occur on a public blockchain.
