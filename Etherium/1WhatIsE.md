# **What is Etherium**
- Computer perspective: a deterministic but practically unbounded **state machine**, consisting of a globally accessible **singleton state** and a **virtual machine** that apply changes to that state.

- Practical perspective: an open source, globally **decentralized computing infrastructure** that executes programs called _smart contracts_. It uses a blockchain to syncronize and store the system's state changes along with a crytocurrecy called _ethered_ and constrain execution resource costs.    
## **Compared to Bitcoin**
- Etherium shares many common elements with other blockchains:
  + a peer-to-peer network
  + a Byzantine fault-tolerant consensus algorithm
  + the use of cryptographic primitives
  + a cryptocurrency (ether)
- Difference:

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
