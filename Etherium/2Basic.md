# **Ethereums Basics**
## **Ether Currency Units**
- 1 *ether*, or 1 ETH, or Ξ1, or diamonds1.
- Smallest unit: *1 ether = 10<sup>18</sup> wei*
- Ether denominations and unit names

|Value(_wei_)|Common Name|SI name|
|-|-|-|
|1|wei|Wei|
|10<sup>3</sup>|Babbage|Kilowei or femtoether|
|10<sup>6</sup>|Lovelace|Megawei or picoether|
|10<sup>9</sup>|Shannon|Gigawei or nanoether|
|10<sup>12</sup>|Szabo|Microether or micro|
|10<sup>15</sup>|Finney|Milliether or milli|
|10<sup>18</sup>|Ether|Ether|
|10<sup>21</sup>|Grand|Kiloether|
|10<sup>24</sup>||Megaether|
## **Choosing an Ethereum Wallet**
- Ethereum wallet is your **gateway** to the **Ethereum system** (holding keys and creating transactions)
- Changing wallets easily: 
  - Make a transaction that sends funds from the old wallet to the new wallet
  - Export private keys and import them into the new one

## **Control and Responsibility**
- Each user of Ethereum can and should control their own private keys which can access to funds and smart contracts
- Private key = account. Lose key = funds lost forever
- Tips:
  - Do not improvise security. Use tried-and-tested standard approaches.
  - The more important the account, the higher security measures should be taken.
  - The highest security is gained from an air-gapped device, but this level is not required for every account.
  - Never store your private key in plain form, especially digitally.
  - When you are prompted to back up a key as a mnemonic word sequence, use pen and paper to make a physical backup.
## **Getting Started with MetaMask**
- **Main Ethereum Network**: The main public Ethereum blockchain. Real ETH, real value, and real consequences.
- **Ropsten Test Network**: Ethereum public test blockchain and network
- **Kovan Test Network**: Aura consensus protocol with proof of authority (federated signing) and use the Clique consensus protocol for proof of authority–based verification.
- **Rinkeby Test Network**: Clique consensus protocol with proof of authority (federated signing)
- **Localhost 8545**: part of any public blockchain

MetaMask wallet uses the same private key and Ethereum address on all the networks it connects to
- Fees are required for gas and network testing.
## **Introducing the World Computer**
- Ethereum is much more than cryptocurrecy.
- Ether is used to pay for running _smart contract_ which are computer program running on *Ethereum Virtual Machine* (EVM).
- Each node runs a local copy of the EVM to validate contract execution, while Ethereum blockchain records the _changing state_  of the world computer.

## **Externally Owned Accounts (EOAs) and Contracts**
- *Externally owned account* (EOA): controls private keys
- *Contract account*: 
  - Has smart contract code, owned by the logic of its smart contract code.
  - Has address and can send and receive _ether_
  - When a transaction destination is a contract address, it causes that contract to run in the EVM
  - Do not has private key &#8594; Do not _initiate_ transactions
## **A Simple Contract: A Test Ether Faucet**
- Ethereum has many different high-level languages for writing contract and produce EVM bytecode.
- Dominant: Solidity
- Remix: integrated development environment (IDEs)
## **Interacting with Contract**
- Ethereum contracts are programs that control money, which run inside a virtual machine called the EVM.
- Special transaction: submit bytecodes to blockchain.
- Anytime someone sends a transaction to a contract address it causes the contract to run in the EVM, with the transaction as its input