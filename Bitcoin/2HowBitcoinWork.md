# **How Bitcoin Works**
## **Transactions, Blocks, Mining and the Blockchain** 
- The bitcoin system consists of users with wallet containing keys, transactions that are propagated across the network and miners who produce the consensus blockchain
- The bitcoin network can transact in fractional values, e.g., from millibitcoin (1/1000th of a bitcoin) down to 1/1000,000,000th of a bitcoin, which is known as a satoshi.
### **Bitcoin Transactions** 
#### **Definition**
- A transaction tells the network that the owner of some bitcoin value has **authorized the transfer** of that value to another owner.
- The new owner can now spend the bitcoin by creating another transaction that authorizes the transfer to another owner, an so on, in a chain of ownership
#### **Inputs and Outputs**
- Each transaction contains one or more "inputs" which are like **debits** against a bitcoin account
- On the other side of the transaction, there are one or more "outputs" which are like **credit** added to bitcoin account
- Outputs add up to slightly less than inputs and the difference represents an **implied transaction fee**
#### **Transactions Chains**
- The transactions form a chain, where the inputs from the latest transaction correspond to outputs from previous transactions
#### **Making change**
- Many bitcoin transactions will include outputs that reference both an address of the new owner and an address of the current owner, called the _change address_
- The _change address_ does not have to be the same address as that of the input and for privacy reasons is often a new address from the owner's wallet 
- Different wallets may use different strategies when aggregating inputs to make a payment requested by the user.
- Unless the wallet can aggregate inputs in such a way to exactly match the desired payment plus transaction fees, the wallet will need to generate some change. And bitcoin wallet developers strive to program this balance 
#### **Common Transaction Forms**
- _Common Transaction_: The most common form of transaction is a simple payment from one address to another, which has **one input** and **two outputs** often includes some "change" returned to the original owner. 
- _Aggregating Transaction_: aggregating several inputs to a single output.
- _Distributing Transaction_: distributing one input to multiple outputs representing multiple recipients. It is often used by commercial entities to distribute funds.

### **Constructing a Transaction**
#### **Getting the right input**
- A bit coin wallet application that runs as a full-node client actually contains a copy of every unspent output from every transaction in the blockchain, which allowing a wallet to construct transaction inputs as well as quickly verify incoming transactions as having conrrect inputs
- If the wallet application does not maintain a copy of unspent transaction outputs, it can query the bitcoin network to retrieve this information using a variety of APIs available by different providers or by asking a full-node using API call.
#### **Creating the Outputs**
- A transaction output is created in the form of a script that creates an encumbrance on the value and can only be redeemed by the introduction of a solution to the script.
#### **Adding the Transaction to the Ledger**
- Transaction must be transmitted to the bitcoin network where it will become part of the blockchain. Because the transaction contains all the information neccessary to process, it does not matter how or where it is transmitted to the bitcoin network.
- Any system that participates in the bitcoin network by "speaking" the bitcoin protocol is called a _bitcoin node_.
- Any bitcoin node that receives a valid transaction it has not seen before will immediately forward it to all other nodes to which it is connected.
### **Bitcoin Mining**
- Transaction does not become part of the _blockchain_ until it is verified and included in a block by a process called _mining_
- The mining process serves two purposes in bitcoin:
  - Validating all transactions by reference to bitcoin's _consensus rules_ => Providing security for bitcoin transactions by rejecting invalid or malformed transaction
  - Creating new bitcoin in each block, almost like a central bank printing new money.
- A successful collect a _reward_ in the form of new bitcoin and transactions fees. 
- The reward will only collected if the miner has correctly validated all the transactions to the satisfaction of rules of _consensus_ 
- The "puzzle" used in bitcoin is based on a cryptographic hash and exhibits similar characteristics: it is asymmetrically hard to solve but easy to verify, and its difficulty can be adjusted.
- The algorithm of *Proof-of-Work* involves repeatedly hashing the header of the block and a random number with the SHA26 cryptographic algorithm until a solution matching a predetermined pattern emerges.
### **Mining Transactions in Blocks**
- As new transanctions are seen by bitcoin network nodes, they get added to a temporary pool of unverified transactions.
- As miners contruct a new block, they add unverified transactions from this pool to the new block and attempt to prove the validity with the mining algo (PoW)
- Each miner starts the process of mining a new block of transaction as soon as they receive the previous block from the network. They immediately create a new block, fill it with transactions and the fingerprint of the previous block, start calculating the PoW problem.
- If they find a solution make that block valid, they win the reward 
### **Spending the Transactions**
- Full-node clients can track the sources of the funds from moment the bitcoin were first generated in a block, incrementally from transaction to transaction, until they reach the address.
- Light-weight clients can do what is called a simplified payment verification by confirming that the transaction is in the blockchain and has several block mined after it
