---
id: 5vhy4yxl34a7p6064a13u49
title: SQL-Injection
desc: ''
updated: 1657832605769
created: 1657403199233
---

# What is SQL?

SQL (Structured Query Language) Injection, mostly referred to as SQLi, is an attack on a web application database server that causes malicious queries to be executed.

- When a web application communicates with a database using input from a user that has not been properly validated, there is potential of an attacker being able to steal, delete or alter private and customer data.

## What is a Database?

A database is a way of electronically storing collections of data in an organized manner. A database is controlled by a DBMS (Database Management System) and is **Relational** or **Non-Relational**.

![database](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/f31d5855476c01e8359df000da4ac79d.png)

Within a DBMS, you can have multiple databases, each containing its own set of related data.

- A database called 'shop' to store information about products available to purchase, users who signed up, and information about the orders received. This information is stored as tables and each are identified with a unique name.

### What is a Table?

A table is made up of columns and rows. A table is like a grid with the columns going across the top from left to right containing the name of the cell and the rows going from top to bottom with each one having data.

![table](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/cee2844345f5ab5bc704b163797b3604.png)

**Columns:** Referred to as a field has a unique name per table. When creating a column, the type of data could be set as integer (numbers), strings (standard text) or dates. Some databases can contain much more complex data, such as geo location data.

- Setting the data type also ensures that incorrect information is not stored, such as the string "hello world" being stored in a column meant for dates. If this happens, an error message is produced.
- Each row of data create a key field that has to be unique for every row of data which can be used to find that exact row in SQL queries.

**Rows**: Rows or records are what contains the individual lines of data. When adding data to the table, a new row/record is created and removed when data is deleted.

### Relational vs Non-Relational Databases

A relational database, stores information in tables and have shared information between them - Columns are used to specify and define the data being stored and rows to store the data.

- The tables often contain a column with a unique ID (primary key) which is then used in other tables to reference it and cause a relationship between the tables.

Non-relational databases sometimes called NoSQL is any database that does not use tables, columns and rows to store the data - Specific database layout does not need to be constructed so each row of data can contain different information which can provide more flexibility over a relational database.

- Popular non-relational databases are MongoDB, Cassandra and ElasticSearch.

## What is SQL Injection?

The point where a web application using SQL can turn into SQL Injection is when user-provided data gets included in the SQL query.

In the following scenario, the blog entries may be either set to public or private depending on whether they are ready for public release. The URL for each blog entry may look like something: `https://website.thm/blog?id=1`

From the URL, the blog entry has been selected comes from the id parameter in the query string. The web application needs to retrieve the article from the database and may use an SQL statement that looks something like: `SELECT * from blog where id=1 and private=0 LIMIT 1;`

Now pretend article id 2 is still locked as private, so it cannot be viewed on the website: `https://website.thm/blog?id=2;--`

- The SQL statement would be `SELECT * from blog where id=2 and private=0 LIMIT 1;`
- The semicolon in the URL signifies the end of the SQL statement, and the two dashes cause everything afterwards to be treated as comment (`SELECT * from blog where id=2;--`).
  - This will return the article with an id of 2 whether it is set to public or not.
- This is one example of an SQL Injection vulnerability of a type called In-Band SQL Injection.
  - There are 3 types in total: In-Band, Blind and Out of Band.

## In-Band SQL Injection

In-Band SQL injection is the easiest type to detect and exploit; In-Band refers to the same method of communication being used to exploit the vulnerability and also receive the results. For example, discovering an SQL Injection vulnerability on a website page and then being able to extract data from the database to the same page.

**Error-Based SQL Injection**: Type of injection is the most useful for easily obtaining information about the database structure as error messages from the database are printed directly to the browser screen.

**Union-Based SQL Injection**: Utilizes the SQL UNION operator alongside a SELECT statement to return additional results to the page. This method is the most common way of extracting large amounts of data via an SQL Injection vulnerability.

## Out-of-Band SQLi

Is not as common as it depends on specific features being enabled on the database server or the web application's business logic.

An Out-of-Band attack is classified by having two different communication channels with one to launch an attack and the other to gather the results. For example, the attack channel could be a web request, and the data gathering channel could be monitoring HTTP/DNS requests made to a service you control.

1. An attacker makes a request to a website vulnerable to SQL Injection with an injection payload.
2. The website makes an SQL query to the database which also passes the hacker's payload.
3. The payload contains a request which forces an HTTP request back to the hacker's machine containing data from the database.

## Remediation

Developers have a way to protect their web applications from them by following the below advice:

- **Prepared Statements (With parameterized queries)**: The developer writes the SQL query and then any user inputs are added as a parameter afterwards. Writing prepared statements ensures that the SQL code structure does not change and the database can distinguish between the query and the data.
- **Input Validation**: Employing an allow list can restrict input to only certain strings, or a string replacement method in the programming language can filter the characters to allow or disallow.
- **Escaping User Input**: Method of pre-pending a backslash (\) to these characters, which then causes them to be parsed just as a regular string and not a special character.