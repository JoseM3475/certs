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
Domain controllers authenticate all users and computers in a domain. Therefore, it's critical to ensure the optimal number and placement of domain controllers in any Active Directory Domain Services (AD DS) environment, especially in larger, distributed environments.

Deploy AD DS domain controllers in an on-premises environment.
-  Install the binaries necessary to implement the domain controller role.
-  Configure AD DS role.

SYSVOL

Install a domain controller on a Server Core installation of Windows Server.
Install a domain controller from media.
Branch office considerations. When you deploy a domain controller in a branch office that can't guarantee physical security, you can use additional measures to reduce the impact of a security breach. Deploy an RODC. The RODC contains a read-only copy of the AD DS database, and by default, it doesn't cache any user passwords. Once an RODC is deployed, most of its configuration centres on controlling which credentials it caches and who manages it. This is governed by the Password Replication Policy (PRP).

### Migrate a domain controller to a new site

Managing sites and subnets is a critical part of managing any corporate domain. Creating a new site allows for grouping objects by their physical location. Adding a subnet keeps all of the resources at the new site on the same network (or parts of the network). Finally, migrating a domain controller to the new site helps reduce internet traffic and lag associated with reaching out to a distant site for authentication and authorization queries.

Create a new site.
Map the new site to a subnet.
Move a domain controller to a new site

### Manage Active Directory Domain Services operations masters

Active Directory Domain Services (AD DS) uses a multiple-master process to copy data between domain controllers, and automatically implements a conflict resolution algorithm that remediates simultaneous, conflicting updates. multiple users and applications can concurrently apply changes to AD DS objects on different domain controllers. Such a model is necessary to support any AD DS environment with two or more domain controllers.

What are AD DS operations masters?

AD DS operation master roles are responsible for performing operations that are not suitable for a multiple-master model.  An operations master role is also known as a Flexible Single Master Operation (FSMO) role. There are five operations master roles:

- Schema master
- Domain-naming master
- Infrastructure master
- RID master
- PDC emulator master

  By default, the first domain controller installed in a forest hosts all five roles.

  Forest operations masters.
  - Domain naming master.
  - Schema master.
 
  Domain operations masters.
  - RID master. Security principal.
  - Infrastructure master.
  - PDC emulator master.

Manage AD DS operations masters
In an AD DS environment where you distribute operations master roles among domain controllers, you might need to move a role from one domain controller to another.
When you perform a move in a planned manner between two online domain controllers, the move is known as transferring the role. 
In emergencies, if the current role holder is not available, the move is known as seizing the role. When you transfer a role, the latest data from the domain controller in that role replicates to .the  target server.

Transfer operations master roles

## Create and manage Active Directory objects

### Define users, groups, and computers

What are managed service accounts? AD DS object, named a managed service account, which you use to facilitate service-account management.
Group managed service accounts enable you to extend the capabilities of standard managed service accounts to more than one server in your domain.
Network Load Balancing (NLB).

Group types:
- Security. Security groups are security-enabled, and you use them to assign permissions to various resources. You can use security groups in permission entries in access control lists (ACLs) to help control security for resource access. If you want to use a group to manage security, it must be a security group.
- Distribution. Email applications typically use distribution groups, which are not security-enabled. You also can use security groups as a means of distribution for email applications.

Group scopes. The scope of a group determines both the range of a group’s abilities or permissions and the group membership. 
- Local.
- Domain-local.
- Global.
- Universal.

What are computer objects?
Computers, like users, are security principals, in that:

- They have an account with a sign-in name and password that Windows changes automatically on a periodic basis.
- They authenticate with the domain.
- They can belong to groups and have access to resources, and you can configure them by using Group Policy.

Computers container. Before you create a computer object in AD DS, you must have a place to put it. The Computers container is a built-in container in an AD DS domain. This container is the default location for the computer accounts when a computer joins the domain. This container is not an OU. Instead, it is an object of the Container class. You cannot create an OU within a container, so you cannot subdivide the Computers container. You also cannot link a Group Policy Object to a container. Therefore, we recommend that you create custom OUs to host computer objects, instead of using the Computers container.

### Define organizational units

## Create and configure Group Policy Objects in Active Directory

### Define Group Policy Objects

Administrators can define settings centrally and then deploy them to computers across their organizations.
You define Group Policy settings within a Group Policy Object (GPO). A GPO is an object that contains one or more policy settings that apply to one or more configuration settings for a user or a computer.
User configuration settings or user policies, computer configuration settings or computer policies.
Settings do not affect groups directly and apply only to user and computer objects.

At the top of every GPO, settings are divided into two nodes: Computer Configuration node and the User Configuration node.
- Computer Configuration contains settings that apply to a computer, regardless of which user signs in. These settings define operating-system behavior, security configuration, startup and shutdown scripts, and system-wide application settings. Examples include password and account-lockout requirements, service startup behavior, and settings that control Windows components for every user of the device.
- User Configuration contains settings that apply to a user, regardless of which computer that user signs in to. These settings define the desktop environment, such as the appearance of the Start menu, logon and logoff scripts, folder redirection, and restrictions on the tools and Control Panel items that a user can access.

Policies and preferences:
- Policies contain managed settings that Group Policy enforces.
- Preferences contain settings that establish an initial configuration that a user can subsequently change.

The Policies node contains three subfolders in both Computer Configuration and User Configuration:
- Software Settings holds the Software installation extension, which you use to deploy applications to computers or users.
- Windows Settings holds settings that configure the operating system. Common items include Scripts (startup and shutdown for computers, logon and logoff for users), Security Settings (such as account policies, local policies, and Windows Defender Firewall), Name Resolution Policy, and Deployed Printers. Under User Configuration, this folder also includes Folder Redirection.
- Administrative Templates holds hundreds of registry-based settings, organized into folders such as Control Panel, Network, System, Printers, and Windows Components. Each setting in this folder corresponds to a specific registry value that controls the behavior of Windows or an application.

The Preferences node
The structure of an individual policy setting.
What are starter GPOs?

### Implement Group Policy Object scope and inheritance

The scope of a GPO is the collection of users and computers that will apply the settings in the GPO. You scope a GPO by linking it to an OU that contains the target users and computers.

You can link GPOs to: Sites, Domains, Organizational Units (OUs).

You can further narrow the scope of the GPO with one of two types of filters discussed in the following table.
- Security. These specify security groups or individual user or computer objects that relate to a GPO’s scope, but to which the GPO explicitly should or shouldn't apply.
- WMI. These specify a scope by using characteristics of a system, such as an operating system version or free disk space.

GPO processing order
The GPOs that apply to a user, computer, or both don't apply all at once. GPOs apply in a particular order. Conflicting settings that process later might overwrite settings that process first.

Group Policy follows the following hierarchical processing order:

- Local GPOs.
- Site-linked GPOs.
- Domain-linked GPOs.
- OU-linked GPOs.
- Child OU-linked GPOs.

In Group Policy application, the default rule is that the last policy (the most specific policy) applied prevails.

If you link several GPOs to an OU, their processing occurs in the order that the administrator specifies on the OU’s Linked Group Policy Objects tab in the Group Policy Management Console. 










