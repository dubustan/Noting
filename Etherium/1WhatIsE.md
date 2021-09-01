# **What is Etherium**
- Computer perspective: a deterministic but practically unbounded **state machine**, consisting of a globally accessible **singleton state** and a **virtual machine** that apply changes to that state.

- Practical perspective: an open source, globally **decentralized computing infrastructure** that executes programs called _smart contracts_. It uses a blockchain to syncronize and store the system's state changes along with a crytocurrecy called _ethered_ and constrain execution resource costs.    
## **Compared to Bitcoin**
- Etherium shares many common elements with other blockchains:
  + a peer-to-peer network
  + a Byzantine fault-tolerant consensus algorithm
  + the use of cryptographic primitives
  + a cryptocurrency (ether)
s- Difference:

| Bitcoin      | Etherium |
| ----------- | ----------- |
| primarily a ditgital currency payment network      |ether is intended as a _utility currency_ to pay for the use of Etherium platform        |
| having limited scripting language   | general-purpose programmable blockchain - running a _virtual machine_ capable of executing code of arbitrary and unbounded complexity       |
| intentionally contrained to simple true/false evaluation of spending conditions | _Turing complete_ - straightforwardly function as a general-purpose computer |
## **Components of a Blockchain**
- An open, fully blockchain are (usually):
  + A **P2P network connecting** participants propagating transactions of blocks and verified transactions, based on _gossip protocol_ 
  + **Transaction messages** representing state transitions
  + A **set of consensus roles** used to validate state transactions 
  + A **state machine** processing transactions according to the consensus roles
  + A **chain of cryptographically secured blocks** acting as journal for verified transitions
  + A **consensus algorithm** that decentralizes control over the blockchain
  + A **game-theoretically sound incentivization scheme** to economically secure the state machine
  + Open source software implementations of the above (**clients**)
- Most of these components are usually combined into a single software client.
- A _reference specification_, a mathematic description of the system to which there are a number of clients are built
- There are a huge variety of blockchain with different property. Characteristic of the blockchain: _open, public, global, decentralized, neutral, and censorship-resistant_

## **The birth of Ethereum**
- By using a general-purpose blockchain like Ethereum, a developer could program their particular application without having to implement the underlying mechanisms of peer-to-peer networks, blockchains, consensus algorithms, etc

## **Ethereum: A General-Purpose Blockchain**
- Bitcoin: 
  - Tracking units of bitcoin and their ownership
  - A distributed consensus *state machine*, where transactions cause a global *state transition* contrained by the rules of consensus, altering the ownership of coins
- Ethereum:
  - Tracking the state of currency ownership and state transitions of a general-purpose data store which hold data as *key-value tuple*
  - Storing both **code and data**, using the Ethereum blockchain to **track how this memory changes** over time
  - Ethereum state changes are governed by the **rules of consensus** and the state is **distributed globally**

## **Ethereum's Components**
- **P2P network**: Ethereum runs on the *Ethereum main network*, which is addressable on TCP port 30303, and runs a protocol called ÐΞVp2p.
- **Consensus rules**: Ethereum’s consensus rules are defined in the reference specification, the Yellow Paper
- **Transactions**: Ethereum transactions are network messages that include (among other things) a sender, recipient, value, and data payload.
- **State machine**: Ethereum state transitions are processed by the Ethereum Virtual Machine (EVM), a stack-based virtual machine that executes bytecode (machine-language instructions). EVM programs, called "smart contracts," are written in high-level languages (e.g., Solidity) and compiled to bytecode for execution on the EVM.
- **Data structures**: Ethereum’s state is stored locally on each node as a database (usually Google’s LevelDB), which contains the transactions and system state in a serialized hashed data structure called a Merkle Patricia Tree.
- **Consensus algorithm**: Ethereum uses Bitcoin’s consensus model, Nakamoto Consensus, which uses sequential single-signature blocks, weighted in importance by PoW to determine the longest chain and therefore the current state. However, there are plans to move to a PoS weighted voting system, codenamed Casper, in the near future.
- **Economic security**: Ethereum currently uses a PoW algorithm called Ethash, but this will eventually be dropped with the move to PoS at some point in the future.
- **Clients**: Ethereum has several interoperable implementations of the client software, the most prominent of which are Go-Ethereum (Geth) and Parity.
## **Ethereum and Turing Completeness**
- A system to be Turing complete if it can be used to simulate any Turing machine - _Universal Turing machine_ (UTM)
- Ethereum’s ability to execute a stored program, in a state machine called the Ethereum Virtual Machine, while reading and writing data to memory makes it a Turing-complete system and therefore a UTM
- Ethereum programs run "everywhere," yet produce a common state that is secured by the rules of consensus.
### **Turing Completeness as a "Feature"**
- The fact that Ethereum is Turing complete means that any program of any complexity can be computed by Ethereum, which brings some thorny security and resource management problems
### **Implication of Turing Completeness**
- We cannot predict the path of a program without running it
- Challenge: Every participating node (client) must validate every transaction, running any smart contracts it calls
- Ethereum can’t predict if a smart contract will terminate, or how long it will run, without actually running it.
- **Answer**: 
  - When a transaction triggers the execution of a smart contract, it must include an amount of gas that sets the upper limit of what can be consumed running the smart contract
  - The EVM will terminate execution if the amount of gas consumed by computation exceeds the gas available in the transaction.
- Gas can only be purchased as part of a transaction, and can only be bought with ether
- The price of gas is not fixed - acceptable
## **From General-Purpose Blockchains to Decentralized Applications (DApps)**
- Ethereum started as a way to make a general-purpose blockchain that could be programmed for a variety of uses, Ethereum’s vision expanded to become a platform for programming DApps.
- A DApps is composed at least:
  - Smart contracts on a blockchain
  - A web frontend user interface
  - A decentralized (P2P) storage protocol and platform (additional)
  - A decentralized (P2P) messaging protocol and platform (additional)
- 
