# **The Blockchain**
## **Introduction**
- The blockchain data structure is an ordered, back-linked list of blocks of transactions
- Visualized as a vertical stack: the first block serving as the foundation of the stack
- Each block contains the hash of its parent inside its own header
- First block ever created: _genesis block_
- Although a block has just one parent, it can temporarily have multiple children
- The child’s own identity changes if the parent’s identity changes
- In the blockchain, the most recent few blocks might be revised if there is a chain recalculation due to a fork. The remaining is less and less likely to change
## **Structure of a block**
- The block header is 80 bytes, whereas the average transaction is at least 400 bytes and the average block contains more than 1900 transactions

|Size|Field|Description|
|-|-|-|
|4 bytes|Block Size|The size of the block, in bytes, following this field|
|80 bytes|Block Header|Several fields form the block header|
|1-9 bytes (VarInt)|Transaction Counter|How many transactions follow|
|Variable|Transactions|The transactions recorded in this block|

## **Block Header**
|Size|Field|Description|
|-|-|-|
|4 bytes|Version|A version number to track software/protocol upgrades|
|32 bytes|Previous Block Hash|A reference to the hash of the previous (parent) block in the chain|
|32 bytes|Merkle Root|A hash of the root of the merkle tree of this block’s transactions|
|4 bytes|Timestamp|The approximate creation time of this block (in seconds elapsed since Unix Epoch)|
|4 bytes|Difficulty Target|The Proof-of-Work algorithm difficulty target for this block|
|4 bytes|Nonce|A counter used for the Proof-of-Work algorithm|  

## **Block Identifiers: Block Header Hash and Block Height**
- Primary identifier: cryptographic hash, a digital fingerprint
  - The resulting 32-byte hash is called the _block header hash_
  - The block’s hash is computed by each node as the block is received from the network and stored in a separate database table as part of the block’s metadata.
- Second identifier: _block height_
  - A block always has a specific block height
  - Not unique identifier
## **The Genesis Block**
- Created in 2009
- Common ancestor of all the blocks in the blockchain
- Genesis block is statically encoded within the bitcoin client software, such that it cannot be altered
- The genesis block contains a hidden message within it
## **Linking block in Blockchain**
- Bitcoin full nodes: constantly updated as new blocks are found and used to extend the chain
- To establish a link, a node will examine the incoming block header and look for the "previous block hash."

## **Merkle Trees**
- A data structure used for efficiently summarizing and verifying the integrity of large sets of data

