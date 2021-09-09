# **Tokens**
- It is commonly used to refer to privately issued special-purpose coin-like items of insignificant intrinsic value, such as transportation tokens, laundry tokens, and arcade game tokens.
## **How Tokens Are Used**
- The most obvious use of tokens is as digital private currencies
- Tokens can be programmed to serve many different functions, often overlapping
  - ***Currency***: A token can serve as a form of currency, with a value determined through private trade.
  - ***Resource***: A token can represent a resource earned or produced in a sharing economy or resource-sharing environment; for example, a storage or CPU token representing resources that can be shared over a network.
  - ***Asset***: A token can represent ownership of an intrinsic or extrinsic, tangible or intangible asset; for example, gold, real estate, a car, oil, energy, MMOG items, etc.
  - ***Access***: A token can represent access rights and grant access to a digital or physical property, such as a discussion forum, an exclusive website, a hotel room, or a rental car.
  - ***Equity***: A token can represent shareholder equity in a digital organization (e.g., a DAO) or legal entity (e.g., a corporation).
  - ***Voting***: A token can represent voting rights in a digital or legal system.
  - ***Collectible***: A token can represent a digital collectible (e.g., CryptoPunks) or physical collectible (e.g., a painting).
  - ***Identity***: A token can represent a digital identity (e.g., avatar) or legal identity (e.g., national ID).
  - ***Attestation***: A token can represent a certification or attestation of fact by some authority or by a decentralized reputation system (e.g., marriage record, birth certificate, college degree)
  - ***Utility***: A token can be used to access or pay for a service.
## **Tokens and fungibility**
- fungible = directly exchangeable for money
- Tokens are fungible when we can **substitute** any single **unit of the token** for **another** **without any difference** in its value or function.
- The ability to track provenance can lead to blacklisting and whitelisting, reducing or eliminating fungibility.
- Non-fungible tokens are tokens that each represent a unique tangible or intangible item and therefore are not interchangeable
- Each non-fungible token is associated with a unique identifier, such as a serial number.

## **Counterparty Risk**
- The risk that the other party in a transaction will fail to meet their obligations
-  In general, when an asset is traded indirectly through the exchange of a token of ownership, there is additional counterparty risk from the custodian of the asset

## **Tokens and Intrinsicality**
- Some tokens representing digital items that are intrinsic to the blockchain are governed by consensus rules.
- Tokens that represent intrinsic assets do not carry additional counterparty risk
- Many tokens are used to represent *extrinsic* things which are governed by law, custom, and policy and depend on real-world non-smart contract.
- One of the most important ramifications of blockchain-based tokens is the ability to convert extrinsic assets into intrinsic assets and thereby remove counterparty risk

## **Using Tokens: Utility or Equity**
- The use of tokens can be seen as the ultimate management or organization tool.
- Utility tokens are those where the use of the token is **required to gain access** to a service, application, or resource
- Equity tokens are those that represent **shares in the control or ownership of something**, such as a startup

### **Utility Tokens: Who Needs Them?**
- The real problem is that utility tokens introduce significant risks and adoption barriers for startups
- The underlying reason for the insignificant value of most tokens is because they can only be used in a very narrow context: when you add a utility token to your platform, but the token can only be used on your single platform with a small market, you are recreating the conditions that made physical tokens worthless
- Adopt a token because your application cannot work without a token. Adopt it because the token lifts a fundamental market barrier or solves an access problem.

## **Tokens on Ethereum**
- Blockchain tokens existed before Ethereum (Bitcoin is a token). However, the introduction of the first token standard on Ethereum led to an explosion of tokens.
- Tokens are different from ether because the Ethereum protocol does not know anything about them
  - Sending ether is an intrinsic action of the Ethereum platform, but sending or even owning tokens is not
  - The ether balance of Ethereum accounts is handled at the protocol level, whereas the token balance of Ethereum accounts is handled at the smart contract level

## **Using Token Standards**
### **What Are Token Standards? What Is Their Purpose?**
- Token standards are the *minimum* specifications for an implementation. You are *free* to add to the functionality by implementing functions that are not part of the standard.
- Purpose: encourage *interoperability* between contracts
- The standards are meant to be *descriptive*, rather than *prescriptive*. How you choose to implement those functions is up to you—the internal functioning of the contract is not relevant to the standard. 

### **Should You Use These Standards?**
- This dilemma is not easy to resolve: 
  - Standards necessarily restrict your ability to innovate
  - The basic standards have emerged from experience with hundreds of applications and often fit well with the vast majority of use cases.
- Value of all the systems designed or the cost of building all of the support infrastructure

### **Security by Maturity**
- There are a number of existing "reference" implementations that are widely used in the Ethereum ecosystem, or you could write your own from scratch, which can have serious security implications.
- It is much safer to use a well-tested, widely used implementation
- If you use an existing implementation you can also extend it. Again, however, be careful with this impulse

### **Extensions to Token Interface Standards**
- Many projects have created extended implementations to support features that they need for their applications. Some of these features include:
  - ***Owner control***: The ability to give specific addresses, or sets of addresses (i.e., multisignature schemes), special capabilities, such as blacklisting, whitelisting, minting, recovery, etc.
  - ***Burning***: The ability to deliberately destroy (“burn”) tokens by transferring them to an unspendable address or by erasing a balance and reducing the supply.
  - ***Minting***: The ability to add to the total supply of tokens, at a predictable rate or by "fiat" of the creator of the token.
  - ***Crowdfunding***: The ability to offer tokens for sale, for example through an auction, market sale, reverse auction, etc.
  - ***Caps***: The ability to set predefined and immutable limits on the total supply (the opposite of the "minting" feature).
  - ***Recovery backdoors***: Functions to recover funds, reverse transfers, or dismantle the token that can be activated by a designated address or set of addresses.
  - ***Whitelisting***: The ability to restrict actions (such as token transfers) to specific addresses. Most commonly used to offer tokens to "accredited investors" after vetting by the rules of different jurisdictions. There is usually a mechanism for updating the whitelist.
  - ***Blacklisting***: The ability to restrict token transfers by disallowing specific addresses. There is usually a function for updating the blacklist.
## **Tokens and ICOs**
- Tokens have been an explosive development in the Ethereum ecosystem
- Nevertheless, the importance and future impact of these standards should not be confused with an endorsement of current token offerings.


 



