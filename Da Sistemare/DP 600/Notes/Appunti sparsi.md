# Tenant vs Capacity vs Workspace
![[Esempio Fabric tenant.png]]
**Tenant**: dove è deployato Fabric, colelgato a uno specifico DNS 
**Capacity**: risiede all'interno di un tenant, rappresenta un isnieme di risorse allocate a Microsoft Fabric la sua size determina l'ammontare di potenza disponibile, espresso in licenze che definiscono le feature che si possono utilizzare e gli item e le CU/SKU.
**Workspace**: sono dei conteinrs di un items, è il luogo dove i dati sono creati, trasformati e consumati

Quando accedi a Fabric  ci sono due tipi di licenze
- **capacity license** una licenza che provvede a un insieme di risorse per le attività svolte in Fabric. le licenze sono distinte in SKU, ognuni SKU provvede a sua volta un numero di CU che sono usate per calcolare la potenza computazionale delle capacity
- **per user license** licenze usate dagli utenti per permettere di operare con Fabric

Il ruolo che permette di gestire le license è Fabric admin

# DT vs DO

_Data transformation_ involves altering the structure or content of data to meet specific requirements. Tools for data transformation in Fabric include Dataflows (Gen2) and notebooks. Dataflows are a great option for smaller semantic models and simple transformations. Notebooks are a better option for larger semantic models and more complex transformations. Notebooks also allow you to save your transformed data as a managed Delta table in the lakehouse, ready for reporting.

_Data orchestration_ refers to the coordination and management of multiple data-related processes, ensuring they work together to achieve a desired outcome. The primary tool for data orchestration in Fabric is _pipelines_. A pipeline is a series of steps that move data from one place to another, in this case, from one layer of the medallion architecture to the next. Pipelines can be automated to run on a schedule or triggered by an event.

# One lake security

# Workspace role assigment

# Analyzer tabular Editor

# Query Folding

# aaaa

