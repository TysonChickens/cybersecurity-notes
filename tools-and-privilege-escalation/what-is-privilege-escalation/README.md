---
description: Privilege escalation is a journey. There is no magic bullet.
---

# What is Privilege Escalation?

Involves moving from a lower permission to a higher permission level. Technically, it is the exploitation of vulnerability, design flaw or configuration oversight in an operating system or application to gain unauthorized access to resources that are usually restricted from the users.

Rarely during CTF or real-world penetration test, will be able to gain initial access that affords administrator access. Privilege escalation allows to gain system administrator levels of access to:

* Reset passwords
* Bypass access controls to compromise protected data
* Edit software configurations
* Enable persistence to gain access to the machine later
* Change privilege of users
* And other administrator or super user commands...

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/603df7900d7b6f1dff18b0bd/room-content/2e51bfc8489168a3f6580dc76b46ba90.png" alt="user to super admin"><figcaption><p>From user to super admin privilege escalation.</p></figcaption></figure>

## Direction of Privilege Escalation

![privilege tree](https://github.com/TheRealPoloMints/Blog/blob/master/Security%20Challenge%20Walkthroughs/Common%20Linux%20Privesc/Resources/tree.png?raw=true)

There are two main privilege escalation variants:

### Horizontal Privilege Escalation

* Expand reach over the compromised system by taking over a different user who is on the same privilege level.
  * Hijack a normal user to inherit files and access the user has.
  * Can be used to access another normal privilege user that haves their SUID file attached to their home directory which can then be used to get super user access (travel sideways on the tree).

### Vertical Privilege Escalation

* Attempt to gain higher privileges or access, with an existing account that is already compromised.
* For local privilege escalation attacks, this might mean hijacking an account with administrator privileges or root privileges (travel up on the tree).
