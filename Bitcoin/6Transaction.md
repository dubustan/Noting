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
- Transaction fees encourages **priority processing**: A transaction with sufficient fees is likely to be included in the next block mined.
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
#### **The script execution stack**
- Bitcoin's scripting language is called a **stack-based language** because it uses a data structure called a _stack_
- The scripting language executes the script by processing each item from left to right. Operators **push or pop one or more parameters** from the stack, **act on them**, and **might push a result** onto the stack
  - OP_ADD will pop two items, compute the sum and add the result
- Conditional operators evaluate a condition, producing a boolean result of TRUE or FALSE. For example OP_EQUAL.
- Bitcoin transaction scripts usually contain a conditional operator, so that they can produce the TRUE result
#### **A s1mpl3 script**
- Although most locking scripts refer to a public key hash (bitcoin address), thereby requiring proof of ownership to spend the funds, the script does not have to be that complex. 
- Any **combination of locking and unlocking** scripts that results in a TRUE value **is valid** 

![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0604.png)

#### **Seperate execution of unlocking and locking scripts**
- In the original bitcoin client, the unlocking and locking scripts were concatenated and executed in sequence. But this was changed in 2017 due to security reason.
- Current implementation: scripts are executed seperately with the stack transferred between the two executions.
- The unlocking script is executed using stack execution engine. If the unlocking script executed successful, the main stack is copied and the locking script is executed. If the result of executing the locking script with the stack data copied from the unlocking script is "TRUE," ...
### **Pay-to-Public-Key-Hash (P2PKH)**
- Majority of transactions spend outputs locked with a P2PKH script
- These outputs contain a locking script that locks the output to a **public key hash** (bitcoin address). 
- Outputs can be unlocked (spent) by presenting a **public key** and a **digital signature**
- Example: Cafe Public Key Hash
```
Locking script: OP_DUP OP_HASH160 <Cafe Public Key Hash> OP_EQUALVERIFY OP_CHECKSIG
Unlocking script: <Cafe Signature> <Cafe Public Key>
Combine: <Cafe Signature> <Cafe Public Key> OP_DUP OP_HASH160
<Cafe Public Key Hash> OP_EQUALVERIFY OP_CHECKSIG
```
(The result will be TRUE if and only if the unlocking script has a valid signature from the cafe's private key that corresponds to the public key hash set as an encumbrance.)
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0605.png)
![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0606.png)

## **Digital signature**
- Wikipedia: A digital signature is a **mathematical scheme** for **demonstrating the authenticity** of a digital message or documents. A valid digital signature gives a recipient reason to believe that the message was created by a known sender (authentication), that the sender cannot deny having sent the message (nonrepudiation), and that the message was not altered in transit (integrity).
- Digital signature used in bitcoin is the _Elliptic Curve Digital Signature Algorithm_ or _ECDSA_ (based on elliptic curve private/public key pairs)
- ECDSA is used by the script functions OP_CHECKSIG, OP_CHECKSIGVERIFY, OP_CHECKMULTISIG and OP_CHECKMULTISIGVERIFY
- Purpose:
  - Proving the owner of private key has authorized the spending of those funds
  - Proof of authorization is _undeniable_ (nonrepudiation)
  - Proving the transaction cannot be _modified_ by anyone after it has been signed
- Note that each transaction input is signed independently

### **How Digital Signatures work**
- Digital Signature consist of 2 parts:
  -  An algorithm for creating a signature, using a private key (the signing key), from a message (the transaction)
  -  An algorithm that allows anyone to verify the signature, given also the message and a public key.
#### **Creating a digital signature**
- In ECDSA algorithm, the message being signed in a hash of a specific subset of the data in the transaction. The signing key is the user's private key:
- Result: _Sig = F<sub>sig</sub>(F<sub>hash</sub>(m), dA)_
  - dA is the signing private key
  - m is the transaction
  - F<sub>hash</sub> is the hashing function
  - F<sub>sig</sub> is the signing algorithm
- F<sub>sig</sub> produces a signature Sig: Sig = (R, S)
- R and S are serialized into a byte-stream using an international standard encoding scheme called _Distinguished Encoding Rules_ (DER)
#### **Serialization of signatures (DER)**
- The signature is a serialized byte-stream of the R and S values produced by Alice's wallet to prove she owns the private key authorized to spend that output.
- The serialization format consists of 9 elements as follows:
  - 0x30 - start of a DER sequence
  - 0x45 - the length of the sequence (69 bytes)
  - 0x02 - an integer value follows 
  - 0x21 - the length of an integer (33 bytes) 
  - R - 00884d142d86652a3f47ba4746ec719bbfbd040a570b1deccbb6498c75c4ae24cb
  - 0x02 - another integer follows 0x20-the length of an integer (32 bytes)
  - 0x20 - the length of the integer (32 bytes)
  - S - 4b9f039ff08df09cbe9f6addac960298cad530a863ea8f53982c09db8f6e3813
  - A suffix (0x01) indicating the type of hash used (SIGHASH_ALL)
