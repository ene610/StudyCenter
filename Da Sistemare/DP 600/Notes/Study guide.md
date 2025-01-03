# Plan, implement, and manage a solution for data analytics (10–15%)

## Plan a data analytics environment
- Identify requirements for a solution, including components, features, performance, and capacity stock-keeping units (SKUs)
    
    - [Microsoft Fabric concepts and licenses](https://learn.microsoft.com/en-us/fabric/enterprise/licenses)X
    - [Power BI guidance documentation](https://learn.microsoft.com/en-us/power-bi/guidance/) V
    - [Power BI Embedded with Microsoft Fabric](https://powerbi.microsoft.com/en-us/blog/power-bi-embedded-with-microsoft-fabric/) V
- Recommend settings in the Fabric admin portal
    
    - [Microsoft Fabric documentation for admins](https://learn.microsoft.com/en-us/fabric/admin/)
- Choose a data gateway type
    
    - [What is an on-premises data gateway?](https://learn.microsoft.com/en-us/data-integration/gateway/)
    - [Guidance for deploying a data gateway for the Power BI service](https://learn.microsoft.com/en-us/power-bi/connect-data/service-gateway-deployment-guidance)
    - [On-premises data gateway in-depth](https://learn.microsoft.com/en-us/power-bi/connect-data/service-gateway-onprem-indepth)
    - [Manage on-premises data gateway high-availability clusters and load balancing](https://learn.microsoft.com/en-us/data-integration/gateway/service-gateway-high-availability-clusters)
    - [Manage security roles of an on-premises data gateway](https://learn.microsoft.com/en-us/data-integration/gateway/manage-security-roles)
    - [Add or remove a gateway data source](https://learn.microsoft.com/en-us/power-bi/connect-data/service-gateway-data-sources)
    - [Manage your data source - import and scheduled refresh](https://learn.microsoft.com/en-us/power-bi/connect-data/service-gateway-enterprise-manage-scheduled-refresh)
    - [Use custom data connectors with an on-premises data gateway](https://learn.microsoft.com/en-us/power-bi/connect-data/service-gateway-custom-connectors)
    - [Plan, scale, and maintain a business-critical gateway solution](https://learn.microsoft.com/en-us/data-integration/gateway/plan-scale-maintain)
    - [On-premises data gateway sizing](https://learn.microsoft.com/en-us/power-bi/guidance/gateway-onprem-sizing)
    - [What is a virtual network (VNet) data gateway (Preview)?](https://learn.microsoft.com/en-us/data-integration/vnet/overview)
    - [Virtual network data gateway architecture](https://learn.microsoft.com/en-us/data-integration/vnet/data-gateway-architecture)
- Create a custom Power BI report theme
    
    - [Use report themes in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-report-themes)

## Implement and manage a data analytics environment

- Implement workspace and item-level access controls for Fabric items
    
    - [Roles in workspaces in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/get-started/roles-workspaces)
    - [Give users access to workspaces](https://learn.microsoft.com/en-us/fabric/get-started/give-access-workspaces)
    - [Share items in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/get-started/share-items)
- Implement data sharing for workspaces, warehouses, and lakehouses
    
    - Workspaces
        - [Share Power BI reports and dashboards with coworkers and others](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-share-dashboards)
        - [Display the dashboards and reports that others have shared with me](https://learn.microsoft.com/en-us/power-bi/collaborate-share/end-user-shared-with-me)
        - [Request or grant access to shared dashboards or reports](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-request-access)
        - [Share a filtered Power BI report](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-share-reports)
        - [Troubleshoot issues sharing dashboards and reports](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-troubleshoot-sharing)
        - [Filter a report using query string parameters in the URL](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-url-filters)
        - [Ways to collaborate and share in Power BI](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-how-to-collaborate-distribute-dashboards-reports)
        - [View Power BI files in OneDrive and SharePoint](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-sharepoint-viewer)
    - Lakehouses
        - [How lakehouse sharing works](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-sharing)
        - [OneLake security](https://learn.microsoft.com/en-us/fabric/onelake/onelake-security)
        - [Get started securing your data in OneLake](https://learn.microsoft.com/en-us/fabric/onelake/get-started-security)
    - Warehouses
        - [Workspace roles in Fabric data warehousing](https://learn.microsoft.com/en-us/fabric/data-warehouse/workspace-roles)
        - [Security for data warehousing in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-warehouse/security)
        - [Share your warehouse and manage permissions](https://learn.microsoft.com/en-us/fabric/data-warehouse/share-warehouse-manage-permissions)
        - [SQL granular permissions in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-warehouse/sql-granular-permissions)
        - [Column-level security in Fabric data warehousing](https://learn.microsoft.com/en-us/fabric/data-warehouse/column-level-security)
        - [Row-level security in Fabric data warehousing](https://learn.microsoft.com/en-us/fabric/data-warehouse/row-level-security)
    - Best practices
        - [Power BI implementation planning: Report consumer security planning](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-security-report-consumer-planning)
        - [Power BI implementation planning: Content creator security planning](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-security-content-creator-planning)
        - [Distribute Power BI content to external guest users using Microsoft Entra B2B](https://learn.microsoft.com/en-us/power-bi/guidance/whitepaper-azure-b2b-power-bi)
        - [Power BI usage scenarios](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-usage-scenario-overview)
- Manage sensitivity labels in semantic models and lakehouses
    
    - [Power BI implementation planning: Information protection for Power BI](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-info-protection)
    - [Information protection in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/governance/information-protection)
    - [Sensitivity labels in Power BI](https://learn.microsoft.com/en-us/power-bi/enterprise/service-security-sensitivity-label-overview)
    - [Enable sensitivity labels in Fabric](https://learn.microsoft.com/en-us/power-bi/enterprise/service-security-enable-data-sensitivity-labels)
    - [How to apply sensitivity labels in Power BI](https://learn.microsoft.com/en-us/power-bi/enterprise/service-security-apply-data-sensitivity-labels)
    - [Sensitivity label downstream inheritance](https://learn.microsoft.com/en-us/power-bi/enterprise/service-security-sensitivity-label-downstream-inheritance)
    - [Audit schema for sensitivity labels in Power BI](https://learn.microsoft.com/en-us/power-bi/enterprise/service-security-sensitivity-label-audit-schema)
    - [Data protection metrics report](https://learn.microsoft.com/en-us/power-bi/enterprise/service-security-data-protection-metrics-report)
- Configure Fabric-enabled workspace settings
    
    - [Create, configure, and use an environment in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-engineering/create-and-use-environment)
    - [Spark workspace administration settings in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-engineering/workspace-admin-settings)
    - [Configuring starter pools in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-engineering/configure-starter-pools)
    - [Billing and utilization reporting for Spark in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-engineering/billing-capacity-management-for-spark)
    - [How to create custom Spark pools in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-engineering/create-custom-spark-pools)
    - [Configure high concurrency mode for Fabric notebooks](https://learn.microsoft.com/en-us/fabric/data-engineering/configure-high-concurrency-session-notebooks)
- Manage Fabric capacity
    
    - [Microsoft Fabric concepts and licenses](https://learn.microsoft.com/en-us/fabric/enterprise/licenses)
    - [Buy a Microsoft Fabric subscription](https://learn.microsoft.com/en-us/fabric/enterprise/buy-subscription)
    - [Pause and resume your capacity](https://learn.microsoft.com/en-us/fabric/enterprise/pause-resume)
    - [Scale your capacity](https://learn.microsoft.com/en-us/fabric/enterprise/scale-capacity)
    - [The Fabric throttling policy](https://learn.microsoft.com/en-us/fabric/enterprise/throttling)
    - [Microsoft Fabric Capacity Metrics app](https://learn.microsoft.com/en-us/fabric/enterprise/metrics-app)
    - [Microsoft Fabric trial](https://learn.microsoft.com/en-us/fabric/get-started/fabric-trial)
    - [Configure and manage data engineering and data science settings for Fabric capacities](https://learn.microsoft.com/en-us/fabric/data-engineering/capacity-settings-management)

## Manage the analytics development lifecycle


- Implement version control for a workspace
    
    - [Lifecycle management documentation in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/cicd/)
    - [Lakehouse deployment pipelines and git integration (Preview)](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-git-deployment-pipelines)
- Create and manage a Power BI Desktop project (.pbip)
    
    - [Power BI Desktop projects](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-overview)
    - [Power BI Desktop project dataset folder](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-dataset)
    - [Power BI Desktop project report folder](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-report)
    - [Power BI Desktop projects Git integration](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-git)
    - [Power BI Desktop projects Azure DevOps integration](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-azdo)
    - [Power BI Project (PBIP) and Azure DevOps build pipelines for continuous integration](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-build-pipelines)
- Plan and implement deployment solutions
    
    - [Introduction to deployment pipelines](https://learn.microsoft.com/en-us/fabric/cicd/deployment-pipelines/intro-to-deployment-pipelines)
    - [The deployment pipelines process](https://learn.microsoft.com/en-us/fabric/cicd/deployment-pipelines/understand-the-deployment-process)
    - [Create deployment rules](https://learn.microsoft.com/en-us/fabric/cicd/deployment-pipelines/create-rules)
    - [Automate your deployment pipeline by using APIs and Azure DevOps](https://learn.microsoft.com/en-us/fabric/cicd/deployment-pipelines/pipeline-automation)
- Perform impact analysis of downstream dependencies from lakehouses, data warehouses, dataflows, and semantic models
    
    - [Data lineage](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-data-lineage)
    - [Semantic model impact analysis](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-dataset-impact-analysis)
    - [Data source impact analysis](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-data-source-impact-analysis)
- Deploy and manage semantic models by using the XMLA endpoint
    
    - [Power BI usage scenarios: Advanced data model management](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-usage-scenario-advanced-data-model-management)
    - [Semantic model connectivity with the XMLA endpoint](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-connect-tools)
    - [Troubleshoot XMLA endpoint connectivity](https://learn.microsoft.com/en-us/power-bi/enterprise/troubleshoot-xmla-endpoint)
    - [Create perspectives](https://learn.microsoft.com/en-us/analysis-services/tutorial-tabular-1400/as-lesson-8-create-perspectives?view=asallproducts-allversions)
    - [ALM Toolkit](https://www.sqlbi.com/tools/alm-toolkit/)
- Create and update reusable assets, including Power BI template (.pbit) files, Power BI data source (.pbids) files, and shared semantic models
    
    - [Create and use report templates in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-templates)
    - [Use PBIDS files to get data](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-data-sources#use-pbids-files-to-get-data)
    - [Use semantic models across workspaces](https://learn.microsoft.com/en-us/power-bi/connect-data/service-datasets-across-workspaces)
    - [Semantic model description](https://learn.microsoft.com/en-us/power-bi/connect-data/service-dataset-description)
    - [Share access to a semantic model](https://learn.microsoft.com/en-us/power-bi/connect-data/service-datasets-share)
    - [Semantic model permissions](https://learn.microsoft.com/en-us/power-bi/connect-data/service-datasets-permissions)
    - [Manage semantic model access permissions](https://learn.microsoft.com/en-us/power-bi/connect-data/service-datasets-manage-access-permissions)
    - [Build permission for shared semantic models](https://learn.microsoft.com/en-us/power-bi/connect-data/service-datasets-build-permissions)
    - [Create reports based on semantic models from different workspaces](https://learn.microsoft.com/en-us/power-bi/connect-data/service-datasets-discover-across-workspaces)
    - [Copy reports from other workspaces](https://learn.microsoft.com/en-us/power-bi/connect-data/service-datasets-copy-reports)
    - [Control the use of semantic models across workspaces](https://learn.microsoft.com/en-us/power-bi/connect-data/service-datasets-admin-across-workspaces)
    - [Endorse your content](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-endorse-content)

# Prepare and serve data (40–45%)

## Create objects in a lakehouse or warehouse

- Ingest data by using a data pipeline, dataflow, or notebook
    
    - General
        - [Microsoft Fabric decision guide: copy activity, dataflow, or Spark](https://learn.microsoft.com/en-us/fabric/get-started/decision-guide-pipeline-dataflow-spark)
    - Data pipelines
        - [Quickstart: Create your first pipeline to copy data](https://learn.microsoft.com/en-us/fabric/data-factory/create-first-pipeline-with-sample-data)
        - [How to monitor activity in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/monitor-data-factory)
        - [How to monitor data pipeline runs in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/monitor-pipeline-runs)
        - [Migrate to Data Factory in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/upgrade-paths)
        - [Data Factory end-to-end scenario: introduction and architecture](https://learn.microsoft.com/en-us/fabric/data-factory/tutorial-end-to-end-introduction)
        - [Activity overview](https://learn.microsoft.com/en-us/fabric/data-factory/activity-overview)
        - [How to copy data using copy activity](https://learn.microsoft.com/en-us/fabric/data-factory/copy-data-activity)
        - [Copy activity performance and scalability guide](https://learn.microsoft.com/en-us/fabric/data-factory/copy-activity-performance-and-scalability-guide)
        - [Parameters for Data Factory in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/parameters)
        - [Concept: Data pipeline Runs](https://learn.microsoft.com/en-us/fabric/data-factory/pipeline-runs)
        - [Templates for Data Factory in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/templates)
        - [Incrementally load data from Data Warehouse to Lakehouse](https://learn.microsoft.com/en-us/fabric/data-factory/tutorial-incremental-copy-data-warehouse-lakehouse)
    - Dataflows
        - [What are dataflows?](https://learn.microsoft.com/en-us/power-query/dataflows/overview-dataflows-across-power-platform-dynamics-365)
        - [Ingest Data with Dataflows Gen2 in Microsoft Fabric](https://learn.microsoft.com/en-us/training/modules/use-dataflow-gen-2-fabric/)
        - [Quickstart: Create your first dataflow to get and transform data](https://learn.microsoft.com/en-us/fabric/data-factory/create-first-dataflow-gen2)
        - [A guide to learning Dataflows for Mapping Data Flow users](https://learn.microsoft.com/en-us/fabric/data-factory/guide-to-dataflows-for-mapping-data-flow-users)
        - [Getting from Dataflow Generation 1 to Dataflow Generation 2](https://learn.microsoft.com/en-us/fabric/data-factory/dataflows-gen2-overview)
        - [Data Factory Dataflow Gen2 limitations](https://learn.microsoft.com/en-us/fabric/data-factory/dataflow-gen2-limitations)
        - [Use a dataflow in a pipeline](https://learn.microsoft.com/en-us/fabric/data-factory/tutorial-dataflows-gen2-pipeline-activity)
        - [Pattern to incrementally amass data with Dataflow Gen2](https://learn.microsoft.com/en-us/fabric/data-factory/tutorial-setup-incremental-refresh-with-dataflows-gen2)
        - [What is Power Query?](https://learn.microsoft.com/en-us/power-query/power-query-what-is-power-query)
        - [On-premises data gateway considerations for data destinations in Dataflow Gen2](https://learn.microsoft.com/en-us/fabric/data-factory/gateway-considerations-output-destinations)
        - [Transform data with a dataflow in Data Factory](https://learn.microsoft.com/en-us/fabric/data-factory/tutorial-end-to-end-dataflow)
    - Notebooks
        - [Ingest data with Spark and Microsoft Fabric notebooks](https://learn.microsoft.com/en-us/training/modules/ingest-data-with-spark-fabric-notebooks/)
        - [Transform data by running a notebook](https://learn.microsoft.com/en-us/fabric/data-factory/notebook-activity)
- Create and manage shortcuts
    
    - [OneLake shortcuts](https://learn.microsoft.com/en-us/fabric/onelake/onelake-shortcuts)
    - [What are shortcuts in lakehouse?](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-shortcuts)
    - [Create a OneLake shortcut](https://learn.microsoft.com/en-us/fabric/onelake/create-onelake-shortcut)
    - [Access Fabric OneLake shortcuts in a Spark notebook](https://learn.microsoft.com/en-us/fabric/onelake/access-onelake-shortcuts)
    - [Create an Azure Data Lake Storage Gen2 shortcut](https://learn.microsoft.com/en-us/fabric/onelake/create-adls-shortcut)
    - [Create an Amazon S3 shortcut](https://learn.microsoft.com/en-us/fabric/onelake/create-s3-shortcut)
    - [Real-Time Analytics: Create OneLake shortcuts](https://learn.microsoft.com/en-us/fabric/real-time-analytics/onelake-shortcuts?tabs=onelake-shortcut)
    - [Link your Dataverse environment to Microsoft Fabric and unlock deep insights](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/azure-synapse-link-view-in-fabric)
    - [Tables over shortcuts](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-and-delta-tables)
- Implement file partitioning for analytics workloads in a lakehouse
    
    - [Data partitioning guidance](https://learn.microsoft.com/en-us/azure/architecture/best-practices/data-partitioning)
    - [Efficient Data Partitioning with Microsoft Fabric: Best Practices and Implementation Guide](https://techcommunity.microsoft.com/t5/fasttrack-for-azure/efficient-data-partitioning-with-microsoft-fabric-best-practices/ba-p/3890097)
    - [Better together: the lakehouse and warehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/get-started-lakehouse-sql-analytics-endpoint)
    - [Configure Lakehouse in a copy activity](https://learn.microsoft.com/en-us/fabric/data-factory/connector-lakehouse-copy-activity)
    - [Configure Data Warehouse in a copy activity](https://learn.microsoft.com/en-us/fabric/data-factory/connector-data-warehouse-copy-activity)
    - [Get streaming data into lakehouse with Spark structured streaming](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-streaming-data)
    - [What is autotune for Apache Spark configurations in Fabric and how to enable and disable it?](https://learn.microsoft.com/en-us/fabric/data-engineering/autotune?tabs=sparksql)
    - [Implement medallion lakehouse architecture in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/onelake/onelake-medallion-lakehouse-architecture)
    - [The need for optimize write on Apache Spark](https://learn.microsoft.com/en-us/azure/synapse-analytics/spark/optimize-write-for-apache-spark)
- Create views, functions, and stored procedures
    
    - [What is the SQL analytics endpoint for a Lakehouse?](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-sql-analytics-endpoint)
    - [Query using the visual query editor](https://learn.microsoft.com/en-us/fabric/data-warehouse/visual-query-editor)
    - [Query using the SQL query editor](https://learn.microsoft.com/en-us/fabric/data-warehouse/sql-query-editor)
    - [View data in the Data preview in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-warehouse/data-preview)
    - [Transact-SQL reference (Database Engine)](https://learn.microsoft.com/en-us/sql/t-sql/language-reference?view=fabric&preserve-view=true)
    - [What are the SQL database functions?](https://learn.microsoft.com/en-us/sql/t-sql/functions/functions?view=fabric)
    - [CREATE PROCEDURE (Transact-SQL)](https://learn.microsoft.com/en-us/sql/t-sql/statements/create-procedure-transact-sql?view=fabric)
    - [What is data warehousing in Microsoft Fabric?](https://learn.microsoft.com/en-us/fabric/data-warehouse/data-warehousing)
    - [How to use Stored procedure activity](https://learn.microsoft.com/en-us/fabric/data-factory/stored-procedure-activity)
    - [Tutorial: Transform data using a stored procedure](https://learn.microsoft.com/en-us/fabric/data-warehouse/tutorial-transform-data)
- Enrich data by adding new columns or tables
    
    - [Transform data with a dataflow in Data Factory](https://learn.microsoft.com/en-us/fabric/data-factory/tutorial-end-to-end-dataflow)

## Copy data

- Choose an appropriate method for copying data from a Fabric data source to a lakehouse or warehouse
    
    - [Microsoft Fabric decision guide: copy activity, dataflow, or Spark](https://learn.microsoft.com/en-us/fabric/get-started/decision-guide-pipeline-dataflow-spark)
- Copy data by using a data pipeline, dataflow, or notebook
    
    - see above
- Add stored procedures, notebooks, and dataflows to a data pipeline
    
    - [How to use Stored procedure activity](https://learn.microsoft.com/en-us/fabric/data-factory/stored-procedure-activity)
    - [Use the Dataflow activity to run a Dataflow Gen2](https://learn.microsoft.com/en-us/fabric/data-factory/dataflow-activity)
    - [Transform data by running a notebook](https://learn.microsoft.com/en-us/fabric/data-factory/notebook-activity)
- Schedule data pipelines, dataflows and notebooks
    
    - [Concept: Data pipeline Runs](https://learn.microsoft.com/en-us/fabric/data-factory/pipeline-runs)
    - [Use the Invoke pipeline activity to run another pipeline](https://learn.microsoft.com/en-us/fabric/data-factory/invoke-pipeline-activity)

## Transform data

- Implement a data cleansing process
    
    - [What is the medallion lakehouse architecture?](https://learn.microsoft.com/en-us/azure/databricks/lakehouse/medallion)
    - [Organize a Fabric lakehouse using medallion architecture design](https://learn.microsoft.com/en-us/training/modules/describe-medallion-architecture/)
    - [Power BI usage scenarios: Advanced data preparation](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-usage-scenario-advanced-data-preparation)
    - [Use Python in Power Query Editor](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-python-in-query-editor)
- Implement a star schema for a lakehouse or warehouse, including Type 1 and Type 2 slowly changing dimensions
    
    - [Understand star schema and the importance for Power BI](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema)
    - [Best practices for creating a dimensional model using dataflows](https://learn.microsoft.com/en-us/power-query/dataflows/best-practices-for-dimensional-model-using-dataflows)
    - [Populate slowly changing dimensions in Azure Synapse Analytics pipelines](https://learn.microsoft.com/en-us/training/modules/populate-slowly-changing-dimensions-azure-synapse-analytics-pipelines/)
- Implement bridge tables for a lakehouse or a warehouse
    
    - [Many-to-many relationship guidance](https://learn.microsoft.com/en-us/power-bi/guidance/relationships-many-to-many)
- Denormalize data
    
    - [Normalization vs. denormalization](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#normalization-vs-denormalization)
- Aggregate or de-aggregate data
    
    - [User-defined aggregations](https://learn.microsoft.com/en-us/power-bi/transform-model/aggregations-advanced)
    - [Automatic aggregations](https://learn.microsoft.com/en-us/power-bi/enterprise/aggregations-auto)
- Merge or join data
    
    - [Append queries](https://learn.microsoft.com/en-us/power-query/append-queries)
    - [Merge queries overview](https://learn.microsoft.com/en-us/power-query/merge-queries-overview)
    - [Tutorial: Shape and combine data in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-shape-and-combine-data)
    - [One-to-one relationship guidance](https://learn.microsoft.com/en-us/power-bi/guidance/relationships-one-to-one)
    - [Many-to-many relationship guidance](https://learn.microsoft.com/en-us/power-bi/guidance/relationships-many-to-many)
    - [Active vs inactive relationship guidance](https://learn.microsoft.com/en-us/power-bi/guidance/relationships-active-inactive)
- Identify and resolve duplicate data, missing data, or null values
    
    - [Using the data profiling tools](https://learn.microsoft.com/en-us/power-query/data-profiling-tools)
    - [Working with duplicate values](https://learn.microsoft.com/en-us/power-query/working-with-duplicates)
    - [Dealing with errors in Power Query](https://learn.microsoft.com/en-us/power-query/dealing-with-errors)
    - [Replace values and errors](https://learn.microsoft.com/en-us/power-query/replace-values)
- Convert data types by using SQL or PySpark
    
    - [Data types in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-warehouse/data-types)
    - [CAST and CONVERT (Transact-SQL)](https://learn.microsoft.com/en-us/sql/t-sql/functions/cast-and-convert-transact-sql?view=fabric)
    - [Conversion Functions (Transact-SQL)](https://learn.microsoft.com/en-us/sql/t-sql/functions/conversion-functions-transact-sql?view=fabric)
    - [PySpark – Cast Column Type With Examples](https://sparkbyexamples.com/pyspark/pyspark-cast-column-type/)
- Filter data
    
    - [Spark DataFrame Where Filter | Multiple Conditions](https://sparkbyexamples.com/spark/spark-dataframe-where-filter/)
    - [WHERE (Transact-SQL)](https://learn.microsoft.com/en-us/sql/t-sql/queries/where-transact-sql?view=fabric)
    - [Filter by values in a column](https://learn.microsoft.com/en-us/power-query/filter-values)

## Optimize performance

- Identify and resolve data loading performance bottlenecks in dataflows, notebooks, and SQL queries
    
    - [Copy activity performance and scalability guide](https://learn.microsoft.com/en-us/fabric/data-factory/copy-activity-performance-and-scalability-guide)
    - [On-premises data gateway considerations for data destinations in Dataflow Gen2](https://learn.microsoft.com/en-us/fabric/data-factory/gateway-considerations-output-destinations))
    - [Query insights in Fabric data warehousing](https://learn.microsoft.com/en-us/fabric/data-warehouse/query-insights)
    - [Monitor connections, sessions, and requests using DMVs](https://learn.microsoft.com/en-us/fabric/data-warehouse/monitor-using-dmv)
    - [Billing and utilization reporting in Synapse Data Warehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/usage-reporting)
    - [Query folding guidance in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/guidance/power-query-folding)
- Implement performance improvements in dataflows, notebooks, and SQL queries
    
    - [Troubleshoot pipelines for Data Factory in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/pipeline-troubleshoot-guide)
    - [Statistics in Fabric data warehousing](https://learn.microsoft.com/en-us/fabric/data-warehouse/statistics)
    - [Caching in Fabric data warehousing](https://learn.microsoft.com/en-us/fabric/data-warehouse/caching)
    - [Burstable capacity in Fabric data warehousing](https://learn.microsoft.com/en-us/fabric/data-warehouse/burstable-capacity)
    - [Smoothing and throttling in Fabric Data Warehousing](https://learn.microsoft.com/en-us/fabric/data-warehouse/compute-capacity-smoothing-throttling)
    - [Workload management](https://learn.microsoft.com/en-us/fabric/data-warehouse/workload-management)
    - [Synapse Data Warehouse in Microsoft Fabric performance guidelines](https://learn.microsoft.com/en-us/fabric/data-warehouse/guidelines-warehouse-performance)
- Identify and resolve issues with Delta table file sizes
    
    - [Review Delta Lake table details with describe detail](https://learn.microsoft.com/en-us/azure/databricks/delta/table-details)
    - [Delta Lake table optimization and V-Order](https://learn.microsoft.com/en-us/fabric/data-engineering/delta-optimization-and-v-order?tabs=sparksql)
    - [Use table maintenance feature to manage delta tables in Fabric](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-table-maintenance)
    - [The need for optimize write on Apache Spark](https://learn.microsoft.com/en-us/azure/synapse-analytics/spark/optimize-write-for-apache-spark)
    - [Best practices](https://docs.delta.io/latest/best-practices.html)

# Implement and manage semantic models (20–25%)

## Design and build semantic models

- Choose a storage mode, including Direct Lake
    
    - [Semantic model modes in the Power BI service](https://learn.microsoft.com/en-us/power-bi/connect-data/service-dataset-modes-understand)
    - [Manage storage mode in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-storage-mode)
    - [Direct Lake](https://learn.microsoft.com/en-us/power-bi/enterprise/directlake-overview)
    - [Analyze query processing for Direct Lake datasets](https://learn.microsoft.com/en-us/power-bi/enterprise/directlake-analyze-qp)
    - [How direct lake mode works with Power BI reporting](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-pbi-reporting)
    - [Default Power BI semantic models in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-warehouse/semantic-models)
- Identify use cases for DAX Studio and Tabular Editor 2
    
    - [External tools in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-external-tools)
    - [Power BI implementation planning: User tools and devices](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-user-tools-devices)
    - [Power BI implementation planning: Data-level auditing](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-auditing-monitoring-data-level-auditing)
    - [Power BI usage scenarios: Advanced data model management](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-usage-scenario-advanced-data-model-management)
    - [Power BI usage scenarios: Enterprise content publishing](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-usage-scenario-enterprise-content-publishing)
- Implement a star schema for a semantic model
    
    - [Understand star schema and the importance for Power BI](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema)
    - [Slowly changing dimensions](https://en.wikipedia.org/wiki/Slowly_changing_dimension)
- Implement relationships, such as bridge tables and many-to-many relationships
    
    - [Many-to-many relationship guidance](https://learn.microsoft.com/en-us/power-bi/guidance/relationships-many-to-many)
- Write calculations that use DAX variables and functions, such as iterators, table filtering, windowing, and information functions
    
    - [Use DAX iterator functions in Power BI Desktop models](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-iterator-functions/)
    - [Modify DAX filter context in Power BI Desktop models](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-modify-filter/)
    - [WINDOW](https://learn.microsoft.com/en-us/dax/window-function-dax)
    - [WINDOW](https://dax.guide/window/)
    - [Window Functions](https://powerdobs.nl/blog/new-in-dax-window-functions/)
    - [Information functions](https://learn.microsoft.com/en-us/dax/information-functions-daxs)
- Implement calculation groups, dynamic strings, and field parameters
    
    - [Create calculation groups](https://learn.microsoft.com/en-us/power-bi/transform-model/calculation-groups)
    - [Create dynamic format strings for measures](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-dynamic-format-strings)
    - [Let report readers use field parameters to change visuals (preview)](https://learn.microsoft.com/en-us/power-bi/create-reports/power-bi-field-parameters)
- Design and build a large format dataset
    
    - [Large semantic models in Power BI Premium](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-large-models)
- Design and build composite models that include aggregations
    
    - [Use composite models in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-composite-models)
    - [Composite model guidance in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/guidance/composite-model-guidance)
    - [User-defined aggregations](https://learn.microsoft.com/en-us/power-bi/transform-model/aggregations-advanced)
    - [Automatic aggregations](https://learn.microsoft.com/en-us/power-bi/enterprise/aggregations-auto)
- Implement dynamic row-level security and object-level security
    
    - [Row-level security (RLS) with Power BI](https://learn.microsoft.com/en-us/power-bi/enterprise/service-admin-rls)
    - [Row-level security (RLS) guidance in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/guidance/rls-guidance)
    - [USERPRINCIPALNAME()](https://learn.microsoft.com/en-us/dax/userprincipalname-function-dax)
    - [Object level security (OLS)](https://learn.microsoft.com/en-us/power-bi/enterprise/service-admin-ols?tabs=table)
- Validate row-level security and object-level security
    
    - See above

## Optimize enterprise-scale semantic models

- Implement performance improvements in queries and report visuals
    
    - [Optimization guide for Power BI](https://learn.microsoft.com/en-us/power-bi/guidance/power-bi-optimization)
    - [Optimize ribbon in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-optimize-ribbon)
    - [DirectQuery optimization scenarios with the Optimize ribbon](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-optimize-ribbon-scenarios)
    - [Use Performance Analyzer to examine report element performance in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-performance-analyzer)
    - [Power BI implementation planning: Data-level auditing](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-auditing-monitoring-data-level-auditing)
- Improve DAX performance by using DAX Studio
    
    - [Troubleshoot DAX performance by using DAX Studio](https://learn.microsoft.com/en-us/training/modules/use-tools-optimize-power-bi-performance/3-troubleshoot-dax-performance-use-dax-studio)
- Optimize a semantic model by using Tabular Editor 2
    
    - [Best Practice Analyzer](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-auditing-monitoring-data-level-auditing)
- Implement incremental refresh
    
    - [Incremental refresh and real-time data for semantic models](https://learn.microsoft.com/en-us/power-bi/connect-data/incremental-refresh-overview)
    - [Configure incremental refresh and real-time data](https://learn.microsoft.com/en-us/power-bi/connect-data/incremental-refresh-configure)
    - [Advanced incremental refresh and real-time data with the XMLA endpoint](https://learn.microsoft.com/en-us/power-bi/connect-data/incremental-refresh-xmla)
    - [Troubleshoot incremental refresh and real-time data](https://learn.microsoft.com/en-us/power-bi/connect-data/incremental-refresh-troubleshoot)

# Explore and analyze data (20–25%)

## Perform exploratory analytics

- Implement descriptive and diagnostic analytics
    
    - [Understand star schema and the importance for Power BI](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema)
    - [Create and view decomposition tree visuals in Power BI](https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-decomposition-tree)
    - [Tutorial: Create a decomposition tree with a Power BI sample](https://learn.microsoft.com/en-us/power-bi/create-reports/sample-tutorial-decomp-tree)
- Integrate prescriptive and predictive analytics into a visual or report
    
    - [Use the Analytics pane in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-analytics-pane)
    - [Build a machine learning model in Power BI](https://learn.microsoft.com/en-us/power-bi/connect-data/service-tutorial-build-machine-learning-model)
    - [Consume Azure Machine Learning models in Power BI](https://learn.microsoft.com/en-us/power-bi/connect-data/service-aml-integrate)
- Profile data
    
    - [Using the data profiling tools](https://learn.microsoft.com/en-us/power-query/data-profiling-tools)
    - [ydata-profiling](https://github.com/ydataai/ydata-profiling)

## Query data by using SQL

- Query a lakehouse in Fabric by using SQL queries or the visual query editor
    
    - [SQL analytics endpoint of the Lakehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/data-warehousing#sql-analytics-endpoint-of-the-lakehouse)
- Query a warehouse in Fabric by using SQL queries or the visual query editor
    
    - [Query using the visual query editor](https://learn.microsoft.com/en-us/fabric/data-warehouse/visual-query-editor)
    - [Query using the SQL query editor](https://learn.microsoft.com/en-us/fabric/data-warehouse/sql-query-editor)
    - [Create cross-warehouse queries with the SQL query editor](https://learn.microsoft.com/en-us/fabric/data-warehouse/tutorial-sql-cross-warehouse-query-editor)
- Connect to and query datasets by using the XMLA endpoint
    
    - [Integration tenant settings](https://learn.microsoft.com/en-us/fabric/admin/service-admin-portal-integration)
    - [Datasets - Execute Queries](https://learn.microsoft.com/en-us/rest/api/power-bi/datasets/execute-queries)
    - [EVALUATE](https://learn.microsoft.com/en-us/dax/evaluate-statement-dax)