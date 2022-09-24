# Active Directory Basics

Microsoft's Active Directory is the backbone of the corporate world to simplify the management of devices and users within a corporate environment.

Become familiar with Active Directory basic topics:

* What is Active Directory?
* What is Active Directory Domain?
  * What components go into an Active Directory Domain?
* What are Forests and Domain Trusts?

## Windows Domains

A **Windows** **domain** is a group of users and computers under the administration of a given business. The main goal behind a domain is to centralize the administration of common components of a Windows computer network in a single repository called **Active Directory (AD).** The server that runs the Active Directory services is known as **Domain Controller (DC)**.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/bebe5dfec0208bf563d01fa2dd1fb7a7.png" alt=""><figcaption><p>Domain</p></figcaption></figure>

The main advantages of having a configured Windows domain are:

* **Centralized Identity Management**: All users across the network can be configured from Active Directory with minimum effort.
* **Managing security policies**: Can configure security policies directly from Active Directory and apply them to users and computers across the network as needed.

### Real-World Example

In school/university networks, there will be a provided username and password that can be used on any of the computers available on the campus.

* Credentials are valid for all machines because of the forward authentication process back to the Active Directory to be verified. They do not need to exist in each machine and are available throughout the network.
* Active Directory is also the component that allows school/university/workplace to restrict access with policies.
  * Policies will be deployed throughout the network to prevent administrative privileges over those computers.

## Active Directory

The core of any Windows Domain is the **Active Directory Domain Server (AD DS).** This service acts  as a catalog that holds the information of all the 'objects' supported by the AD.

The objects supported by the AD, there are users, groups, machines, printers, shares and many others.

### Users

Users are one of the most common object types in Active Directory. Users are known as **security principals**, meaning they can be authenticated by the domain and can be assigned privileges over **resources** like files or printers.

Users can be used to represent two types of entities:

* **People:** Users will generally represent individuals in the organization that need access to the network, like employees.
* **Services**: Can define users to be used by services like IIS or MSSQL. Every single service requires a user to run.
  * Service users are different from regular users as they will only have the privileges needed to run their specific service.

### Machines

Machines are another type of objective within Active Directory; for every computer that joins the Active Directory domain, a machine object will be created.

* Machines are also considered "security principals" and are assigned an account as a regular user.
* Machine accounts are local administrators on the assigned computer and generally not supposed to be accessed by anyone except the computer itself.
  * As with any other account, if you have the password, you can use it to log in.
  * Machine account passwords are automatically rotated out and are comprised of 120 random characters.

Identifying machine accounts is relatively easy. They follow a specific naming scheme with the computer's name followed by a dollar sign.

* For example, a machine named `DC01` will have a machine account called `DC01$`.

### Security Groups

If you are familiar with Windows, it is possible to define user groups to assign access rights to files or other resources to entire groups instead of single users. This allows for better manageability when adding  new users to an existing group, and they will automatically inherit all of the group's privilege.

* Security groups are also considered security principals, therefore, can have privileges over resources on the network.

Groups can have both users and machines as members. If needed, groups can include other groups as well.

| Security Group     | Description                                                                                                                                   |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Domain Admins      | Users of this group have administrative privileges over the entire domain. They can administer any computer on the domain, including the DCs. |
| Server Operators   | Users in this group can administer Domain Controllers. They cannot change any administrative group memberships.                               |
| Backup Operators   | Users are allowed to access any file, ignoring their permissions. They are used to perform backups of data on computers.                      |
| Account Operators  | Users in this group can create or modify other accounts in the domain.                                                                        |
| Domain Users       | Includes all existing user accounts in the domain.                                                                                            |
| Domain Computers   | Includes all existing computers in the domain.                                                                                                |
| Domain Controllers | Includes all existing DCs on the domain.                                                                                                      |

A complete list of default security groups from the [Microsoft documentation.](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-groups)

### Users and Computers

