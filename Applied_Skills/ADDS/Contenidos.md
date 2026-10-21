# Administer Active Directory Domain Services

## Deploy and manage Active Directory Domain Services domain controllers

Topology of domain controllers within an Active Directory environment.

Deploying, managing, and migrating a domain controller between servers.

### Introduction
### Define Active Directory Domain Services

The AD DS database is the central store of all the domain objects, such as user accounts, computer accounts, and groups. AD DS provides a searchable, hierarchical directory and a method for applying configuration and security settings for objects in an enterprise.

AD DS includes logical and physical components. You should understand how AD DS components work together so that you can manage your infrastructure efficiently. In addition, you can use AD DS options to perform actions such as:

- Installing, configuring, and updating apps.
- Managing the security infrastructure.
- Enabling Remote Access Service and DirectAccess.
- Issuing and managing digital certificates.

AD DS logical components are structures that you use to implement an AD DS design that is appropriate for an organization. 
- A partition, or naming context, is a portion of the AD DS database. Although the database consists of one file named Ntds.dit, different partitions contain different data. For example, the schema partition contains a copy of the Active Directory schema. The configuration partition contains the configuration objects for the forest, and the domain partition contains the users, computers, groups, and other objects specific to the domain. Active Directory stores copies of partitions on multiple domain controllers and updates them through directory replication.
- A schema is the set of definitions of the object types and attributes that you use to define the objects created in AD DS.
- A domain is a logical administrative container for objects such as users and computers. A domain maps to a specific partition and you can organize the domain with parent-child relationships to other domains.

