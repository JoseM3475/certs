# Conceptos AZ-305.
## Proximity Placement Groups
[Proximity placement groups](https://learn.microsoft.com/en-us/azure/virtual-machines/co-location)

## Azure Functions that use the Consumption hosting plan has a default timeout of five minutes. You can extend this to 10 minutes maximum. Process2 and Process3 have too long a duration for this. Both C# and PHP are supported.
[Design for Azure Functions solutions](https://learn.microsoft.com/en-us/training/modules/design-compute-solution/8-design-for-azure-functions-solutions)

[Azure Functions hosting options](https://learn.microsoft.com/en-us/azure/azure-functions/functions-scale)

## Cache aside Pattern
[Cache-Aside pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/cache-aside)

## Private Links
[What is Azure Private Link service?](https://learn.microsoft.com/en-us/azure/private-link/private-link-service-overview)

## Virtual networks in different subscriptions can also be connected by using VPN gateways.
[]()

Azure VPN Gateways

## Virtual Networks flow logs
[Azure security logging and auditing](https://learn.microsoft.com/en-us/azure/security/fundamentals/log-audit)7

## Immutable Storage legal hold and Premium Blob storage ensure that logs are held for the required time and are stored immutable, meaning they cannot be changed once stored.

## Azure Monitor Workbooks 
To achieve centralized monitoring while respecting team autonomy, configure Data Collection Rules (DCRs) to control data ingestion into a centralized workspace, ensuring only relevant data is collected. Implement a centralized Log Analytics workspace with role-based access control (RBAC) to provide a unified view of logs and metrics while maintaining data security. Use Azure Monitor Workbooks to create interactive dashboards that consolidate data from various sources, offering a comprehensive view of resource performance. Implementing multiple Log Analytics workspaces with separate access controls leads to fragmented data management, using Azure Policy to enforce monitoring standards is more about governance than performance monitoring, and using Azure Monitor Alerts does not directly contribute to centralized monitoring.

**Question:** You have an application that runs on load-balanced Azure virtual machines. The application must access an Azure storage account and an Azure Key Vault.

You need to recommend an identity strategy for accessing Azure resources. The solution must meet the following requirements:

- Secure access to the resources based on permissions.
- Minimize the number of identities to create.

Which type of identity should you include in the recommendation?

**Answer**: You create a single managed identity and assign it to virtual machines and permissions. Using system-assigned managed identities create one identity for each virtual machine and those identities must be added to permissions for each resource accessed by the virtual machines. Microsoft Entra ID users and groups requires creating the users and the group manually.

**Question:** You have an on-premises Microsoft SQL Server solution that runs the following services:

- SQL Server Database Engine
- SQL Server Integration Services (SSIS)
- SQL Server Analysis Services (SSAS)
- SQL Server Reporting Services (SSRS)
- You need to migrate the solution to Azure. You must minimize costs and time to migrate.

What should you use?

**Answer:** SQL Server on Azure Virtual Machines is the only option to maintain SSIS, SSAS, and SSRS. SQL Managed Instance and Azure SQL Database do not support SSIS, SSAS, and SSRS. Azure Synapse Analytics does not support the SQL Server Database Engine, SSIS, and SSRS.

**Diferencia entre las capas Cool y Cold en Azure Blob Storage**

Tanto **Cool** como **Cold** son capas de acceso **online** de Azure Blob Storage. Esto significa que los datos están disponibles inmediatamente y no necesitan rehidratación para ser leídos. La diferencia principal es la frecuencia esperada de acceso y el equilibrio entre coste de almacenamiento y coste de recuperación. 【1-4ba6e3】【2-fc7828】

Comparativa

| Característica | Cool | Cold |
|----------------|------|-------|
| Tipo de acceso | Online | Online |
| Frecuencia de acceso esperada | Poco frecuente | Muy rara |
| Coste de almacenamiento | Bajo | Más bajo |
| Coste de lectura y recuperación | Alto | Más alto |
| Retención mínima recomendada | 30 días | 90 días |
| Latencia de acceso | Inmediata (milisegundos) | Inmediata (milisegundos) |
| Casos de uso típicos | Backups recientes, DR, logs | Backups históricos, auditorías, cumplimiento normativo |

【1-4ba6e3】【2-fc7828】

## Cool Tier

La capa **Cool** está diseñada para datos que:

- Se acceden ocasionalmente.
- Deben estar disponibles inmediatamente.
- Permanecerán almacenados al menos 30 días.

### Ejemplos

- Backups semanales.
- Informes mensuales.
- Logs recientes.
- Datos de recuperación ante desastres (DR).

La capa Cool reduce el coste de almacenamiento respecto a Hot, pero aumenta el coste de lectura y acceso. 【1-4ba6e3】【3-9edcc7】

## Cold Tier

La capa **Cold** está diseñada para datos que:

- Se acceden muy raramente.
- Deben seguir estando disponibles inmediatamente.
- Permanecerán almacenados al menos 90 días.

### Ejemplos

- Backups trimestrales o anuales.
- Datos históricos.
- Información para auditorías.
- Registros de cumplimiento normativo.

La capa Cold reduce aún más el coste de almacenamiento respecto a Cool, pero incrementa los costes de acceso y recuperación. 【1-4ba6e3】【2-fc7828】

## Diferencia clave para el examen AZ-305

### Cool

> Acceso poco frecuente, pero todavía relativamente habitual.

Ejemplo:
- Un backup que podría restaurarse varias veces al año.

### Cold

> Acceso muy raro, pero debe poder recuperarse inmediatamente si es necesario.

Ejemplo:
- Un backup que probablemente nunca se restaurará, aunque debe permanecer disponible online.


## Comparación con Archive

```text
Frecuencia de acceso

Hot -----> Cool -----> Cold -----> Archive

Más accesos                    Menos accesos

Coste almacenamiento:
Alto -> Bajo -> Más bajo -> Mínimo

Tiempo de recuperación:
Inmediato -> Inmediato -> Inmediato -> Horas (rehidratación)
```

La diferencia más importante entre **Cold** y **Archive** es que **Cold sigue siendo online**, mientras que **Archive es offline y requiere rehidratación antes de acceder a los datos**. 【1-4ba6e3】【2-fc7828】

## Regla rápida de memorización para AZ-305

- **Hot** → acceso frecuente.
- **Cool** → acceso ocasional.
- **Cold** → acceso muy raro pero inmediato.
- **Archive** → acceso excepcional y con latencia de horas.



**Question:** You are designing a data analysis solution in Azure. The solution will retrieve data from an Azure Event Hubs instance that contains the GPS location of a fleet of vehicles and send live data for a given vehicle to a Microsoft Power BI dashboard.

What should you use to process the data and send it to Power BI?

Select only one answer.

- Azure Data Factory
- Azure Event Grid
- Azure SQL Database
- Azure Stream Analytics

**Answer:** Stream Analytics can process a live stream and filter it. Azure SQL Database can be used to store the data, but not to do real-time streaming. Data Factory can be used to transform data but does not run continuous live jobs. Event Grid can be used as a data sink but does not provide filtering and a direct link to Power BI.

Introduction to Azure Stream Analytics | Microsoft Learn

Design an Azure Stream Analytics solution for data analysis - Training | Microsoft Learn

**Question:** You need to design a data analysis solution in Azure that meets the following requirements:

- Allows for data transformation
- Links data to Microsoft Power BI
- Performs near real-time log analysis
- What should you use?

Select only one answer.

- Azure Cosmos DB
- Azure Data Factory
- Azure SQL Manage Instance

**Answer:** Azure Synapse Analytics allows you to transform data, links data to Power BI, and performs near real-time log analysis. You cannot do near-real time log analysis in Data Factory. You cannot perform near real-time analysis in Azure Cosmos DB or SQL Managed Instance.

What is Azure Synapse Analytics? - Azure Synapse Analytics | Microsoft Learn

Design a data integration and analytic solution with Azure Synapse Analytics - Training | Microsoft Learn

## 
Azure Data Factory is a fully managed data integration service designed to ingest and transform data on a scheduled basis from on-premises systems into Azure storage with minimal administrative effort.
Azure Data Explorer is optimized for interactive analytics over large volumes of telemetry and log data not for orchestrating scheduled data movement.
Azure Event Grid provides event-based routing rather than batch data integration.
Azure Service Bus is a messaging service used for decoupling applications and does not perform data ingestion or integration workflows.

##
You have Azure virtual machines that contain Microsoft SQL Server databases configured in an Always On availability group.

Backups must be retained for 10 years and managed centrally in the Azure portal.

You need an Azure-native backup solution that does NOT require managing the backup infrastructure.

What should you recommend?

Select only one answer.

Configure Automated Backup for SQL Server on each virtual machine and store the backups in Azure Storage.


Install the Microsoft Azure Recovery Services (MARS) agent and back up the SQL Server data files.

This answer is incorrect.

Perform manual backups to managed disks and copy the backups to Azure Storage.


Use Azure Backup for SQL Server on Azure VMs with a Recovery Services vault and long-term retention.

This answer is correct.
Objective:

3.1 Design solutions for backup and disaster recovery

What This Item Tests:

Recommend a backup and recovery solution for databases

Additional Reading:

Decision matrix - Training | Microsoft Learn

When to use Azure Backup - Training | Microsoft Learn

Introduction - Training | Microsoft Learn

Backup and Recovery - Training | Microsoft Learn

Backup and restore - Training | Microsoft Learn

Rationale:

Azure Backup for SQL Server on Azure VMs provides application-consistent backups, centralized management in the Azure portal, and long-term retention through a Recovery Services vault without requiring a custom backup infrastructure. The other options require virtual machine-level management, manual processes, and do not provide database-aware backup capabilities.

## Availability sets provide high availability for Azure virtual machines by distributing instances across fault and update domains, ensuring workloads remain available during host maintenance or hardware failures. Azure Backup and virtual machine snapshots provide recovery after failure but do not ensure availability. Azure Site Recovery is a disaster recovery solution designed for regional outages rather than host-level availability.

##
You have an Azure App Service web app that writes data to an Azure SQL database.

You plan to configure the database to use the Always Encrypted feature.

You need to recommend a solution to ensure that the web app can write encrypted data.

Which two actions should you include in the recommendations? Each correct answer presents part of the solution.

Select all answers that apply.

Change the connection string used by the application.

This answer is correct.

Change the SSL settings for the web app.


Enable Transparent Data Encryption (TDE).

This answer is incorrect.

Store keys in Azure Key Vault.

This answer is correct.

Store keys in the certificate store.

You need to change the connection string to use Always Encrypted and access to the keys from a store such as Key Vault. Changing the SSL settings for the web app allows the use of SSL for in transit encryption, but not Always Encrypted.

Tutorial: Getting started with Always Encrypted - SQL Server | Microsoft Learn

## 
You have a Microsoft SQL Server application that uses SQL common language runtime (CLR) integration.

You need to migrate the application to Azure. The solution must minimize ongoing administration costs.

What should you use?

Select only one answer.

Azure Cosmos DB for NoSQL


Azure SQL Database


Azure SQL Managed Instance

This answer is correct.

SQL Server on Azure Virtual Machines

This answer is incorrect.
SQL Managed Instance supports SQL CLR and avoids general administrative overhead. Azure SQL Database does not support SQL CLR integration. SQL Server on Azure Virtual Machines supports SQL CLR integration but has higher ongoing administrative overhead. Azure Cosmos DB for NoSQL API supports SQL syntax over documents. It does not support SQL CLR.

Design for Azure SQL Managed Instance - Training | Microsoft Learn

##

You have an Azure SQL database named DB1 that contains a table named Customers and is 500 GB.

You need to minimize how long it takes to back up and restore DB1.

What should you do?

Select only one answer.

Configure DB1 to use the Business Critical service tier.


Configure DB1 to use the Hyperscale service tier.

This answer is correct.

Configure DB1 to use the Premium service tier.


Split the Customers table into multiple tables within the same database.

This answer is incorrect.
Objective:

2.1 Design data storage solutions for relational data

What This Item Tests:

Recommend a database service tier and compute tier

Additional Reading:

Understand SQL database hyperscale - Training | Microsoft Learn

Rationale:

Configuring the database to use the Hyperscale service tier minimizes backup and restore times by using snapshot-based backups and a distributed storage architecture optimized for very large databases, making it well suited for a 500-GB workload. Business Critical and Premium service tiers prioritize performance and availability but rely on traditional backup mechanisms that take longer as the database size increases. Splitting the table introduces schema and application complexity and does not directly improve backup or restore performance.

## 
Your organization operates from locations in the United States, the United Kingdom, Australia, and Germany. Each location has employees that work with files stored in a File Share on Azure Storage.

You are designing the structure of the storage accounts. The accounts must meet the following requirements:

A single policy will enforce regulatory requirements.
Low IO latency is critical.
Costs must be minimized.
How many storage accounts should you create?

Select only one answer.

1

This answer is incorrect.

2


3


4

This answer is correct.
The requirement for high performance is best met by local files in each country. A single policy can still be applied at a scope that covers the four storage accounts. Increasing the number of storage accounts does not increase the costs of the solution, apart from a very small potential increase in administration costs.

Design for Azure storage accounts - Training | Microsoft Learn

##

You need to design a data storage solution in Azure. The solution must meet the following requirements:

Be optimized for JSON data.
Support failover to a different Azure region.
Minimize costs.
What should you include in the design?

Select only one answer.

Azure Cosmos DB

This answer is incorrect.

Azure Data Lake Storage

This answer is correct.

Azure SQL Database


Azure SQL Managed Instance

Data Lake Storage is optimized for unstructured data, provides GRS, and is cheaper. Azure SQL Database and SQL Managed Instance are optimized for relational data. Azure Cosmos DB is optimized for JSON data and failover but is a lot more expensive than Data Lake Storage.

Data redundancy - Azure Storage | Microsoft Learn

Design a data integration solution with Azure Data Lake - Training | Microsoft Learn

## 
You need to design a file storage solution in Azure. The solution must meet the following requirements:

Provide the highest possible durability.
Remain available during a zone or Azure region failure.
Which type of redundancy should you use?

Select only one answer.

geo-redundant storage (GRS)


geo-zone-redundant storage (GZRS)

This answer is correct.

locally-redundant storage (LRS)


zone-redundant storage (ZRS)

This answer is incorrect.
Geo-zone-redundant storage (GZRS) provides zone and region redundancy, and the highest durability. Locally-redundant storage (LRS) provides redundancy at the zone level. Zone-redundant storage (ZRS) provides redundancy at the region level. Geo-redundant storage (GRS) provides redundancy for region failure, but not at the zone and region level.

Data redundancy - Azure Storage | Microsoft Learn

Design for data redundancy - Training | Microsoft Learn
## Your organization has many Microsoft SQL Server Integration Services (SSIS) packages that run on an on-premises SQL Server.

You are migrating the SQL Server resources to Azure.

You need to migrate the SSIS packages to Azure.

Which two options you can use? Each correct answer presents a complete solution.

Select all answers that apply.

Azure Data Factory

This answer is correct.

Azure SQL Database


Azure SQL Managed Instance

This answer is incorrect.

SQL Server on Azure Virtual Machines

This answer is correct.
When you deploy SQL Server to an Azure virtual machine, you can install SSIS and run the packages natively. You can also deploy an SSIS integration runtime to Data Factory to execute the SSIS packages. The other options do not support SSIS.

Design a data integration solution with Azure Data Factory - Training | Microsoft Learn

## 
You have an on-premises Microsoft SQL Server deployment that you plan to migrate to Azure.

The SQL Server code regularly executes operating system commands by using the xp_cmdshell statement.

Performance metrics for the existing system show the following:

- Average CPU is 45 percent.
- Average disk I/O is 98 percent.

Which deployment option should you recommend for the migrated system?

Select only one answer.

Azure SQL Database

Azure SQL Managed Instance

This answer is incorrect.

Azure Storage-optimized virtual machine

This answer is correct.

Azure Memory-optimized virtual machine

You need to deploy a virtual machine-based solution for SQL Server as low-level operating system access is required. From the available options, the storage-optimized virtual machine provides the best performance, given the current loadings.

Design for Azure Virtual Machines solutions - Training | Microsoft Learn


Design security for data at rest, data in motion, and data in use - Training | Microsoft Learn

## 
Your organization manufactures breathing machines to assist patients with asthma.

You are creating a Microsoft Power BI dashboard to monitor the overall effectiveness of the machines across all users.

Each machine has built-in wireless internet connectivity and can send monitoring data to an online service. Azure Stream Analytics will be used to populate a streaming dataset in Power BI.

To which service should the breathing machines send data?

Select only one answer.

Azure Cosmos DB


Azure Event Hubs

This answer is correct.

Azure SQL Database


Azure Stream Analytics

This answer is incorrect.
Event Hubs is a good target for large numbers of events from internet-connected devices. It is also a good source of event data for Stream Analytics, which can then be used to populate a streaming dataset in Power BI.

Introduction to Azure Stream Analytics | Microsoft Learn

Design an Azure Event Hubs messaging solution - Training | Microsoft Learn

## You are designing a networking solution to optimize connectivity from the internet to a web app hosted in Azure. The solution must meet the following requirements:

Be available if an Azure region fails.
Route users to the closest region hosting the app.
What should you include in the recommendation?

Select only one answer.

Azure API Management


Azure Application Gateway


Azure Load Balancer

This answer is incorrect.

Azure Traffic Manager

This answer is correct.
Traffic Manager provides failover and geographic routing. Azure API Management, Azure Load Balancer, and Application Gateway do not provide any of these features.

Azure Traffic Manager | Microsoft Learn

Design for Azure Traffic Manager - Training | Microsoft Learn

## You are migrating resources to Azure.

You are designing the required virtual networks.

You need to identify whether multiple virtual networks will be required.

Which three requirements will cause you to create multiple virtual networks? Each correct answer presents a complete solution.

Select all answers that apply.

deploying Azure Key Vault


deploying multiple Azure SQL Managed Instances

This answer is correct.

deploying resources to multiple resource groups

This answer is incorrect.

deploying resources to multiple subscriptions

This answer is correct.

organizational security requirements

This answer is correct.

organizational SLAs

Virtual networks can span resource groups but not subscriptions. Some services such as SQL Managed Instance deploy their own virtual networks. You might have security requirements that require isolating or segmenting resources.

Recommend a network architecture solution based on workload requirements - Training | Microsoft Learn

## You have two subscriptions named Sub1 and Sub2 in an Azure tenant.

You need to connect a virtual network in Sub1 to a virtual network in Sub2..

Which two networking features should you recommend? Each correct answer presents a complete solution.

Select all answers that apply.

Azure Private Link

This answer is incorrect.

ExpressRoute


Virtual network peering

This answer is correct.

VPN gateways

This answer is correct.
Virtual networks cannot span subscriptions. Virtual network peering is the correct mechanism to ensure that the resources in each subscription can communicate with each other as a single logical virtual network. Virtual networks in different subscriptions can also be connected by using VPN gateways.

Design for subscriptions - Training | Microsoft Learn
Configure a VNet-to-VNet VPN gateway connection: Azure portal - Azure VPN Gateway | Microsoft Learn

##

You have two subscriptions named Sub1 and Sub2 in an Azure tenant.

You need to connect a virtual network in Sub1 to a virtual network in Sub2..

Which two networking features should you recommend? Each correct answer presents a complete solution.

Select all answers that apply.

Azure Private Link

This answer is incorrect.

ExpressRoute


Virtual network peering

This answer is correct.

VPN gateways

This answer is correct.
Virtual networks cannot span subscriptions. Virtual network peering is the correct mechanism to ensure that the resources in each subscription can communicate with each other as a single logical virtual network. Virtual networks in different subscriptions can also be connected by using VPN gateways.

Design for subscriptions - Training | Microsoft Learn
Configure a VNet-to-VNet VPN gateway connection: Azure portal - Azure VPN Gateway | Microsoft Learn

## You are migrating an on-premises application to Azure.

The application is deployed to three Azure virtual machines that are each configured as web servers. The application manages its own users and passwords.

The application requires permission to access Azure resources. Each web server must use the same identity to authenticate to Microsoft Entra ID.

What should the web servers use to authenticate?

Select only one answer.

a service principal

This answer is incorrect.

a system-assigned managed identity


a user-assigned managed identity

This answer is correct.

a username and password

User-assigned managed identities automate credential rotation and can be applied to multiple resources. Service principals depend on secrets that expire and do not have automatic credential rotation. System-assigned managed identities apply to single resources and will not work for three web servers. A username and password do not provide automatic credential rotation.

Design service principals for applications - Training | Microsoft Learn

## You have an Azure storage account that contains a file share.

You need to recommend a solution to automatically back up the file share.

What should you recommend using to store the backups?

Select only one answer.

Azure Files in a second Azure region

This answer is incorrect.

Azure Key Vault


Backup Vault


Recovery Services vault

This answer is correct.
Recovery Service vaults and Backup Vaults provide protection for data from different data sources. Azure Files is a supported data source for Recovery Service vaults.

Design for Azure files backup and recovery - Training | Microsoft Learn

## You have an Azure subscription that contains Azure SQL databases.

You need to recommend a backup solution for the databases. The solution must ensure that the backups are configurable for at least 90 days.

What should you recommend?

Select only one answer.

Geo-zone-redundant storage (GZRS)


Locally-redundant storage (LRS)


Long-term retention (LTR)

This answer is correct.

Transaction log backups

This answer is incorrect.
LTR is required to store a backup for more than 35 days.

LRS and GZRS options are valid storage redundancy options.. Transaction log backups are not relevant for this scenario.

Design for Azure SQL backup and recovery - Training | Microsoft Learn

## You have an Azure subscription that contains a multi-tier application named WebApp1. WebApp1 uses a frontend application running on virtual machines that run Windows Server and SQL Server on Azure virtual machines for backend processing.

You need to recommend a high-availability solution for WebApp1 to limit the impact of:

Azure-related maintenance activities
Azure datacenter-level failures
Which two solutions should you recommend? Each correct answer presents a full solution.

Select all answers that apply.

Always On availability group


Always On Failover Cluster Instance (FCI)


Availability sets

This answer is correct.

Availability zones

This answer is correct.

Azure Backup

Availability sets and availability zones are designed to limit the impact of environmental issues at the Azure level, such as datacenter failure, physical hardware failure, network outages, power interruptions, and maintenance activities. The two cannot be combined. Azure Backup is not a high-availability solution. The Always On options are for Microsoft SQL Server high availability only.

Resiliency checklist for services - Azure Architecture Center | Microsoft Learn

## You have an Azure subscription that contains an Azure SQL Managed Instance.

You need to recommend a high-availability solution for the Azure SQL Managed Instance architecture. The solution must ensure that the instance can replicate and fail over to another Azure region.

What should you recommend?

Select only one answer.

active geo-replication

This answer is incorrect.

Always On availability group


auto-failover groups

This answer is correct.

SQL Data Sync for Azure

Auto-failover groups allow high availability for Azure SQL Managed Instance. Active geo-replication is not supported for Azure SQL Managed Instance. SQL Data Sync for Azure cannot control failover. Always On failover cluster requires additional administrative effort to implement high availability and cannot control replication or failover to another Azure region.

Active geo-replication - Azure SQL Database | Microsoft Learn

Explore high availability and disaster recovery options - Training | Microsoft Learn

Describe high availability and disaster recovery options for PaaS deployments - Training | Microsoft Learn

Auto-failover groups overview & best practices - Azure SQL Managed Instance | Microsoft Learn





