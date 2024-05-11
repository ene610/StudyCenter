# Introduction

Completed 100 XP

- 1 minute

Azure AI services provides a cloud-based platform for building artificial intelligence capabilities into your applications. Like any software service, you should monitor AI services to track costs, identify utilization trends, and detect potential issues.

After completing this module, you'll be able to:

- Monitor Azure AI services costs.
- Create alerts and view metrics for Azure AI services.
- Manage Azure AI services diagnostic logging.
# Monitor cost

Completed 100 XP

- 3 minutes

One of the main benefits of using cloud services is that you can gain cost efficiencies by only paying for services as you use them. Some Azure AI services resources offer a free tier with restrictions on use, which is useful for development and testing; and one or more billed tiers that incur charges based on transactions. The specific billing rate depends on the resource type.

## Plan costs for AI services

Before deploying a solution that depends on AI services, you can estimate costs by using the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).

To use the pricing calculator to estimate AI services costs, create a new estimate and select **Azure AI services** in the **AI + Machine Learning** category. Then select the specific AI service API you plan to use (for example, _Azure AI Text Analytics_), the region where you plan to provision it, and the pricing tier of the instance you plan to use; and fill in the expected usage metrics and support option. To create an estimate that includes multiple AI services APIs, add additional **Azure AI services** products to the estimate.

After you've created an estimate, you can save it. You can also export it in Microsoft Excel format.

## View costs for AI services

In common with other Azure resources, you can view details of accumulated costs for AI services resources in the Azure portal.

To view costs for AI services, sign into the Azure portal and select your subscription. You can then view overall costs for the subscription by selecting the **Cost analysis** tab. To view only costs for AI services, add a filter that restricts the data to reflect resources with a **service name** of **Cognitive Services**.

Note

For more information, see [Plan and manage costs for Azure AI services](https://learn.microsoft.com/en-us/azure/ai-services/plan-manage-costs) in the AI services documentation.

# Create alerts

Completed 100 XP

- 3 minutes

Microsoft Azure provides alerting support for resources through the creation of _alert rules_. You use alert rules to configure notifications and alerts for your resources based on events or metric thresholds. These alerts will ensure that the correct team knows when a problem arises.

![A screenshot of an alert in the Azure portal and an email.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/monitor-ai-services/media/alert.png)

## Alert rules

To create an alert rule for an Azure AI services resource, select the resource in the Azure portal and on the **Alerts** tab, add a new alert rule. To define the alert rule, you must specify:

- The _scope_ of the alert rule - in other words, the resource you want to monitor.
- A _condition_ on which the alert is triggered. The specific trigger for the alert is based on a _signal type_, which can be _Activity Log_ (an entry in the activity log created by an action performed on the resource, such as regenerating its subscription keys) or _Metric_ (a metric threshold such as the number of errors exceeding 10 in an hour).
- Optional _actions_, such as sending an email to an administrator notifying them of the alert, or running an Azure Logic App to address the issue automatically.
- _Alert rule details_, such as a name for the alert rule and the resource group in which it should be defined.

Note

For more information, see [Overview of alerts in Microsoft Azure](https://learn.microsoft.com/en-us/azure/azure-monitor/alerts/alerts-overview) in the Azure documentation.

# View metrics

Completed 100 XP

- 3 minutes

Azure Monitor collects metrics for Azure resources at regular intervals so that you can track indicators of resource utilization, health, and performance. The specific metrics gathered depend on the Azure resource. In the case of Azure AI services, Azure Monitor collects metrics relating to endpoint requests, data submitted and returned, errors, and other useful measurements.

## View metrics in the Azure portal

You can view metrics for an individual resource in the Azure portal by selecting the resource and viewing its **Metrics** page. On this page, you can add resource-specific metrics to charts. By default an empty chart is created for you, and you can add more charts as required.

For example, the following image shows the **Metrics** page for an AI services resource, showing the count of total calls to the service over a period of time.

![A screenshot showing metrics for an AI services resource.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/monitor-ai-services/media/metric.png)

You can add multiple metrics to a chart and choose appropriate aggregations and chart types. When you're satisfied with chart, you can _share_ it by exporting it to Excel or copying a link to it, and you can _clone_ it to create a duplicate chart in the **Metrics** page - potentially as a starting point for a new chart that shows the same metrics in a different way.

## Add metrics to a dashboard

In the Azure portal, you can create _dashboards_ that consist of multiple visualizations from different resources in your Azure environment to help you gain an overall view of the health and performance of your Azure resources.

To create a dashboard, select **Dashboard** in the Azure portal menu (your default view may already be set to a dashboard rather than the portal home page). From here, you can add up to 100 named dashboards to encapsulate views for specific aspects of your Azure services that you want to track.

You can add a range of tiles and other visualizations to a dashboard, and when viewing metrics for a specific resource in a chart, as described previously, you can add the chart to a new or existing dashboard. In the following image, two charts showing metrics for an AI services resource have been added to a dashboard.

![A screenshot showing metrics in a dashboard.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/monitor-ai-services/media/metric-dashboard.png)

Note

For more information about dashboards, see [Create a dashboard in the Azure portal](https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-dashboards) in the Azure documentation.

# Manage diagnostic logging

Completed 100 XP

- 3 minutes

Diagnostic logging enables you to capture rich operational data for an Azure AI services resource, which can be used to analyze service usage and troubleshoot problems.

## Create resources for diagnostic log storage

To capture diagnostic logs for an AI services resource, you need a destination for the log data. You can use Azure Event Hubs as a destination in order to then forward the data on to a custom telemetry solution, and you can connect directly to some third-party solutions; but in most cases you'll use one (or both) of the following kinds of resource within your Azure subscription:

- **Azure Log Analytics** - a service that enables you to query and visualize log data within the Azure portal.
- **Azure Storage** - a cloud-based data store that you can use to store log archives (which can be exported for analysis in other tools as needed).

You should create these resources before configuring diagnostic logging for your AI services resource. If you intend to archive log data to Azure Storage, create the Azure Storage account in the same region as your AI services resource.

## Configure diagnostic settings

With your log destinations in place, you can configure diagnostic settings for your AI services resource. You define diagnostic settings on the **Diagnostic settings** page of the blade for your AI services resource in the Azure portal. When you add diagnostic settings, you must specify:

- A name for your diagnostic settings.
- The categories of log event data that you want to capture.
- Details of the destinations in which you want to store the log data.

In the following example, the diagnostic settings store all available log data and metrics in Azure Log Analytics and Azure Storage.

![A screenshot of diagnostic settings for an Azure AI services resource.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/monitor-ai-services/media/diagnostic-settings.png)

## View log data in Azure Log Analytics

It can take an hour or more before diagnostic data starts flowing to the destinations, but when the data has been captured, you can view it in your Azure log Analytics resource by running queries, as shown in this example.

![A screenshot of an Azure log Analytics query returning diagnostic data logged for an Azure AI services resource.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/monitor-ai-services/media/azure-log-analytics.png)

Note

For more information, see [Enable diagnostic logging for Azure AI services](https://learn.microsoft.com/en-us/azure/ai-services/diagnostic-logging) in the Azure AI services documentation.