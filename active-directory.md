---
id: ce290z98noyy6eb5pniawk9
title: Active Directory
desc: ''
updated: 1654385500186
created: 1654210284561
---

A directory service for Windows Domain Networks used by many companies.

## What is Active Directory?

Active Directory
: A collection of machines and servers connected inside of domains, that are a collective part of bigger forest of domains, make up the Active Directory network.

- Domain Controllers
- Forests, Trees, Domains
- Users + Groups
- Trusts
- Policies
- Domain Services

All these parts of Active Directory make up a big network of machines and servers.

### Why Use Active Directory?

Many large companies use Active Directory because it allows for the control and monitoring of the user's computers through a single domain controller. Allows for any user in the company to use any machine that the company owns, without having to set up multiple users on a machine.

#### Physical Active Directory

- Servers and machines on-premises or anything from domain controllers and storage to user machines.

Domain Controllers
: A Windows server that has Active Directory Domain Services (AD DS) installed and has been promoted to a domain controller in the forest.

- Holds the AD DS data store
- Handles the authentication and authorization services
- Replicate updates from other domain controllers in the forest
- Allows admin access to manage domain resources

#### AD DS Data Store

Active Directory Data Store
: Holds the databases and processes needed to store and manage directory information such as users, groups, and services.

- Contains the NTDS.dit - a database that contains all of the information of an Active Directory domain controller as well as password hashes for domain users.
- Stored by default in %SystemRoot%\NTDS
- Accessible only by the domain controller

## The Forest

Defines everything; it is the container that holds all of the other bits and pieces of the network together - without the forest, all the other trees and domains would not be able to interact.

- The "forest" is to describe the connection created between these trees and domains by the network.
  - A collection of one or more domain trees inside of an Active Directory network:
    - **Trees** - Hierarchy of domains in Active Directory Domain Services
    - **Domains** - Used to group and manage objects
    - **Organizational Units (OUs)** - Containers for groups, computers, users, printers and other OUs
    - **Trusts** - Allows user to access resources in other domains
    - **Objects** - Users, groups, printers, computers, shares
    - **Domain Services** - DNS server, LLMNR, IPv6
    - **Domain Schema** - Rules for object creation

## Users + Groups

Users and groups are inside of an Active Directory. When a domain controller is created, has default groups and two default users: Administrator and guest.

### Users

Users are the main component to Active Directory. There are four main types of users and there could be more depending on the permissions of its users:

- **Domain Admins** - Control the domains and only access to the domain controller
- **Service Accounts** (can be Domain Admins) - Required by Windows for services such as SQL to pair a service with a service account
- **Local Administrators** - These users can make changes to local machines as an administrator but cannot access the domain controller
- **Domain Users** - Everyday users in the organization

### Groups

Groups make it easier to give permissions to users and objects by organizing them into groups with specified permissions. 

- **Security Groups** - Used to specify permissions for a large number of users.
- **Distribution Groups** - Used to specify email distribution lists.

#### Default Security Groups

**Domain Controllers**
: All domain controllers in the domain

**Domain Guests**
: All domain guests

**Domain Users**
: All domain users

**Domain Computers**
: All workstations and servers joined to the domain

**Domain Admins**
: Designated administrators of the domain

**Enterprise Admins**
: Designated administrators of the enterprise

**Schema Admins**
: Designated administrators of the schema

**DNS Admins**
: DNS administrators of the group

**DNS Update Proxy**
: DNS clients who are permitted to perform dynamic updates on behalf of some other clients (such as DHCP servers)

**Allowed RODC Password Replication Group**
: Members in this group can have their passwords replicated to all read-only domain controllers in the domain

**Group Policy Creator Owners**
: Members can modify group policy for the domain

**Denied RODC Password Replication Group**
: Members cannot have their passwords replicated to any read-only domain controllers

**Protected Users**
: Members are afforded additional protections against authentication security threats

**Cert Publishers**
: Members are permitted to publish certificates to the directory

**Read-Only Domain Controllers**
: Members are Read-Only Domain Controllers in the domain

**Enterprise Read-Only Domain Controllers**
: Members are Read-Only Domain Controllers in the enterprise

**Key Admins**
: Members can perform administrative actions on key objects within the domain

**Enterprise Key Admins**
: Members can perform administrative actions on key objects within the forest

**Cloneable Domain Controllers**
: Members that are domain controllers may be cloned

**RAS and IAS Servers**
: Servers can access remote access properties of users

## Trusts + Policies

Help the domain and trees communicate with each other and maintain 'security' inside of the network.

### Domain Trusts

Trusts are mechanisms in place for users in the network to gain access to other resources in the domain. Trusts outline how domains inside of a forest communicate to each other, and some can be extended to external domains and forests in some cases.

- **Directional** - The direction of the trust flows from a trusting domain to a trusted domain
- **Transitive** - Trust relationship expands beyond two domains to include other trusted domains

### Domain Policies

Policies dictate how the server updates and what rules it will and will not follow. They act as a rule book for Active Directory that a domain admin can modify and alter as necessary to keep the network running smoothly and securely.

- Disable Windows Defender - Disables windows defender across all machine on the domain
- Digitally Sign Communication (Always) - Disable or enable SMB signing on the domain controller

## Active Directory Domain Services + Authentication

The Active Directory domain services are the core functions of an Active Directory network.

They allow for management of the domain, security certificates, LDAPs, and much more.

### Domain Services

Services that the domain controller provides to the rest of the domain or tree. There is a wide range of various services that can be added to a domain controller.

The default domain services:

**LDAP** - Lightweight Directory Access Protocol provides communication between applications and directory services.

**Certificate Services** - Allows the domain controller to create, validate, and revoke public key certificates.

**DNS, LLMNR, NBT-NS** - Domain Name Services for identifying IP hostnames

### Domain Authentication

There are two types of main types of authentication in place for Active Directory: NTLM and Kerberos.

- **Kerberos** - The default authentication service for Active Directory uses ticket-granting tickets and service tickets to authenticate users and give users access to other resources across the domain.

**NTLM** - Default Windows authentication protocol uses an encrypted challenge/response protocol

The Active Directory domain services are the main access point for attackers and contain some of the most vulnerable protocols for Active Directory.

## Active Directory in the Cloud

Companies have been shifting Active Directory to cloud networks.

### Azure AD

Azure is the most notable cloud provider and its default settings are much more secure than an on-premise physical Active Directory network; however the cloud AD may still have vulnerabilities.

Azure acts as the middle man between physical Active Directory and users' sign on.

### Cloud Security

A comparison table with a cloud Active Directory environment and a physical network.


| Windows Server AD | Azure AD |
| ----------------- | -------- |
| LDAP                | Rest APIs
| NTLM                | OAuth/SAML      
| Kerberos            | OpenID     
| OU Tree             | Flat Structure
| Domains and Forests | Tenants
| Trusts              | Guests

## Active Directory Commands

https://activedirectorypro.com/powershell-commands/

