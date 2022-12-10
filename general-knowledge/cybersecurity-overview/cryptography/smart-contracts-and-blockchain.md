# Smart Contracts & Blockchain

* Explain what smart contracts are, how they relate to the blockchain, and why they are important.
* Understand how contracts are related, what they are built upon, and standard core functions.
* Understand and exploit a common smart contract vulnerability.

## What is a Blockchain?

Historically, it has been used as a financial technology, and recently expanded into many other industries and applications. Informally, a blockchain acts as a database to store information in a specified format and is shared among members of a network with no one entity in control.

By definition, a blockchain is a digital database or ledger distributed among nodes of a peer-to-peer network. The blockchain is distributed among "peers" or members with no central servers (decentralized).

* The core blockchain technology aims to be decentralized and maintain integrity - Cryptography is employed to negotiate transactions and provide utility to the blockchain.
* Security concerns focus on how data is transferred and negotiated.

## Smart Contracts

Most applications of blockchain rely on a technology known as a smart contract.

* Smart contracts are most commonly used as the backbone of DeFi applications (Decentralized Finance) to support a cryptocurrency on a blockchain. DeFi applications faciliate exchange between entities; a smart contract defines the details of the exchange.

Smart contracts are comparable to any other program created from a scripting language.

* Solidity, Vyper, and Yul are some languages have been developed to faciliate the creation of contracts. Smart contracts can even be developed using traditional programming languages such as Rust and JavaScript and smart contracts wait for conditions and execute actions, similar to traditional logic.

### Functionality of a Smart Contract

A contract commonly has several functions that act similarly to accessors and mutators from object-oriented programming, such as checking balance, depositing, and withdrawing currency.

Once a contract is deployed on a blockchain, another contract can then use its functions to call or exeucte the functions.

#### Example

A scenario with Contract A and Contract B wanted to first deposit 1 Ethereum, and then withdraw 1 Ethereum from Contract A, Contract B calls the deposit function of Contract A.

Contract A authorizes the deposit after checking if any pre-determined conditions need to be met.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/7c206b5cd15dbb4ebd4d9dbbe420d905.png" alt=""><figcaption></figcaption></figure>

Contract B calls the withdraw function of Contract A -> authorizes the deposit if the pre-determined conditions for withdrawal are met.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/2a1e2111efdc9b545b1abac86ef792ca.png" alt=""><figcaption></figcaption></figure>

Contract B can execute other functions after the Ether is sent from Contract A but before the function resolves.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/667fe1f786b635b1153973a4a7c8703a.png" alt=""><figcaption></figcaption></figure>

### Vulnerabilities in Smart Contracts

Most smart contract vulnerabilities arise due to logic issues or poor exception handling. Most vulnerabilities in functions when conditions are insecurely implemented through previously mentioned issues.

In the example, the conditions of the withdraw functions are:

* Balance is greater than zero.
* Send Ethereum.

The function should finish before the contract can process any other functions. A contract can consecutively make new calls to a function while an old function is still executing.&#x20;

* An attacker can continuously attempt to call the withdraw function before it can clear the balance meaning the pre-defined conditions will always be met. A developer must modify the function's logic to remove the balance before another call  can be made or require stricter requirements to be met.

#### Re-entrancy Attack

A common vulnerability known as re-entrancy - Occurs when a malicious contract uses a fallback function to continue depleting a contract's total balance due to flawed logic after an initial withdraw function occurs.

Assume Contract B is the attacking contract and Contract A is the storage contract. Contract B will execute a function to deposit, then withdraw at least one Ether. This process is required to initiate the withdraw function's response.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/5f3c424d4d6fb10d1c375649d30c7035.png" alt=""><figcaption></figcaption></figure>

The storage contract separates balances per account and keeps each account's total balance combined.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/c3a7d046821759f5237be1f1faab186e.png" alt=""><figcaption></figcaption></figure>

At this point, contract B can either drop the response from the withdraw function or invoke a fallback function. A fallback function is a reserved function in Solidity that can appear once in a single contract.

* The function is executed when currency is sent with no other context or data. The fallback function calls the withdraw function again, while the original call to the function was never fully restored.
  * Remember, the balance is never set back to zero, and the contract thinks of Ether as its total balance when sending it, not divided into each account, so it will continue to send currency beyond the account's balance until the total balance is zero.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/2f6c70c60729404d5a404de2c409a5a7.png" alt=""><figcaption></figcaption></figure>

Since the withdraw function sends Ether with no context or data, the fallback function will be called again, and an infinite loop can now occur.
