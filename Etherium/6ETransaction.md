# **Transactions**
## **The Structure of a Transaction**
- Structure: 
  - ***Nonce***: A sequence number, issued by the originating EOA, used to prevent message replay
  - ***Gas price***: The amount of ether (in wei) that the originator is willing to pay for each unit of gas
  - ***Gas limit***: The maximum amount of gas the originator is willing to buy for this transaction
  - ***Recipient***: The destination Ethereum address
  - ***Value***: The amount of ether (in wei) to send to the destination
  - ***Data***: The variable-length binary data payload
  - ***v, r, s***: The three components of an ECDSA digital signature of the originating EOA
- Serialized: Recursive Length Prefix (RLP) 

## **The Transaction Nonce**
- The nonce is an up-to-date count of the number of confirmed transactions that have originated from an account
- nonce is calculated dynamically
- Example
  - Order the transactions
  - Make transaction unique.
- The use of the nonce is actually vital for an account-based protocol, in contrast to the “Unspent Transaction Output” (UTXO) mechanism of the Bitcoin protocol.
### **Keeping Track of Nonces**
- The nonce is a zero-based counter, meaning the first transaction has nonce 0.
- When you create a new transaction, you assign the next nonce in the sequence. But until it is confirmed, it will not count toward the getTransactionCount total.
### **Gaps in Nonces, Duplicate Nonces, and Confirmation**
- The Ethereum network processes transactions sequentially, based on the nonce
- A transaction can create an inadvertent "gap" in the nonce sequence because it is invalid or has insufficient gas.
- If you accidentally duplicate a nonce, one of them will be confirmed and one will be rejected
### **Concurrency, Transaction Origination, and Nonces**
- Ethereum, by definition, is a system that allows concurrency of operations (nodes, clients, DApps) but enforces a singleton state through consensus.

## **Transaction Gas**
- Ethereum uses gas to control the amount of resources that a transaction can use, since it will be processed on thousands of computers around the world
- Gas is separate from ether in order to protect the system from the volatility that might arise along with rapid changes in the value of ether, and also as a way to manage the important and sensitive ratios between the costs of the various resources that gas pays for
- The higher the gasPrice, the faster the transaction is likely to be confirmed
- gasLimit gives the maximum number of units of gas the transaction originator is willing to buy in order to complete the transaction
- If your transaction’s destination address is a **contract**, then the amount of gas needed can be **estimated** but not **accurated** because different conditions can lead to different execution paths

## **Transaction Recipient**
- This contains a 20-byte Ethereum address. The address can be an EOA or a contract address.
- Any 20-byte value is considered valid
- Sending a transaction to the wrong address will probably *burn* the ether sent

## **Transaction Value and Data**
- Transactions can have both value and data, only value, only data, or neither value nor data
- A transaction with only value is a *payment*
- A transaction with only data is an *invocation*

### **Transmitting Value to EOAs and Contracts**
- For EOA addresses, or rather for any address that isn’t flagged as a contract, Ethereum will record a state change, add the value you sent to the balance of the address
- If the destination address (to) is a contract, then the EVM will execute the contract and will attempt to call the function named in the data payload of your transaction
-  If there is no data in your transaction, the EVM will call a fallback function
-  A contract can reject incoming payments by throwing an exception

### **Transmitting a Data Payload to an EOA or Contract**
- When your transaction contains data, it is most likely addressed to a contract address
- Most wallets also ignore any data received in a transaction to an EOA they control
- Any interpretation of the data payload by an EOA is not subject to Ethereum’s consensus rules, unlike a contract execution.
- The data will be interpreted by the EVM as a *contract invocation*.
- Most contracts use this data more specifically as a *function invocation*

## **Special Transaction: Contract Creation**
- Contract creation transactions are sent to the zero address - nether EOA nor contract and only used as destination.
- A contract creation transaction need only contain a data payload that contains the compiled bytecode which will create the contract.
- Include an ether amount in the value to set starting balance

## **Digital Signatures**
- Purpose: 
  - Prove that the owner of the private key has authorized the spending of ether or execution of a contract
  - Guarantee non-repudiation: the proof of authorization is undeniable
  - Prove that the transaction data has not been and cannot be modified by anyone after the transaction has been signed