To configure users, groups or machines in Active Directory, need to log in to the Domain Controller and run "Active Directory Users and Computers" from the start menu:

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/11d01963392078c1450300d2881f9160.png" alt=""><figcaption></figcaption></figure>

The window will display a hierarchy of users, computers and groups that exist in the domain. These objects are organized in **Organizational Units (OUs)** which are container objects that allow to classify users and machines.

* Organizational Units are mainly used to define sets of users with similar policing requirements for different parts of the organization.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/c5b1d321108bc065771eba62d24f5e83.png" alt=""><figcaption></figcaption></figure>

* There is an OU called THM with 4 child OUs for IT, Management, Marketing and Sale departments.

There are other default containers apart from the THM OU. These containers are created by Windows automatically and contain the following:

* **Builtin**: Contains default groups available to any Windows host.
* **Computers**: Any machine joining the network will be put here by default.
* **Domain Controllers**: Default OU that contains the DCs in the network.
* **Managed Service Accounts**: Holds accounts used by services in the Windows domain.

### Security Groups vs OUs

Both are used to classify users and computers, their purposes are entirely different.

* **OUs** are for **applying policies** to users and computers, which include specific configurations that pertain to sets of users depending on their particular role in the enterprise.
  * A user can only be a member of a single OU at a time since it would not make sense to apply two different sets of policies to a single user.
* **Security groups** are used to **grant permissions over resources** such as a shared folder or network printer.

### Managing Users

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/88f0ade5a672ae681639e6049406a4ec.png" alt=""><figcaption><p>Organizational chart</p></figcaption></figure>

Given the following organizational chart and are expected to make changes to the AD to match it.

#### Deleting Extra OUs and Users

By default, OUs are protected against accidental deletion. To delete the OU, we need to enable **Advanced Features** in the View menu:

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/15b282b6e3940f4c26c477a8c21f8266.png" alt=""><figcaption></figcaption></figure>

#### Delegation

Active Directory can give specific users some control over some OUs. This process is known as **delegation** and allows to grant users specific privileges to perform advanced tasks on OUs without needing a Domain Administrator to step in.

The most common use cases for this is granting _IT support_ the privileges to reset over low-privilege users' passwords.

#### Managing Computers

By default, all the machines that join a domain (except for the DCs) will be put in the container called "Computers". There is no golden rule on how to organize machines but expect to see devices divided into at least the following categories:

* **Workstations** are one of the most common devices within an Active Directory domain. Each user in the domain will likely be logging into a workstation. This is a device for daily work or normal browsing activities. These devices should never have a privileged user signed into them.
* **Servers** are second most common device within an Active Directory domain. Servers are generally used to provide services to users or other servers.
* **Domain Controllers** are the third most common device within an Active Directory domain. Domain controllers allow to manage the Active Directory domain. These devices are the most sensitive devices within the network as they contain hashed passwords for all user accounts within the environment.

## Group Policies

Windows manages policies through **Group Policy Objects (GPO)**. GPOs are a collection of settings that can be applied to OUs.

* GPOs can contain policies aimed at either users or computers, allowing to set a baseline on specific machines and identities.
* Use the **Group Policy Management** tool from the start menu to configure GPOs.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/d82cb9440894c831f6f3d58a2b0538ed.png" alt=""><figcaption><p>Group Policy Objects</p></figcaption></figure>

The _Default Domain Policy_ indicates basic configurations that should apply to most domains, including password and account lockout policies. Since GPO applies to the whole domain, any change to it would affect all computers.

There are many policies that can be established in a GPO. It is possible to double-click policies and read the **Explain** tab on each of them.

### GPO Distribution

GPOs are distributed to the network via a network share called `SYSVOL`, which is stored in the DC. All users in the domain should have access to this over the network to sync their GPOs periodically.

* The SYSVOL share points by default to the `C:\Windows\SYSVOL\sysvol\` directory on each of the DCs in the network.
* Once a change has been made to any GPO, it might take up to 2 hours for computers to catch up.
  * Can force any computer to sync its GPO immediately on the desired computer with `gpupdate /force`