```
3045022100884d142d86652a3f47ba4746ec719bbfbd040a570b1deccbb6498c75c4ae24cb02204b9f039ff08df09cbe9f6addac960298cad530a863ea8f53982c09db8f6e381301
```
### **Verifying the Signature**
- Requirement: signature (S and R), serialized transaction, the public key (corresponding to the private key to create signature)
- Meaning: "Only the owner of the private key that generated this public key could have produced this signature on this transaction"
- The signature verification algorithm takes message (hash of the transaction or part), the signer's public key and the signature (R and S) return TRUE if ..
### **Signature Hash Types (SIGHASH)**
- The signature implies a _commitment_ to specific transaction data.
- The signature applies to the entire transaction or a subset of data in transaction.
- The SIGHASH flag is a single byte that appended to the signature. Every signature has a different SIGHASH flag
- Each input may contain 1 signature &#8594; A transaction with multiple inputs may have several signatures with several SIGHASH flags
- Modifier flag SIGHASH_ANYONECANPAY: one input is signed, leaving the rest for modification.

|SIGHASH flag|Value|Description|
|--|--|--|
|ALL|0x01|Signature applies to all inputs and outputs|
|NONE|0x02|Signature applies to all inputs, none of the outputs|
|SINGLE|0x03|Signature applies to all inputs but only the one output with the same index number as the signed input|
|ALL\|ANYONECANPAY|0x81|Signature applies to one input and all outputs|
|NONE\|ANYONECANPAY|0x82|Signature applies to one input, none of the outputs|
|SINGLE\|ANYONECANPAY|0x83|Signature applies to one input and the output with the same index number|

![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/sighash_combinations.png)

- The way SIGHASH flags are applied:
  - A copy of the transaction is made and certain fields within are truncated 
  - Resulting transaction is **serialized**
  - **SIGHASH is added** to the end of the serialized transaction and **result is hashed**
  - The hash itself is the message
- The SIGHASH type itself is appended to the transaction **before it is signed**, so that it can’t be modified once signed

#### **ECDSA Math**
- Signature algo first generates an _ephemeral_ (temporary) private public key pair. This key pair is used in the calculation of S and R after a transformation involving the signing private key and the transaction hash
- The temporary key pair is based on random number _k_ used as temporary private key. From _k_ we generate the temporary public key P (_P = k * G_). The _R_ value of the digital signature is the *X* coordinate of _P_
- _S = k<sup>-1</sup>(Hash(m) + dA * R) mod n_
  - _k_ is the ephemeral private key
  - _dA_ is the signing private key
  - _m_ is the transaction data
  - _n_ prime order of elliptic curve 
- _R, S_ can be used to calculate P (point on the elliptic curve) (the ephemeral public key used in signature creation)
-  _P = S<sup>-1</sup> * Hash(m) * G + S<sup>-1</sup> * R * Qa_
  - _R, S_: signatures value
  - _Qa_: Alice's public key
  - _m_: transaction data
### **The Importance of Randomness in Signatures**
- If the same value k is used in the signing algorithm on **two different transactions**, the private key can be **calculated** and **exposed to the world!**
- The industry-standard algorithm for deterministic initialization of k is defined in RFC 6979, published by the Internet Engineering Task Force
## **Bitcoin Addresses, Balances, and Other Abstractions**
- We saw that transactions don’t contain bitcoin addresses, per se, but instead operate through scripts that lock and unlock discrete values of bitcoin

![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0208.png)
- Left: Alice's bitcoin address. Blockchain explorer references to the previous transaction associated with the input and extracts the first output from the older transaction. The blockchain explorer extracted the public key hash and encoded (Base58Check) to produce and display bitcoin address
- Right: 2 outputs: Bob's address and Alice's address (as change). To create these bitcoin addresses, the blockchain explorer extracted the locking script from each output, recognized it as a P2PKH script, and extracted the public-key-hash from within. Finally, the blockchain explorer reencoded each public key hash with Base58Check to produce and display the bitcoin addresses.

![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0608.png)
- The blockchain explorer displays the balance of Bob’s bitcoin address
- Construct the "Total Received" amount: **decode  Base58Check bitcoin address** to **retrieve** the 160-bit hash of **Bob's public key** that is encoded within address. The blockchain explorer will **search through the database** of transactions, **looking for outputs** with P2PKH locking script that **contain Bob's public key hash**. By summing up the value of all the outputs, the blockchain explorer can produce the total value received.
- Constructing "Final balance": The blockchain explorer keeps the UTXO set. The blockchain explorer must monitor the bitcoin network, add newly created UTXO, and remove spent UTXO as they appear in unconfirmed transactions
