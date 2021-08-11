# **Transaction**
- Everything else in bitcoin was designed to ensure that transactions can be created, propagated, validated, added to the global ledger (the blockchain
## **Transaction in detailed**
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0208.png)
### **Transactions - behind the scene**   
- Actual transaction look **different** from a transaction provided by block explorer
- Most of the high-level constructs we see in bitcoin application interfaces _do not exist_ in the bitcoin system.
- Alice's transaction decoded:
```
{
  "version": 1,
  "locktime": 0,
  "vin": [
    {
      "txid": "7957a35fe64f80d234d76d83a2a8f1a0d8149a41d81de548f0a65a8a999f6f18",
      "vout": 0,
      "scriptSig" : "3045022100884d142d86652a3f47ba4746ec719bbfbd040a570b1deccbb6498c75c4ae24cb02204b9f039ff08df09cbe9f6addac960298cad530a863ea8f53982c09db8f6e3813[ALL] 0484ecc0d46f1918b30928fa0e4ed99f16a0fb4fde0735e7ade8416ab9fe423cc5412336376789d172787ec3457eee41c04f4938de5cc17b4a10fa336a8d752adf",
      "sequence": 4294967295
    }
  ],
  "vout": [
    {
      "value": 0.01500000,
      "scriptPubKey": "OP_DUP OP_HASH160 ab68025513c3dbd2f7b92a94e0581f5d50f654e7 OP_EQUALVERIFY OP_CHECKSIG"
    },
    {
      "value": 0.08450000,
      "scriptPubKey": "OP_DUP OP_HASH160 7f9b1a7fb68d60c536c2fd8aeaa53a8f3cc025a8 OP_EQUALVERIFY OP_CHECKSIG",
    }
  ]
}
```
- In bitcoin, there are no coins, no senders, no recipients, no balances, no accounts, no addresses
## **Transaction Outputs and Inputs**
- Transaction output:
   - Fundamental building block of a bitcoin transaction
   - Indivisible chunks of bitcoin currency, recorded on blockchain, recognized as valid by the entire network.
- Bitcoin all node track all _unspent transactions outputs_ (UTXO)
- Collection of UTXO:  _UTXO set_,currently numbers in the millions of UTXO
- Every transaction represents a change (state transition) in UTXO set
- When we say a user's wallet has **received bitcoin**, it means that the wallet has **detected** on the blockchain **an UTXO** that **can be spent** with one of the keys controlled by that wallet.
- User's bitcoin "balance":
  -  Sum of all UTXO that user's wallet can spend.
  -  Calculated by scanning the blockchain and aggregating value of any UTXO that wallet can spend.
  -  Most wallet maintains database to store a quick reference set of UTXO
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0609.png)
- Outputs are _discrete_ and _invisible_ units of value, denominated in integer satoshis.
- If UTXO > desired value for transaction, it consumed entirely and generate change.
- All of the complex assembly is done by user's wallet automatically and is invisible to people.
- Exception of transaction chain: _coinbase transaction_ - the first transaction in each block which is placed by the "winning miner" and creates brand-new bitcoin payable to that miner.
- Inputs or Outputs come first ? Outputs
### **Transaction Outputs**
- Transactions create outputs,  outputs create spendable chunks of bitcoin called UTXO, UTXO is recognized by the whole network and available for user to spend in further transaction.
- New transactions spend one or more of these outputs from the UTXO set
- Transaction outputs consists of 2 part:
   - An **amount of bitcoin**, denominated in _satoshis_, the smallest bitcoin unit
   - A **cryptographic puzzle** (_locking script_, _witness script_, scriptPubKey) that determines the conditions required to spend the output.
- Alice's transaction contains two outputs, each is defined by a value and a cryptographic puzzle, value is shown in bitcoin, cryptographic puzzle is shown as scriptPubKey:
```
"vout": [
  {
    "value": 0.01500000,
    "scriptPubKey": "OP_DUP OP_HASH160 ab68025513c3dbd2f7b92a94e0581f5d50f654e7 OP_EQUALVERIFY
    OP_CHECKSIG"
  },
  {
    "value": 0.08450000,
    "scriptPubKey": "OP_DUP OP_HASH160 7f9b1a7fb68d60c536c2fd8aeaa53a8f3cc025a8 OP_EQUALVERIFY OP_CHECKSIG",
  }
]
```
#### **Transaction serialization - outputs**
- When transactions are transmitted, they are serialized
- Transactional output serialization:

| Size | Field | Description |
| ------- | ------- | ------- |
| 8 bytes (little-endian) | Amount | Bitcoin value in satoshis (10<sup>-8</sup> bitcoin) |
| 1–9 bytes (VarInt) | Locking-Script Size | Locking-Script length in bytes, to follow |
| Variable | Locking-Script | A script defining the conditions needed to spend the output |

- Most bitcoin wallet do not store transactions internally as bytestreams, but as data structure (often object-oriented structures)
- The process of converting byte-stream representation to library's internal representation is called _deserialization_ or _transaction parsing_. 
- The process of converting back to byte-stream (for hashing or storage) is called _serialization_
- Most bitcoin lib have built-in function for serialization and deserialization

### **Transactional Inputs**
- Identify which UTXO will be consumed and provide the proof of ownership.
- To build a transaction, wallet selects from UTXO it controls.
- For each UTXO that will be consumed, the wallet creates one input pointing to the UTXO and unlocks it with an unlocking script.
- Inputs consist of 4 part
  - A transaction id, refering to the transaction containing UTXO being spent
  - An output index (vout), identifying which UTXO from that transaction.
  - A scriptSig, which satisfies conditions place on UTXO, unlocking it for spending.
  - A sequence of number
