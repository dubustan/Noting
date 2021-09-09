# **Smart Contracts and Solidity**
- Two types of accounts: externally owned accounts (EOAs) and contract accounts.
  - EOAs are controlled by users, often via software such as a wallet application that is external to the Ethereum platform
  - Contract accounts are controlled by program code that is executed by the Ethereum Virtual Machine
- Contract accounts do not have private keys and so "control themselves" in the predetermined way prescribed by their smart contract code.
## **What is a Smart Contract?**
- A set of promises, specified in digital form, including protocols within which the parties perform on the other promises.
- Immutable computer programs that run deterministically in the context of an Ethereum Virtual Machine as part of the Ethereum network protocol
  - ***Computer programs***: Smart contracts are simply computer programs
  - ***Immutable***: Once deployed, the code of a smart contract cannot change
  - ***Deterministic***: The outcome of the execution of a smart contract is the same for everyone who runs it
  - ***EVM context***: Smart contracts operate with a very limited execution context
  - ***Decentralized world computer***: The EVM runs as a local instance on every Ethereum node, but because all instances of the EVM operate on the same initial state and produce the same final state, the system as a whole operates as a single "world computer."

## **Life Cycle of a Smart Contract**
- Typically written in a high-level language (such as Solidity) but compiled to the low-level bytecode that runs in the EVM.
- Deployed on the Ethereum platform using a special contract creation transaction, which is identified as such by being sent to the special contract creation address, namely 0x0
- Identified by an Ethereum address
- There are no keys associated with an account created for a new smart contract
- Smart contract accounts own themselves.
- Contracts *only run if they are called by a transaction*
- A contract can call another contract that can call another contract, and so on, but the **first contract** will always have been called by a **transaction** from an EOA. 
- A successful termination of a transaction means 
  - If a transaction is sent from an EOA to another EOA then **any changes to the global state** made by the transaction are recorded
  - If a transaction is sent from an EOA to a contract that does not invoke any other contracts, then **any changes to the global state** are recorded 
  - If a transaction is sent from an EOA to a contract that only invokes other contracts in a manner that propagates errors, then **any changes to the global state** are recorded
  - if a transaction is sent from an EOA to a contract that invokes other contracts in a manner that does not propagates errors, then there may **only be some changes to the global state** recorded
- A failed transaction is still recorded as having been attempted
- A contract can be “deleted” removing the code and its internal state from its address, leaving a blank account.
- The "delete" operation costs “negative gas,” a gas refund, thereby incentivizing the release of network client resources from the deletion of stored state
- Deleting a contract in this way does not remove the transaction history (past) of the contract, since the blockchain itself is immutable

## **Introduction to Ethereum High-Level Languages**
- The EVM is a virtual machine that runs a special form of code called EVM bytecode
- EVM bytecode is  difficult to understand &#8594; developers use high-level language
- Arbitrary language can lead to cumbersome
- Ethereum has several languages, together with the compilers needed to produce EVM-executable bytecode.
- Two broad programming paradigms: *imperative* and *declarative* (*procedural* and *functional*)
  - In declarative programming, we write functions that express the **logic** of a program, but not its flow. Declarative programming is used to create programs where there are **no side effects**: Haskell, SQL
  - Imperative programming, by contrast, is where a programmer writes a set of procedures that **combine the logic and flow** of a program: C++ and Java
  - Hybrid: Lisp, JavaScript, and Python.
- Currently supported high-level programming languages for smart contracts include:
  - ***LLL***: A functional (declarative) programming language, with Lisp-like syntax. It was the first high-level language for Ethereum smart contracts but is rarely used today.
  - ***Serpent***: A procedural (imperative) programming language with a syntax similar to Python. Can also be used to write functional (declarative) code, though it is not entirely free of side effects.
  - ***Solidity***: A procedural (imperative) programming language with a syntax similar to JavaScript, C++, or Java. The most popular and frequently used language for Ethereum smart contracts.
  - ***Vyper***: A more recently developed language, similar to Serpent and again with Python-like syntax. Intended to get closer to a pure-functional Python-like language than Serpent, but not to replace Serpent.
  - ***Bamboo***: A newly developed language, influenced by Erlang, with explicit state transitions and without iterative flows (loops). Intended to reduce side effects and increase auditability. Very new and yet to be widely adopted.
## **Building a Smart Contract with Solidity**
- 