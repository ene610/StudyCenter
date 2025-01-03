# Introduzione

Microsoft Fabric (SaaS) is an end-to-end, all-in-one unified analytics platform that brings together all the data and analytics tools that organizations need. As a single, unified platform for data management, data lakes, data integration, data engineering, data warehousing, data science, real-time analytics, and business intelligence, it has been designed from the ground up to help organizations simplify their analytics workloads, reduce costs, and reduce the time taken to obtain insights in this era of AI.
the core capabilities of Fabric are:
![[core capabilities Fabric.png]]

Microsoft Fabric is a single unified product that takes care of everything an organization (from  
departmental stores to large enterprises) needs to build an analytics system—all the way from  
ingesting data from different types of data sources to transforming at the correct scale using familiar utilities (SQL and Apache Spark)—serving this to business users with industry-leading Power BI, with shared security and governance that works across all the components in a cohesive manner.

### OneLake 
OneLake is based on a SaaS foundation, and underneath, it is built on top of Azure Data Lake  
Storage (ADLS) Gen2, supporting any type of file whether structured, semi-structured, or  
unstructured.

### OneCopy:

### Shortcut
The shortcut feature in OneLake is a reference to the data stored in other file locations; this makes data sharing as simple and easy as sharing files in OneDrive, removing the need for data duplication. No matter where the location is Azure or Amazon or Google, the reference makes it appear as though the files and folders are stored locally. In this way, it creates a data abstraction and data virtualization layer for all the data in your organization.

![[shortcut1.png]]

### OneSecurity
With the OneSecurity feature, Fabric offers a shared universal security model that is enforced across  all the engines in Fabric, as shown in figure This means that you are able to define security once  in the lakehouse and have those permissions honored by every engine in Fabric (Spark, SQL, and  Power BI). This security definition can be used for data access permissions for individual tables or files and folders in the lakehouse and can be granted to individual users and Microsoft Entra ID groups.

![[oneSecurity1.png]]

# Capitolo 2

