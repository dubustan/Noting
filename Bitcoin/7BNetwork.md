# **Bitcoin Network**
## **Peer-to-Peer Network Architecture**
- **Peer-to peer**(P2P): they are all equal, that there are no "special" nodes, and that all nodes share the burden of providing network services
- In addition to the bitcoin P2P protocol, other: Stratum provided by gateway routing server that are used for mining and lightweight or mobile wallets 
- "Extended bitcoin network": P2P protocol and related protocols connecting the components of the bitcoin system
## **Node Types and Roles**
- A bitcoin network node with all four functions: wallet, miner, full blockchain database, and network routing.

![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0801.png)

- _Network Routing Node_ ("N"): All nodes include the routing function to participate in the network
- _Full Node_ ("B"): a complete and up-to-date copy of the blockchain. Otherwise: SPV Nodes
- _Mining Node_ ("M"): compete to create new blocks by running specialized hardware to solve the Proof-of-Work algorithm
- _Wallet_ ("W"): 
  - Full Node: desktop bitcoin clients
  - SPV Node: running on resource-constrained devices
- There are servers and nodes running other protocols
### **The Extended Bitcoin Network**
- The main bitcoin network: 5,000 and 8,000 listening of Bitcoin Core, few hundred nodes of other implementations of the bitcoin P2P protocol
- Network edge routers: full-node clients based on the Bitcoin Core client without mining or wallet function.

![image](https://github.com/bitcoinbook/bitcoinbook/blob/develop/images/mbc2_0802.png?raw=true)
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0803.png)

## **Bitcoin Relay Networks**
- A Bitcoin Relay Network is a network that attempts to minimize the latency in the transmission of blocks between miners.
- Consisted of several specialized nodes hosted on the Amazon Web Services and served to connect miners and mining pools.
- Replaced in 2016: Fast Internet Bitcoin Relay Engine or FIBRE
- FIBRE is a UDP-based relay network that relays blocks within a network of nodes. FIBRE implements _compact block_ optimization to further reduce the amount of data transmitted and the network latency.
- Not replacements for bitcoin’s P2P network
##  **Network Discovery**
- When a new node boots up, it must discover other bitcoin nodes on the network in order to participate
- To connect to a known peer, nodes establish a TCP connection and transmit a version message including:
  - _**nVersion**_: The bitcoin P2P protocol version the client "speaks" (e.g., 70002)
  - ***nLocalServices***: A list of local services supported by the node, currently just NODE_NETWORK
  - ***nTime***: The current time
  - ***addrYou***: The IP address of the remote node as seen from this node
  - ***addrMe***: The IP address of the local node, as discovered by the local node
  - ***subver***: A sub-version showing the type of software running on this node (e.g., /Satoshi:0.9.2.1/)
  - ***BestHeight***: The block height of this node’s blockchain
- The local peer receiving a version message will examine the remote peer’s reported nVersion and decide if the remote peer is compatible
- How does a new node find peers? DNS. The option to use the DNS seeds is controlled by the option switch -dnsseed
- The command-line argument -seednode can be used to connect to one node just for introductions using it as a seed.

![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0804.png)

- When establishing connection(s), the new node send addr (own IP address) to the neighbors, neighbors send addr to their neighbors &#8594; well known 
- The newly connected node can send getaddr to neighbor to ask for list IP of other peers &#8594; find peers to connect

![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0805.png)

- Only one connection is needed to bootstrap, because the first node can offer introductions to its peer nodes and those peers can offer further introductions.
- After bootstrapping, a node will remember its most recent successful peer connections

## **Full Node (full blockchain nodes)**
- Nodes that maintain a complete and up-to-date copy of the bitcoin blockchain with all the transactions, starting from genesis block to latest block.
- Pure bitcoin experience: independent verification of all transactions without the need to rely on, or trust, any other systems.
- Require: more than one hundred gigabytes of persistent storage
## **Exchange Inventory**
- First and foremost: construct a complete blockchain
- Starting with block #0, downloading hundreds of thousands of blocks to synchronize with the network. 
- Syncing: Seeing and comparing the number of blocks. Exchange a getblocks message containing the fingerprint of the top block on their local blockchain.
- The longer peer  will identify the first 500 blocks and transmit their hashes using an inv (inventory) message. The node missing these blocks will then retrieve them.
- The node keeps track of how many blocks are "in transit" per peer connection