![image](https://github.com/bitcoinbook/bitcoinbook/blob/develop/images/mbc2_0901.png?raw=true)

```
HA = SHA256(SHA256(Transaction A))
```
```
HAB = SHA256(SHA256(HA + HB))
```

![image](https://github.com/bitcoinbook/bitcoinbook/blob/develop/images/mbc2_0902.png?raw=true)
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0904.png)
![image](https://github.com/bitcoinbook/bitcoinbook/blob/develop/images/mbc2_0905.png)

```
link:code/merkle.cpp[]
```
```
# Compile the merkle.cpp code
$ g++ -o merkle merkle.cpp $(pkg-config --cflags --libs libbitcoin)
# Run the merkle executable
$ ./merkle
Current merkle hash list:
  32650049a0418e4380db0af81788635d8b65424d397170b8499cdc28c4d27006
  30861db96905c8dc8b99398ca1cd5bd5b84ac3264a4e1b3e65afa1bcee7540c4

Current merkle hash list:
  d47780c084bad3830bcdaf6eace035e4c6cbf646d103795d22104fb105014ba3

Result: d47780c084bad3830bcdaf6eace035e4c6cbf646d103795d22104fb105014ba3
```
|Number of transactions|Approx. size of block|Path size (hashes)|Path size (bytes)|
|-|-|-|-|
|16 transactions|4 kilobytes|4 hashes|128 bytes|
|512 transactions|128 kilobytes|9 hashes|288 bytes|
|2048 transactions|512 kilobytes|11 hashes|352 bytes|
|65535 transactions|16 megabytes|16 hashes|512 bytes|

## **Merkle Trees and Simplified Payment Verification (SPV)**
- Merkle trees are used extensively by SPV nodes
- SPV nodes just download block headers &#8594; use merkle path to verify transaction
  - Establish a bloom filter on its connections to peers
  - Peer will send that block using a merkleblock message containing block headers and merkle path
  - SPV node also uses the block header to link the block to the rest of the blockchain
## **Bitcoin’s Test Blockchains**
- _mainnet_: the main blockchain
- *testnet, segnet, regtest*: testing purpose
### **Testnet—Bitcoin’s Testing Playground**
- A fully featured live P2P network, with wallets, test coins, mining, and all the other features of mainnet   
- Differences:
  - Worthless coin
  - Low mining difficulty
- Difficulties: 
  - Advanced mining equipment &#8594; increasing difficulty &#8594; making coin not worthless
- Solution: Restart the testnet
- Current testnet: _testnet3_ - Not as much as mainnet, but not exactly "lightweight" either
#### **Using testnet**
To start Bitcoin Core on testnet instead of mainnet you use the testnet switch:
```
$ bitcoind -testnet
```
In the logs you should see that bitcoind is building a new blockchain in the testnet3 subdirectory of the default bitcoind directory:
```
bitcoind: Using data directory /home/username/.bitcoin/testnet3
```
To connect to bitcoind, you use the bitcoin-cli command-line tool, but you must also switch it to testnet mode:
```
$ bitcoin-cli -testnet getblockchaininfo
{
  "chain": "test",
  "blocks": 1088,
  "headers": 139999,
  "bestblockhash": "0000000063d29909d475a1c4ba26da64b368e56cce5d925097bf3a2084370128",
  "difficulty": 1,
  "mediantime": 1337966158,
  "verificationprogress": 0.001644065914099759,
  "chainwork": "0000000000000000000000000000000000000000000000000000044104410441",
  "pruned": false,
  "softforks": [
  [...]
```
### **Regtest—The Local Blockchain**
- A Bitcoin Core feature that allows you to create a local blockchain for testing purposes
- Closed systems for local testing
To start Bitcoin Core in regtest mode, you use the regtest flag:
```
$ bitcoind -regtest
```
Just like with testnet, Bitcoin Core will initialize a new blockchain under the regtest subdirectory of your bitcoind default directory:
```
bitcoind: Using data directory /home/username/.bitcoin/regtest
```
To use the command-line tool, you need to specify the regtest flag too. Let’s try the getblockchaininfo command to inspect the regtest blockchain:
```
$ bitcoin-cli -regtest getblockchaininfo
{
  "chain": "regtest",
  "blocks": 0,
  "headers": 0,
  "bestblockhash": "0f9188f13cb7b2c71f2a335e3a4fc328bf5beb436012afca590b1a11466e2206",
  "difficulty": 4.656542373906925e-10,
  "mediantime": 1296688602,
  "verificationprogress": 1,
  "chainwork": "0000000000000000000000000000000000000000000000000000000000000002",
  "pruned": false,
  [...]
```
As you can see, there are no blocks yet. Let’s mine some (500 blocks) and earn the reward:
```
$ bitcoin-cli -regtest generate 500
[
  "7afed70259f22c2bf11e406cb12ed5c0657b6e16a6477a9f8b28e2046b5ba1ca",
  "1aca2f154a80a9863a9aac4c72047a6d3f385c4eec5441a4aafa6acaa1dada14",
  "4334ecf6fb022f30fbd764c3ee778fabbd53b4a4d1950eae8a91f1f5158ed2d1",
  "5f951d34065efeaf64e54e91d00b260294fcdfc7f05dbb5599aec84b957a7766",
  "43744b5e77c1dfece9d05ab5f0e6796ebe627303163547e69e27f55d0f2b9353",
   [...]
  "6c31585a48d4fc2b3fd25521f4515b18aefb59d0def82bd9c2185c4ecb754327"
]
```
It will only take a few seconds to mine all these blocks, which certainly makes it easy for testing. If you check your wallet balance, you will see that you earned reward for the first 400 blocks (coinbase rewards must be 100 blocks deep before you can spend them):
```
$ bitcoin-cli -regtest getbalance
12462.50000000
```
## **Using Test Blockchains for Development**
- Use the test blockchains whether you are developing for Bitcoin Core, or another full-node consensus client; an application such as a wallet, exchange, ecommerce site; or even developing novel smart contracts and complex scripts.
- You can use the test blockchains to establish a development pipeline
- As you make changes, improvements, bug fixes, etc., start the pipeline again, deploying each change first on regtest, then on testnet, and finally into production.
