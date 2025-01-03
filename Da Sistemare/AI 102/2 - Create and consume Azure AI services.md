# Introduction

**Azure AI services** are cloud-based services that encapsulate AI capabilities. Rather than a single product, you should think of AI services as a set of individual services that you can use as building blocks to compose sophisticated, intelligent applications.

AI services includes a wide range of individual services across multiple categories, as shown in the following table.

|Language|Speech|Vision|Decision|
|---|---|---|---|
|Azure AI Language|Azure AI Speech|Azure AI Computer Vision|Azure AI Anomaly Detector|
|Azure AI Translator||Azure AI Custom Vision|Azure AI Content Moderator|
|||Azure AI Face|Azure AI Personalizer|

You can use AI services to build your own AI solutions to provide out-of-the-box solutions for common AI scenarios. Azure AI services include:

- **Azure AI Document Intelligence** - An optical character recognition (OCR) solution that can extract semantic meaning from forms, such as invoices, receipts, and others.
- **Azure AI Immersive Reader** - A reading solution that supports people of all ages and abilities.
- **Azure Cognitive Search** - A cloud-scale search solution that uses AI services to extract insights from data and documents.
- **Azure OpenAI** - An Azure Cognitive Service that provides access to the capabilities of OpenAI GPT-4.

While the details of each AI service can vary, the approach to provisioning and consuming them is generally the same.

In this module, you will learn how to:

- Create Azure AI services resources in an Azure subscription.
- Identify endpoints, keys, and locations required to consume an AI services resource.
- Use a REST API to consume an AI service.
- Use an SDK to consume an AI service.



# Provision an Azure AI services resource

Azure AI services include a wide range of AI capabilities that you can use in your applications. To use any of the AI services, you need to create appropriate resources in an Azure subscription to define an endpoint where the service can be consumed, provide access keys for authenticated access, and to manage billing for your application's usage of the service.

## Options for Azure resources

For many of the available AI services, you can choose between the following provisioning options:

### Multi-service resource

You can provision an **AI services** resource that supports multiple different AI services. For example, you could create a single resource that enables you to use the **Azure AI Language**, **Azure AI Vision**, **Azure AI Speech**, and other services.

This approach enables you to manage a single set of access credentials to consume multiple services at a single endpoint, and with a single point of billing for usage of all services.

### Single-service resource

Each AI service can be provisioned individually, for example by creating discrete **AI Language** and **AI Vision** resources in your Azure subscription.

This approach enables you to use separate endpoints for each service (for example to provision them in different geographical regions) and to manage access credentials for each service independently. It also enables you to manage billing separately for each service.

Single-service resources generally offer a free tier (with usage restrictions), making them a good choice to try out a service before using it in a production application.

## Training and prediction resources

While most AI services can be used through a single Azure resource, some offer (or require) separate resources for model _training_ and _prediction_. This enables you to manage billing for training custom models separately from model consumption by applications, and in most cases enables you to use a dedicated service-specific resource to train a model, but a generic **AI services** resource to make the model available to applications for inferencing.

# Identify endpoints and keys

When you provision an Azure AI services service resource in your Azure subscription, you are defining an endpoint through which the service can be consumed by an application.

To consume the service through the endpoint, applications require the following information:

- **The endpoint URI**. This is the HTTP address at which the REST interface for the service can be accessed. Most AI services software development kits (SDKs) use the endpoint URI to initiate a connection to the endpoint.
- **A subscription key**. Access to the endpoint is restricted based on a subscription key. Client applications must provide a valid key to consume the service. When you provision an AI services resource, two keys are created - applications can use either key. You can also regenerate the keys as required to control access to your resource.
- **The resource location**. When you provision a resource in Azure, you generally assign it to a location, which determines the Azure data center in which the resource is defined. While most SDKs use the endpoint URI to connect to the service, some require the location.

# Use a REST API

Azure AI services provide REST application programming interfaces (APIs) that client applications can use to consume services. In most cases, service functions can be called by submitting data in JSON format over an HTTP request, which may be a POST, PUT, or GET request depending on the specific function being called. The results of the function are returned to the client as an HTTP response, often with JSON contents that encapsulate the output data from the function.

![Diagram of an app submitting a JSON request to an Azure AI services REST API and receiving a JSON response.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/create-manage-ai-services/media/rest-api.png)

The use of REST interfaces with an HTTP endpoint means that any programming language or tool capable of submitting and receiving JSON over HTTP can be used to consume AI services. You can use common programming languages such as Microsoft C#, Python, and JavaScript; as well as utilities such as Postman and cURL, which can be useful for testing.



# Use an SDK

You can develop an application that uses Azure AI services using REST interfaces, but it's easier to build more complex solutions by using native libraries for the programming language in which you're developing the application.

![A diagram of an app submitting a call to an Azure AI services resource through a language-specific SDK, which abstracts the JSON request and response.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/create-manage-ai-services/media/sdk.png)

Software development kits (SDKs) for common programming languages abstract the REST interfaces for most AI services. SDK availability varies by individual AI services, but for most services there's an SDK for languages such as:

- Microsoft C# (.NET Core)
- Python
- JavaScript (Node.js)
- Go
- Java

Each SDK includes packages that you can install in order to use service-specific libraries in your code, and online documentation to help you determine the appropriate classes, methods, and parameters used to work with the service.