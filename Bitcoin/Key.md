# **Key, Address**
## **Introduction**
- Ownership of bitcoin: _digital keys, bitcoin addresses, digital signatures_
### Digital keys
- Stored in a file, or _wallet_ (simple data base), completely independent of the bitcoin protocol.
- Enabling many of the interesting properties of bitcoin.
- Coming in pairs: private (secret) key and a public key. The public key is used to receive funds, and the private key is used to sign transactions to spend the funds.
### Digital signatures
- Most bitcoin transactions require digital signatures, which can be only generated with a secret key (including copy)
- The digital signature used to spend funds is also referred to as a _witness_, which testtifies to the true ownership of the funds being spent 
### Bitcoin address
- Generated from and correspond to a public key. (not all)
- Abstract the recipent of funds, making transaction destinations flexible.
- The only representation of the keys that users will routinely see, because this is the part they need to share with the world.
## **Public Key Cryptography and Cryptocurrency**
- Invented in 1970s
- Using elliptic curve multiplication as the basis for cryptography
- Using public key cryptography to create a key pair controlling access to bitcoin
- When spending bitcoin, the current owner presents public keys and signature (different each time) in a transaction for everyone to verify.
### Private and Public Keys 
- The private key (**k**) is a random number. 
- Using elliptic curve multiplication from the **k** to generate public key (**K**).
- Using one-way cryptographic function from **K** to generate bitcoin address **A**
![image](https://github.com/bitcoinbook/bitcoinbook/blob/develop/images/mbc2_0401.png?raw=true)
- **k** can be applied to digital fingerprint of a transaction to produce numerical signature.

### **Private key**
- Who having **k** can control over the bitcoin secure, so **k** must remain secret and protected.
- Creating **k** is equivalent to "Pick a number between 1 and 2<sup>256</sup>"(precisely 1.1578 * 10<sup>77</sup>)(not predictable or repeatable)
### **Public key**
- **K = k * G** where **G** is the constant point called the _generator point_. The reverse
- Elliptic curve multiplication is one-way function which become the basis for unforgeable and secure digital signatures that prove ownership of bitcoin funds
#### Elliptic Curve Cryptography
- A type of asymmetric or public key cryptography based on the discrete logarithm problem as expressed by addition and multiplication on the points of an elliptic curve.
- Bitcoin uses a specific elliptic curve and set of mathematical constants, as defined in a standard called _secp256k1_
- _secp256k1_  curve: y<sup>2</sup> = (x<sup>3</sup> + 7) over Fp (where p = 2<sup>256</sup> - 2<sup>32</sup> - 2<sup>9</sup> - 2<sup>8</sup> - 2<sup>7</sup> - 2<sup>6</sup> - 2<sup>4</sup> - 1) 
- (+) operator (addition): P1, P2 on the curve, P3 = P1 + P2 on the curve (drawing a line between P1 and P2, P3 is the reflect of intersection (x, -y)).
  + if P1 and P2 are the same, the line should extend to be the tangent on the curve at this point P1.
  + In case the line P1 and P2 is vertical, P3 is _point at infinity_
  + if P1 is _point at infinity_, P1 + P2 = P2
- Multiplication is defined in the standard way that extends addition.
#### Generating a public key
- Start with **k**, multiply by **G** (always the same as part of _secp256k1_) to produce **K** 
### **Bitcoin Address**
- A string of digits and character that can be shared with anyone who want to send money.
- Consisting a string of numbers and letters, beginning with '1'
- Deriving from the public key through the use of one-way cryptographic hashing named Secure Hash Algorithm and the RACE Integrity Primitives Evaluation Message Digest (RIPEMD), specifically SHA256 and RIPEMD160
- **A = RIPEMD160(SHA256(K))** (producing 160-bit number)
- Bitcoin Addresses are almost always encoded as Base58Check
### **Base58 and Base58Check Encoding**
- Base 58 is a set of lowercase and capital letters and number without (0, O, l, I) "123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz"
- Base58Check is a Base58 encoding format having built-in error-checking code.
- Checksum is addtional 4 bytes added to the end of the data that is being encoded.
- When presented with Base58Check, the decoding software will calculate the checksum and compare it to the checksum included in the code.
- Converting data into Base58Check format
  + Add prefix (version byte).
  + Compute "double-SHA" checksum (checksum=SHA256(SHA256(prefix+data)))
  + Take first 4 bytes from the resulting 32-bype hash then add to the end
  ![image](https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/develop/images/mbc2_0406.png)
### **Key Format**
- Both keys can be represented in different formats
#### Private key format
- Can be represented in different formats in different circumstances, all of which correspond to the same 256-bit integer.
  + Hexadecimal and raw binary formats are used in software.
  + WIF for import/export of keys between wallets and often used in QR code
- Decode from Base58Check: base58check-decode
- Encode from hex to Base58Check: base58check-encode
- Encode from hex (compressed ) to Base58Check: append suffix 01 and base58check-encode
#### Public key format
- Either _compressed_ or _uncompressed_
- Uncompressed: 04 ++ 2 256-bit numbers( one for x, one for y)
- Compressed: 02 or 03 ++ ...
#### Compressed public keys
- Reduce the size of transactions and conserve disk space
- If we know X, we can calculate y by solving Y<sup>2</sup> mod p = (X<sup>3</sup> + 7) mod p. It leads to 50% reduction 
- Compressed public keys have two prefix because we have 2 solution for Y, 02 means positive, 03 means negative
- If we convert compressed key to a bitcoin address using double-hash it will produce a **different** bitcoin address. However the private key is identical to both bitcoin address.
- Compressed public keys gradually become the default.
- However not all clients support compressed public key -> when private keys are exported, WIF that is used to represent them is implemented differently in newer bitcoin wallets, to indicate that these private keys have been used to produce compressed public keys and therefore compressed bitcoin addresses

#### Compressed Private Keys
- One bytes suffix longer than uncompressed
- Private keys are not themshelves compressed and cannot be compressed.
  + Compressed Private Keys: private key from which only compressed public keys should be derived 
  + Uncompressed Private Keys: private keys from which only uncompressed public keys should be derived
- If a bitcoin wallet is able to implement compressed public keys, it will use those in all transactions.