### **The Elliptic Curve Digital Signature Algorithm**
### **How Digital Signatures Work**
- A digital signature is a mathematical scheme that consists of two parts
  - An algorithm for creating a signature
  - An algorithm that allows anyone to verify the signature by only using the message and a public key.
####  **Creating a digital signature**
- *Sig = F<sub>sig</sub> ( F<sub>keccak256</sub> ( m ) , k )*
  - *k* is the signing private key.
  - *m* is the RLP-encoded transaction.
  - *F<sub>keccak256</sub>* is the Keccak-256 hash function.
  - *F<sub>sig</sub>* is the signing algorithm.
  - *Sig* is the resulting signature.
- Sig = ( r , s )
### **Verifying the Signature**
- One must have the signature (r and s), the serialized transaction, and the public key that corresponds to the private key used to create the signature
#### **ECDSA Math**
- The signature algorithm first generates an ephemeral (temporary) private key in a cryptographically secure way. So we have q and Q generated from q
- *s ≡ q<sup>-1</sup> (Keccak256(m) + r * k)     (mod p)*
  - _q_ is the ephemeral key
  - _r_ is the x coordinate of the ephemeral public key.
  - *k* is the signing (EOA owner’s) private key.
  - *m* is the transaction data.
  - *p* is the prime order of the elliptic curve.
- Verification is the inverse of the signature generation function
  1. Check all inputs are correctly formed
  2. Calculate _w = s<sup>-1</sup> mod p_
  3. Calculate _u<sub>1</sub> = Keccak256(m) * w mod p_
  4. Calculate _u2 = r * w mod p_
  5. Calculate the point on the elliptic curve _Q ≡ u1 * G + u2 * K (mod p)_
- If the x coordinate of the calculated point Q is equal to r, then the verifier can conclude that the signature is valid.

### **Transaction signing in practice**
- To sign a transaction in Ethereum, the originator must:
  1. Create a transaction data structure, containing nine fields: nonce, gasPrice, gasLimit, to, value, data, chainID, 0, 0.
  2. Produce an RLP-encoded serialized message of the transaction data structure
  3. Compute the Keccak-256 hash of this serialized message
  4. Compute the ECDSA signature, signing the hash with the originating EOA’s private key
  5. Append the ECDSA signature’s computed v, r, and s values to the transaction.

## **The Signature Prefix Value (v) and Public Key Recovery**
- Once you have the public key, you can compute the address easily. The process of recovering the signer’s public key is called _public key recovery_
- Given the values r and s: we can compute two possible public keys: we compute two elliptic curve points, R and R', from the x coordinate r value that is in the signature. From r we also calculate r<sup>-1</sup>, which is the multiplicative inverse of r. Finally, we calculate z, which is the n lowest bits of the message hash, where n is the order of the elliptic curve.
- The two possible public keys are then:
  - K<sub>1</sub> = r<sup>–1</sup> (sR – zG)
  - K<sub>2</sub> = r<sup>–1</sup> (sR' – zG)
## **Separating Signing and Transmission (Offline Signing)**
- The three steps of creating, signing, and broadcasting a transaction normally happen as a single operation
- The most common reason for separating is security

![image](https://raw.githubusercontent.com/ethereumbook/ethereumbook/develop/images/offline_signing.png)

- In an air-gapped system there is no network connectivity at all—the computer is separated from the online environment by a gap of "air." 

## **Transaction Propagation**
- Each Ethereum client acts as a node in a *peer-to-peer (P2P)* network, which (ideally) forms a *mesh network*
- The transaction is validated and then transmitted to all the other Ethereum nodes to validate that are *directly* connected to the originating node
- Within just a few seconds, an Ethereum transaction propagates to all the Ethereum nodes around the globe.

## **Recording on the Blockchain**
- The mining computers add transactions to a candidate block and attempt to find a proof of work that makes the candidate block valid
- Once mined into a block, transactions also modify the state of the Ethereum singleton, either by modifying the balance of an account (in the case of a simple payment) or by invoking contracts that change their internal state

## **Multiple-Signature (Multisig) Transactions**
- Ethereum’s basic EOA value transactions have no provisions for multiple signatures; however, arbitrary signing restrictions can be enforced by smart contracts with any conditions you can think of, to handle the transfer of ether and tokens alike.
- ether has to be transferred to a "wallet contract" that is programmed with the spending rules desired
- The wallet contract then sends the funds when prompted by an authorized EOA once the spending conditions have been satisfied




