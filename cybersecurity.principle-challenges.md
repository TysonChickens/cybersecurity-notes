---
id: 98ah8km7auraq0qhcmdofsl
title: Principle Challenges
desc: ''
updated: 1658623966136
created: 1653033066587
---

# Cybersecurity - A Security Architect's Perspective

- [ ] Describe who are the primary actors in cyber crime and what are the motives of each.

- [ ] Describe why comprehensive cybersecurity architecture can be very complex to implement in reality.
  - [ ] Translation of simple business requirements into technical specifications and deployment decisions can be very difficult.
  - [ ] The protection mechanism itself is subject to attack.
  - [ ] Protectors have to be right all the time. Attackers only have to be right once.

- [ ] Describe security mechanisms and what they include.

- [ ] Describe various Network Security Models.

- [ ] Describe how the destruction, corruption, modification, theft, removal, loss or disclosure of information or other resources and the interruption of service can constitute threats to the security of data or systems.

- [ ] Describe how an action taken by a human, with intent to violate security, constitutes an attack.

- [ ] Identify and classify the various forms of active and passive attacks.

---

- The principles of security:

  - *Confidentiality*: Only sender, intended receiver should 'understand' the message contents. Sender encrypts message and receiver decrypts message.
  
  - *Authentication*: Sender, receiver want to confirm identity of each other.
  
  - *Message Integrity*: Sender, receiver want to ensure message not altered (in transit, or afterwards) without detection.
  - *Access and Availability*: Services must be accessible and available to users.

- NIST definition of Computer Security:
  
  **The protection afforded to an automated information system in order to attain the applicable objectives of preserving the integrity, availability and confidentiality of information system resources, includes hardware, software, firmware, information/data, and telecommunications.**

---

## Additional Computer Security Challenges

- Security is not as simple as it seems.
  - Easy requirements, tough solutions.
- Solutions can be attacked themselves where security policy enforcement structures as the targets.
- Protection of enforcement structure can complicate solutions.
  - Solution itself can be easy, but complicated by protection.
- Security architectural decisions on what to do but where to take action?
- Key management is difficult solution.
- Protectors have to be right all the time and attackers just once to succeed.
- No one like security until its needed (seat belt philosophy).
- Security architectures require constant effort from strategic versus tactical perspectives.
- Security is often a decision after thought.
- Security is viewed as a burden in early development life cycle of a project and not integrated right away.

## Security Models

According the a security model, any system or piece of technology storing information is called an information system, which is how we will reference systems and deices.

Here are some popular and effective security models used to achieve the three elements of the CIA Triad.

### The Bell-LaPadula Model

- Used to achieve confidentiality.
- Assumptions that an organization's hierarchical structure it is used in, where everyone's responsibilities/roles are well-defined.
- Model works by granting access to pieces of data called objects on a strictly need to know basis.
  - Uses the rule "no write down, no read up".

| Advantages                                                                                      | Disadvantages                                                                                                        |
| ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Policies in the model can be replicated to real-life organizations hierarchies (and vice versa) | Even though a user may not have access to an object, they will know about its existence - so it is not confidential. |
| Simple to implement and understand, and has been proven to be successful                        | Relies on a large amount of trust within the organization.                                                           |

![Bell-LaPadula](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/0e6e5d9d80785fc287b4a67e1453b295.png)

The Bell LaPadula model is popular within organizations such as government and military. Members of the organizations are presumed to have already gone through a process called vetting. Vetting is a screening process where applicant's backgrounds are examined to establish the risk they pose to the organization. Therefore, applicants who are successfully vetted are assumed to be trustworthy.

### Biba Model

The Biba model is almost the equivalent of the Bell-LaPadula model but for the integrity of the CIA triad.

This model applies the rule to objects (data) and subjects (users) that can be summarized as "no write up, no read down". This rule means that subjects can create or write content to objects at or below their level but can only read the contents of objects above the subject's level.

| Advantages                                                                                                 | Disadvantages                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| Model is simple to implement                                                                               | There will be many levels of access and objects. Things can be easily overlooked when applying security controls.                                    |
| Resolves the limitations of the Bell-LaPadula model by addressing both confidentiality and data integrity. | Often results in delays within a business. For example, a doctor would not be able to read the notes made by a nurse in a hospital with this model. |

![biba](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/895ba351ef24ef6495d290222e49470e.png)

The Biba model is used in organization or situations where integrity is more important than confidentiality. For example, in software development, developers may only have access to the code that is necessary for their job. They may not need access to critical pieces of information such as databases, etc. 