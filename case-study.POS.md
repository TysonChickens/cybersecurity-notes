---
id: kea71p9fdhj064izld79e2v
title: POS
desc: ''
updated: 1653198789525
created: 1653198757372
---

# Point of Sale Breach Overview

- [ ] Learn what a Point of Sale (PoS) breach is.
- [ ] Learn about PoS systems and their security standards.

- [ ] Learn how malware makes its way onto PoS devices.
- [ ] Learn about the different families of PoS malware.
- [ ] Learn what happens to the stolen information.

- [ ] Understand the timeline of events of the Point of Sale (POS) attack.
- [ ] Learn about what actions were taken by the threat actors.
- [ ] Learn what the impacts are from a POS attack.
---

[The main objective of point of sale (POS) breaches is to steal your 16-digit credit card numbers. Sixty percent of Point of Sale (POS) transactions are performed via credit card, which means big business for cyber-criminals (individual credit cards can be sold for up to 100 dollars apiece). The industries most affected by POS data breaches are usually restaurants, retail stores, grocery stores and hotels. The mainstream media tends to cover stories when the big brand retailers fall victim to these attacks, but data breaches actually happen more frequently to small and medium sized businesses because they are easier to compromise than the computer networks of large retailers. - Norton Internet Security](https://us.norton.com/internetsecurity-id-theft-pos-malware-data-breaches-and-why-they-keep-happening.html)

## Point of Sale

[The term Point of Sale (POS) is used to describe the technology used by a consumer to provide their payment information in exchange for a good or service. POS technology has actually been around for many years with the first cash register dating back to 1879 (Abell, 2009). However, it wasn't until the mid-70s that this technology was converted from a mechanical to an electrical form. - Wes Whitteker, 2014](https://www.giac.org/paper/gsec/35318/point-sale-pos-systems-security/121485)

## PoS Security

The Payment Card Industry Data Security Standard (PCI DSS) is the main payment card industry information security standard. It was created in 2006 by the PCI security standards council (SSC).

- Led by American Express, Discover Financial Services, JCB International, MasterCard, and Visa Inc.
- The goal is to protect cardholder data and sensitive authentication data wherever it is processed, stored or transmitted.

### PCI DSS - Security Controls & Processes for PCI DSS Requirements

Merchants, service providers, and other entities involved with payment card processing must never store sensitive authentication data after authorization.

This includes the 3-or 4-digit security code printed on the front or back of a card, the data stored on a card's magnetic stripe or chip (also called Full Track Data) - and personal identification numbers (PIN) entered by the cardholder.

1. Build and maintain a secure network and systems.
2. Protect cardholder data.
3. Maintain a vulnerability management program.
4. Implement a strong access control measures.
5. Regularly monitor and test networks.
6. Maintain an information security policy.

#### Requirements

- Install and maintain a firewall configuration to protect cardholder data.
- Do not use vendor-supplied defaults for system passwords and other security parameters.
- Protect stored card cardholder data.
- Encrypt transmission of cardholder data across open, public networks.
- Use and regularly update antivirus software.
- Develop and maintain secure systems and applications.
- Restrict access to cardholder data by business need-to-know.
- Assign a unique ID to each person with computer access.
- Restrict physical access to cardholder data.
- Track and monitor all access to network resources and cardholder data.
- Regularly test security systems and processes.
- Maintain a policy that addresses information security.

#### Compliance is Not Enough

[In 2018, cyber attacks increased by 32 percent in the first few months of the year compared to the same period in 2017.  Threats from criminals are constantly evolving and becoming more sophisticated. Being only PCI Compliant is not enough, and businesses need to take additional security measures to protect sensitive cardholder data and their payment technology investment. Here are a few ways businesses can protect their payment infrastructure:](https://blog.ingenico.us/blog/why-pci-compliance-isnt-enough)

Semi-Integrated Payment Approach
: Reduces the communication between the terminal and the electronic cash register (ECR) to non-sensitive commands. Sensitive data is isolated, encrypted and directly sent from the terminal to the intended processing hosts or gateway.

Point-to-Point Encryption (P2PE)
: Helps protect card data while it is on the move during the payment process.

Tokenization
: Helps protect the card data at rest. It replaces the sensitive information with a secure encrypted token protecting from cyber criminals when the data is at rest.

- Current PCI standards do not allow businesses to save and store credit card details unless tokenized on PoS systems or databases after the transaction.

Mobile Device Management (MDM)
: Many businesses use consumer-grade mobile devices to work with their POS systems. MDM is a type of security that allows businesses to remotely deploy and securely manage their mobile POS solutions.

Employee Education
: Effective training of employees to be aware of possibilities regarding basic security protocols to prevent mistakes and protect business of threats.

## PoS Malware

[PoS systems require some sort of connection to a network in order to contact external credit card processors. This is necessary in order to validate credit card transactions. How this connection is provided may depend on the store in question. For small businesses, this may be provided via a cellular data connection. Sufficiently skilled and determined attackers can thus go after a business’s PoS terminals on a large scale and compromise the credit cards of thousands of users at a time. The same network connectivity can also be leveraged to help exfiltrate any stolen information.](http://www.trendmicro.com.ph/cloud-content/us/pdfs/security-intelligence/white-papers/wp-pos-system-breaches.pdf)

- PoS malware specifically target the RAM to steal the un-encrypted information - a process called 'RAM scraping'.
- Industry uses end-to-end encryption of sensitive payment data - which comes from the card's magnetic strip or chip - when it is transmitted, received or stored. Decryption only occurs in the PoS device's random-access memory (RAM), where it is processed.
  - Most PoS run on Windows or Linux, making them small computers.
  - Once inside, the PoS malware can select which data to steal and upload to a remote server... most PoS malware come equipped with backdoor and command-and-control features.

### Types of Malware

PoS malware is rarely used without the aid of other malware. These are the most common and readily available families of PoS malware.

Alina
: Scans the system's memory to check if the contents match regular expressions, which indicate the presence of card information that can be stolen.

vSkimmer
: If it does not find its server, it checks for the presence of a removable drive with the label 'KARTOXA007'. If this drive is found, it drops a file that contains any stolen information into it, allowing a method of offline data exfiltration.

Dexter
: Steals various system information and installs a key-logger onto affected systems.

FYSNA
: Using the Tor network to communicate with its C&C server makes detection and investigation difficult by masking all of the network traffic made by the malware extremely difficult to analyze.

Decebel
: Checks if sand-boxing or analysis tools are present on a machine before running. This allows to make detection and analysis more difficult.

BlackPOS
: Uses FTP to upload information to a server of the attackers' choosing. Allows attackers to consolidate stolen data from multiple PoS terminals on a single server.

### Where is the Data?

Criminals sell the info to brokers who buy the payment card information in bulk and sell the information to 'carders' who use a carder website to obtain payment information which they will purchase pre-paid credit cards with.

- Those credit cards will be used to buy gift cards, which are used to buy goods and sell for profit. The items are shipped to a re-shipper, making the transaction from end to end very difficult to follow.

## Best Prevention Practices

- Actively monitor POS network for changes.
- Using compliant, best-of-class, end-to-end encryption around cardholder data.
- Limiting the hosts that can communicate with POS systems.
- Adopting chip-card enabled POS terminals.
- Utilizing employee screening and training to minimize insider threats.
- Training employees to immediately detect and report possible signs of tampering.

## Case Study - Home Depot

- The attack was completed using stolen credentials from one of the retailer's vendors.
- Those credentials were used to obtain access to the network, privileges elevated and access to POS systems to record credit card details.
- The malware infection went unnoticed for 5 months between April and September 2014.

### Timeline

1. Stolen credentials were used to obtain access to the network...
2. Privileges were subsequently elevated.
3. Access to the POS system was obtained and malware was downloaded to record credit card details.
4. The malware infection went unnoticed for five months between April and September 2014.
5. Home Depot began an investigation on September 2nd.
6. On September 8th, 2014, Home Depot released a statement indicating that its payment card systems were breached.

### Vulnerabilities

The attackers exploited a zero-day vulnerability in Windows, which allowed them to pivot from the vendor-specific environment to the Home Depot corporate environment.

- Lack of regularly scheduled scan
- Did not have proper configuration of the software, or hardware POS terminals and the lack of network segregation.
- Credentials were not properly managed.
- Lack of monitoring capabilities led to a 5 month delay.

### Cost

- 56 million payment cards stolen.
- $19.5 million payout to customers that had been impacted by the breach, including credit monitoring services.
- A minimum of $134.5 million to credit card companies and banks.
- The total cost of the retail data breach is approximately $179 million, not including legal fees.
- Expected total cost is close to $200 million.

### Prevention

- Chip-and-PIN card is embedded with security chip in addition to the traditional mag-stripe.
- Vendors began promoting an alternative method to payment cards using mobile payment methods, like Apple Pay and Google Wallet.
- Additional security was also provided by point-to-point (P2P) encryption.
  - Risk still remains with P2P encryption if someone to install a credit card skimmer on the actual pin-pad - which is still occurring.