```
"vin": [
  {
    "txid": "7957a35fe64f80d234d76d83a2a8f1a0d8149a41d81de548f0a65a8a999f6f18",
    "vout": 0,
    "scriptSig" : "3045022100884d142d86652a3f47ba4746ec719bbfbd040a570b1deccbb6498c75c4ae24cb02204b9f039ff08df09cbe9f6addac960298cad530a863ea8f53982c09db8f6e3813[ALL] 0484ecc0d46f1918b30928fa0e4ed99f16a0fb4fde0735e7ade8416ab9fe423cc5412336376789d172787ec3457eee41c04f4938de5cc17b4a10fa336a8d752adf",
    "sequence": 4294967295
  }
]
```
- To find the UTXO's value, locking script, we must retrieve the referenced UTXO by retrieving the parent transaction containing it
- Transaction seem **incomplete**: When writing bitcoin software, anytime you decode a transaction, your code will first have to retrieve the referenced UTXO from the blockchain to build the context implied but not present in the UTXO references of the inputs &#8594; single operation involves multiple steps

#### **Transaction serialization - inputs**
- When transactions are serialized for transmission, their inputs are encoded into a byte stream :

| Size | Field | Description |
|-------|-------| -------|
| 32 bytes | Transaction Hash | Pointer to the transaction containing the UTXO to be spent | 
| 4 bytes | Output Index | The index number of the UTXO to be spent; first one is 0 |
| 1-9 bytes (VarInt) | Unlocking-Script Size | Unlocking-Script length in bytes, to follow |
| Variable | Unlocking-Script | A script that fulfills the conditions of the UTXO locking script |
| 4 bytes | Sequence Number | Used for locktime or disabled (0xFFFFFFFF) |

- ScriptSig is a specific type of unlocking script that when serialized for transmission on the network, inputs are encoded into bytestream as shown

| Size | Field | Description | 
|-------|-------|-------|
|1-9 bytes (VarInt)| Signature Size | Signature length in bytes, to follow|
| Variable | Signature | A signature that is produced by the user's wallet from his or her private key, which includes a SIGHASH |
| 1-9 bytes (VarInt) |Public Key Size| Public key length in bytes, to follow |
|Variable | Public key | The public key, unhashed |

### **Transaction Fees**
- Most transactions include transaction fees whch **compensate the bitcoin miners** and **serve as a security mechanism**
- Most **wallet calculate** and include transaction fees **automatically**. However, if transactions are **constructed programmatically**, fees must be manually accounted and included
- Incentive to mine a transaction into the next block and disincentive against abuse of the system by imposing 
- Transaction fees are calculated based on the **size** of the transaction in kilobytes
- Miner prioritize transactions in different criteria: fees, process transaction. \
- Transaction fees encourages priority processing: A transaction with sufficient fees is likely to be included in the next block mined.
- At first, transaction fees were constant and gradually the fee structure may be influenced by market forces based on network capacity and transaction volume.
- In Bitcoin Core, fee relay policies are set by minrelaytxfee option.
- Any bitcoin services creating transactions _must_ implement dynamic fees through a third-party fee estimation service or with a built-in fee estimation algorithm.
- Estimation algorithm: 
  - based on capacity and competition fees
  - ranging from simplistic to sophisicated
  - to estimate the reasonable fee that have high chances being selected to block.
  - 3 option: high, medium, low priority.
### **Adding Fees to Transactions**
- The data structure of transactions does not have a field for fees. Fees implied as the difference between the sum of inputs and the sum of outputs
```
Fees = Sum(Inputs) – Sum(Outputs)
```
## **Transactions Scripts and Script Language**
- When a transaction is validated, the unlocking script in each input is executed alongside the corresponding locking script to see if it satisfies the spending condition.
- Script is a very **simple language** that has designed to be **limited in scope** and executable on a range of software.
- Most transactions are based on script called Pay-to-Public-Key-Hash script. 
- Bitcoin transaction is achieved through the execution of a scripting language allowing for a nearly infinite variety of conditions to be expressed.
### **Turing Incompleteness**
- Operators in transactions are limited: no loops for complex flow control capabilities other than conditional flow control &#8594; not _Turing Complete_
- Script is not general-purpose language. A limited language prevents the transaction mechanism from being used as a vulnerability.
### **Stateless Verification**
- The transaction script language is stateless.&#8594; all information needed to execute a script is contained within the script.
- If your system verifies a script, you can be sure that every other system in the bitcoin network will also verify the script, meaning that a valid transaction is valid for everyone and everyone knows this.
### **Script Construction**
- Bitcoin's transaction validation engine relies on 2 types of script: locking and unlocking
  - Locking script (*scriptPubKey*) is a spending condition placed on an output: it specifies the conditions that must be met to spend the output in the future. You will see locking script as _witness script_ or as a _cryptographic puzzle_
  - An unlock script (*scriptSig*) is a script that solves (satisfies) the conditions placed on an output by a locking script and allows the output to be spent. Most of the time they contain a digital signature. You will 
- Every bitcoin validating node will validate transactions by executing the locking and unlocking script together: Each input contains an unlocking script and refers to a **previously existing UTXO**. The validation software will **copy** the unlocking script, **retrieve** the UTXO referenced by the input, and copy the locking script from that UTXO. The unlocking and locking script are then executed in sequence
- Combining unlocking script and locking script to evaluate a transaction script

![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0603.png)