![image](https://github.com/bitcoinbook/bitcoinbook/blob/develop/images/mbc2_0806.png?raw=true)

## **Simplified Payment Verification (SPV) Nodes**
- Allowing space- and power-constrained to operate without using the full blockchain
- Downloading only the **block headers** and do not download the transactions (1,000 times smaller than the full blockchain)
- Analogy: full node = **tourist with detailed map**, SPV **without map**
- Reference to their depth: Verifying the chain of all blocks (but not all transactions) and link that chain to the transaction of interest.
- A transaction’s existence can be "hidden" from an SPV node. &#8594; denial-of-service attack or for a double-spending attack  &#8594; connect to serveral node to increase prob of contacting with at least 1 honest node. &#8594; network partitioning attacks or Sybil attacks
- SPV nodes use a getheaders message &#8594; peer will send up to 2,000 block headers using a single headers message
- Any transactions of interest are retrieved using a getdata request. The peer generates a tx message containing the transactions, in response
- **Privacy risk**: inadvertently reveal the addresses

![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0807.png)

## **Bloom Filter**
- A probabilistic search filter that offers an efficient way to express a search pattern while protecting privacy
- Allowing an SPV node to specify a search pattern for transactions that can be tuned toward precision or privacy
- Specific bloom filter produces accurate results, but at the expense of revealing patterns &#8594; revealing address

### **How Bloom Filters Work**
- Variable: 
  - _N_: Variable-size array of binary digits 
  - _M_: hash functions

![image](https://github.com/bitcoinbook/bitcoinbook/blob/develop/images/mbc2_0808.png?raw=true)
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0809.png)
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0810.png)
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0811.png)
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0812.png)

## **How SPV Nodes Use Bloom Filters**
1. Initialize a bloom filter as "empty"
2. Make a list of all the addresses, keys, and hashes that it is interested in
3. Add each of these to the bloom filter
4. Send a filterload message to the peer, containing the bloom filter to use on the connection.
5. Bloom filters are checked against each incoming transaction:
   - The transaction ID
   - The data components from the locking scripts of each of the transaction outputs (every key and hash in the script)
   - Each of the transaction inputs
   - Each of the input signature data components (or witness scripts)
6. The peer will then test each transaction’s output against the bloom filter and send merkleblock message that contains only block headers for blocks matching the filter and a merkle path for each matching transaction
7. Discard any false positives and uses the correctly matched transactions to update its UTXO set and wallet balance

## **SPV Nodes and Privacy**
### **Encrypted and Authenticated Connections**
- Even with bloom filters, an adversary monitoring the traffic of an SPV client or connected to it directly as a node in the P2P network can collect enough information over time to learn the addresses in the wallet of the SPV client.
### **Encrypted and Authenticated Connections**
- Original implementation of bitcoin communicates entirely in the clear &#8594; big problem for SPV nodes
#### **Tor Transport (The Onion Routing)**
- A software project and network that offers encryption and encapsulation of data through randomized network paths that offer anonymity, untraceability and privacy.
#### **Peer-to-Peer Authentication and Encryption**
- BIP-150 offers optional peer authentication that allows nodes to authenticate each other’s identity
- BIP-151 enables negotiated encryption for all communications between two nodes that support BIP-151
## **Transaction Pools**
- _memory pool, mempool, or transaction pool_ is used to keep track of transactions that are known to the network but are not yet included in the blockchain.
- If a transaction’s inputs refer to a transaction that is not yet known, such as a missing parent, the orphan transaction will be stored temporarily in the orphan pool until the parent transaction arrives.
- When a transaction is added to the transaction pool, the orphan pool is checked for any orphans that reference this transaction’s outputs (its children). Any matching orphans are then validated. If valid, they are removed from the orphan pool and added to the transaction pool, completing the chain that started with the parent transaction
- the UTXO pool is not initialized empty but instead contains millions of entries of unspent transaction outputs, everything that is unspent from all the way back to the genesis block

