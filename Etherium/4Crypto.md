# **Cryptography**
## **Keys and Addresses**
- Two types of accounts: *externally owned accounts* (EOAs) and *contracts*
- Ownership of ether by EOAs is established through digital *private keys*, *Ethereum addresses*, and *digital signatures*
- Only account addresses and digital signatures are ever transmitted and stored on the Ethereum system
- Access and control of funds is achieved with digital signatures created using the private key
- In the payment portion of an Ethereum transaction, the intended recipient is represented by an Ethereum address generated from the public key

## **Public Key Cryptography and Cryptocurrency**
- *trapdoor functions*: difficult to invert unless you are given a piece of secret information
- *discrete logarithm problem*
- They are considered a "pair" because the public key is derived from the private key
-  private key controls access by being the unique piece of information needed to create *digital signatures*
-  Anyone can verify that a transaction is valid, by checking that the digital signature matches the transaction details and the Ethereum address to which access is being requested. 
-  There is no encryption as part of the Ethereum protocol—all messages that are sent as part of the operation of the Ethereum network can (necessarily) be read by everyone

## **Private Key**
- The private key must also be backed up and protected from accidental loss

## **Cryptographic Hash Functions**
- Properties of hash functions:
  - ***Determinism***: A given input message always produces the same hash output.
  - ***Verifiability***: Computing the hash of a message is efficient
  - ***Noncorrelation***: A small change to the message should change the hash output so extensively that it cannot be correlated to the hash of the original message.
  - ***Irreversibility***: Computing the message from its hash is infeasible, equivalent to a brute-force search through all possible messages.
  - ***Collision protection***: It should be infeasible to calculate two different messages that produce the same hash output.
- Security applications: 
  - Data fingerprinting
  - Message integrity
  - Proof of work
  - Authentication
  - Pseudorandom number generators
  - Message commitment
  - Unique identifiers

### **Ethereum’s Cryptographic Hash Function: Keccak-256**
- Ethereum uses the Keccak-256 cryptographic hash function in many places
- SHA-3 refers to Keccak-256
```
Keccak256("") = c5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470

SHA3("") = a7ffc6f8bf1ed76651c14756a061d662f580ff4de43b49fa82d80a4b80f8434a
```
- Ethereum uses Keccak-256, even though it is often called SHA-3 in the code.

## **Ethereum Addresses**
- Unique identifiers that are derived from public keys or contracts using the Keccak-256 one-way hash function and keeping only last 20 bytes and add 0x
- Ethereum addresses are presented as raw hexadecimal without any checksum
### **Inter Exchange Client Address Protocol**
- The Inter exchange Client Address Protocol (ICAP) is an Ethereum address encoding that is partly compatible with the International Bank Account Number (IBAN) encoding, offering a versatile, checksummed, and interoperable encoding for Ethereum addresses
- ICAP addresses can encode Ethereum addresses or common names registered with an Ethereum name registry

