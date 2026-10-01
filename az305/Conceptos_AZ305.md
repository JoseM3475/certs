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

## Question
You have an application that runs on load-balanced Azure virtual machines. The application must access an Azure storage account and an Azure Key Vault.

You need to recommend an identity strategy for accessing Azure resources. The solution must meet the following requirements:

Secure access to the resources based on permissions.
Minimize the number of identities to create.
Which type of identity should you include in the recommendation?

Answer: You create a single managed identity and assign it to virtual machines and permissions. Using system-assigned managed identities create one identity for each virtual machine and those identities must be added to permissions for each resource accessed by the virtual machines. Microsoft Entra ID users and groups requires creating the users and the group manually.

## Question:
You have an on-premises Microsoft SQL Server solution that runs the following services:

- SQL Server Database Engine
- SQL Server Integration Services (SSIS)
- SQL Server Analysis Services (SSAS)
- SQL Server Reporting Services (SSRS)
- You need to migrate the solution to Azure. You must minimize costs and time to migrate.

What should you use?

Answer: SQL Server on Azure Virtual Machines is the only option to maintain SSIS, SSAS, and SSRS. SQL Managed Instance and Azure SQL Database do not support SSIS, SSAS, and SSRS. Azure Synapse Analytics does not support the SQL Server Database Engine, SSIS, and SSRS.

## Cool - Cold

# Diferencia entre las capas Cool y Cold en Azure Blob Storage

## Resumen

Tanto **Cool** como **Cold** son capas de acceso **online** de Azure Blob Storage. Esto significa que los datos están disponibles inmediatamente y no necesitan rehidratación para ser leídos. La diferencia principal es la frecuencia esperada de acceso y el equilibrio entre coste de almacenamiento y coste de recuperación. 【1-4ba6e3】【2-fc7828】

## Comparativa

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

【1-4ba6e3】【4-472df5】

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

【1-4ba6e3】【3-9edcc7】

## 
You are designing a data analysis solution in Azure. The solution will retrieve data from an Azure Event Hubs instance that contains the GPS location of a fleet of vehicles and send live data for a given vehicle to a Microsoft Power BI dashboard.

What should you use to process the data and send it to Power BI?

Select only one answer.

Azure Data Factory
This answer is incorrect.
Azure Event Grid
Azure SQL Database


Azure Stream Analytics

This answer is correct.
Stream Analytics can process a live stream and filter it. Azure SQL Database can be used to store the data, but not to do real-time streaming. Data Factory can be used to transform data but does not run continuous live jobs. Event Grid can be used as a data sink but does not provide filtering and a direct link to Power BI.

Introduction to Azure Stream Analytics | Microsoft Learn

Design an Azure Stream Analytics solution for data analysis - Training | Microsoft Learn

##
You need to design a data analysis solution in Azure that meets the following requirements:

Allows for data transformation
Links data to Microsoft Power BI
Performs near real-time log analysis
What should you use?

Select only one answer.

Azure Cosmos DB


Azure Data Factory

This answer is incorrect.

Azure SQL Manage Instance


Azure Synapse Analytics

This answer is correct.
Azure Synapse Analytics allows you to transform data, links data to Power BI, and performs near real-time log analysis. You cannot do near-real time log analysis in Data Factory. You cannot perform near real-time analysis in Azure Cosmos DB or SQL Managed Instance.

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





