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
- A domain tree is a hierarchical collection of domains that share a common root domain and a contiguous Domain Name System (DNS) namespace.
- A forest is a collection of one or more domains that have a common AD DS root, a common schema, and a common global catalog.
- An OU is a container object for users, groups, and computers that provides a framework for delegating administrative rights and administration by linking Group Policy Objects (GPOs).
- A container is an object that provides an organizational framework for use in AD DS. You can use the default containers, or you can create custom containers. You can't link GPOs to containers.

What are the physical components? Those objects that are tangible, or that describe tangible components in the real world.
- A domain controller contains a copy of the AD DS database. For most operations, each domain controller can process changes and replicate the changes to all the other domain controllers in the domain.
- A copy of the data store exists on each domain controller. The AD DS database uses Microsoft Jet database technology and stores the directory information in the Ntds.dit file and associated log files. The C:\Windows\NTDS folder stores these files by default.
- A global catalog server is a domain controller that hosts the global catalog, which is a partial, read-only copy of all the objects in a multiple-domain forest. A global catalog speeds up searches for objects that might be stored on domain controllers in a different domain in the forest.
- Read-only domain controller (RODC). An RODC is a special, read only installation of AD DS. RODCs are common in branch offices where physical security is not optimal, IT support is less advanced than in the main corporate centers, or line-of-business applications need to run on a domain controller.
- A site is a container for AD DS objects, such as computers and services that are specific to a physical location. This is in comparison to a domain, which represents the logical structure of objects, such as users and groups, in addition to computers.
- A subnet is a portion of the network IP addresses of an organization assigned to computers in a site. A site can have more than one subnet.

In addition to the high-level components and objects, AD DS contains other objects such as users, groups, and computers.

### Define Active Directory Domain Services forests and domains

An Active Directory Domain Services (AD DS) forest is a collection of one or more AD DS trees that contain one or more AD DS domains. Domains in a forest share:
- A common root.
- A common schema.
- A global catalog.
An AD DS domain is a logical administrative container for objects such as:
- Users
- Groups
- Computers

A forest is a top-level container in AD DS. Each forest is a collection of one or more domain trees that share a common directory schema and a global catalog. A domain tree is a collection of one or more domains that share a contiguous namespace. The forest root domain is the first domain that you create in the forest.

The forest root domain contains objects that don't exist in other domains in the forest. Because you always create these objects on the first domain controller, a forest can consist of as few as one domain with a single domain controller, or it can consist of several domains across multiple domain trees.

The following objects exist in the forest root domain:

- The schema master role.
- The domain naming master role.
- The Enterprise Admins group.
- The Schema Admins group.

An AD DS forest is often described as:
- A security boundary.
- A replication boundary.

The global catalog makes it possible to find objects from any domain in the forest.

Typically, an organization creates only one forest.

The following objects exist in each domain (including the forest root):

- Relative ID (RID) master role.
- Infrastructure master role.
- Primary domain controller (PDC) emulator master role.
- Domain Admins group.

An AD DS domain is a logical container for managing user, computer, group, and other objects. The AD DS database stores all domain objects, and each domain controller stores a copy of the database.

An AD DS domain is often described as:

- A replication boundary. 
- An administrative unit. Administrator account and a Domain Admins group. The Administrator account in the forest root domain has additional rights.

An AD DS domain provides:
- Authentication.
- Authorization.

Trust relationships
AD DS trusts enable access to resources in a complex AD DS environment. When you deploy a single domain, you can easily grant access to resources within the domain to users and groups from the domain. When you implement multiple domains or forests, you should ensure that the appropriate trusts are in place to enable the same access to resources.

In a multiple-domain AD DS forest, two-way transitive trust relationships generate automatically between AD DS domains so that a path of trust exists between all the AD DS domains. The trusts that create automatically in the forest are all transitive trusts, which means that if domain A trusts domain B, and domain B trusts domain C, then domain A trusts domain C.

You can deploy other types of trusts.

- Parent and child. Transitive. Two-way. When you add a new AD DS domain to an existing AD DS tree, you create new parent and child trusts.
- Tree-root. Transitive. Two-way. When you create a new AD DS tree in an existing AD DS forest, you automatically create a new tree-root trust.
- External. Nontransitive. One-way or two-way. External trusts enable resource access with a Windows NT 4.0 domain or an AD DS domain in another forest. You also can set these up to provide a framework for a migration.
- Realm. Transitive or nontransitive. One-way or two-way. Realm trusts establish an authentication path between a Windows Server AD DS domain and a Kerberos version 5 (v5) protocol realm that implements by using a directory service other than AD DS.
- Forest (complete or selective). Transitive. One-way or two-way. Trusts between AD DS forests allow two forests to share resources.
- Shortcut.	Nontransitive.	One-way or two-way. Configure shortcut trusts to reduce the time taken to authenticate between AD DS domains that are in different parts of an AD DS forest. No shortcut trusts exist by default, and an administrator must create them if they are required.

### Deploy Active Directory Domain Services domain controllers



