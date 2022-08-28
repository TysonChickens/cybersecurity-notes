---
id: 32cujyc2fzndqns6719xs81
title: Web Applications
desc: ''
updated: 1656764728122
created: 1656566156592
---

# Introduction

Every person uses different programs on their computers. A web application is like a 'program' that we can use without installation as long we have a modern web browser, such as Firefox, Safari, or Chrome. Here are some examples of web applications:

- Web mail such as Tutanota, Protonmail, Outlook, and Gmail.
- Online office suites such as Microsoft Office 365 (Word, Excel, and PowerPoint), Google Drive (Docs, Sheets, and Slides), and Zoho Office (Writer, Sheet, and Show).
- Online shopping such as Amazon.com, AliExpress, and Etsy.
- Other examples include online banking, money transfer, weather forecast, and social media.

The idea of a web application is a program that is running on a remote server.

- A server refers to a computer system running continuously to 'serve' the clients.

Consider an online shopping applications that includes information about products, customers, and invoices. A database is used to store information in an organized way. A database server is responsible for many functions, including reading, searching, and writing to the database.

- Products database: Contains details about the products, such as name, images, specifications, and price.
- Customers database: Contains all details related to customers, such as name, address, email, and phone number.
- Sales database: Expect to see what each customer has purchased and how they paid.

![shop](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/9efb37af45d16b776ec3d6c6b9235c15.png)

Displays how a search for an item on an online shopping site works.

1. The user enters an item name or related keywords in the search field. The web browser sends the search keyword(s) to the online shopping web application.
2. The web applications queries (searches) the products database for submitted keywords.
3. The product database returns the search results matching the provided keywords to the web application.
4. The web application formats the results as a friendly web page and returns them to the user.

![user_perspective](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/7cd9405026eca43ed73206e6e10e6b4c.png)

The user's perspective will only see an elegant online shop where all the technical infrastructure is hidden.


Many companies offer bug bounty programs. A bug bounty program allows the company to offer a reward for anyone who discovers a security vulnerability (weakness) in the company’s systems.

## Security Risks

https://owasp.org/www-project-top-ten/

Expectations of an online shop to function can some times be attacked.

![functions](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/352114ac8da5f156f42aa551701323a2.png)

1. Log in at the website: The attacker can try to discover the password. The attacker would use a long list of passwords with an automated tool to test them against the login page.
2. Search for the product: The attacker can attempt to breach the system by adding specific characters and codes to the search term and return data it should not.
3. Provide payment details: The attacker would check if the payment details are sent in cleartext or using weak encryption. Encryption refers to making the data unreadable without knowing the secret key or password.

### Identification and Authentication Failure

- Allow the attacker to use brute force methods, i.e., try many passwords, usually using automated tools, to find valid login credentials.
- Allow user's to choose a weak password.
- Storing the users' passwords in plain text.

### Broken Access Control

Access control ensures that each user can only access files (documents, images, etc.) related to their role or work.

- Failing to apply the principle of the least privilege and giving users more access permissions than they need.
  - An online customer should be able to view prices of the items, but they should not be able to change them.
- Able to view or modify someone's account by using its unique identifier.
  - Do not want a bank client to be able to view the transactions of another client.
- Able to browse pages that require authentication (logging in) as an unauthenticated user.

### Injection

A vulnerability in the web application where the user can insert malicious code as part of their input.

- Lack of proper validation and sanitization of the user's input.

### Cryptographic Failures

Cryptography focuses on the processes of encryption and decryption of data. Encryption scrambles cleartext into cipher text, which should be gibberish to anyone who does not have the secret key to decrypt it. Encryption ensures that no one can read the data without knowing the secret key - Decryption converts the cipher text back into the original cleartext using the secret key.

- Sending sensitive data in clear text through HTTP instead of HTTPS.
- Relying on weak cryptographic algorithm.
- Using default or weak keys for cryptographic functions.

