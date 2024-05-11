# Introduction

Azure AI Document Intelligence uses Azure AI Services to analyze the content of scanned forms and convert them into data. It can recognize text values in both common forms and forms that are unique to your business.

In this module, we consider this scenario: You work for a company that conducts polls for private companies and political parties. Participants submit their responses as paper forms or as online PDFs. You currently spend a lot of time and money entering these responses into databases. You want to assess Azure AI Document Intelligence to find out if you can use it to streamline this process.

In this module, you'll learn about the architecture of Azure AI Document Intelligence and how to design a solution that can ingest data from forms into a data store.

## Learning objectives:

At the end of this module, you'll be able to:

- Describe the components of an Azure AI Document Intelligence solution.
- Create and connect to Azure AI Document Intelligence resources in Azure.
- Choose whether to use a prebuilt, custom, or composed model.
# Understand AI Document Intelligence

Azure AI Document Intelligence is easy to use but, to create a reliable solution, you must understand its objects such as models, APIs, and tools.

In your polling company, you're assessing Azure AI Document Intelligence to see if it can streamline your data entry workflow. You need to understand what data Azure AI Document Intelligence can obtain from the different polling forms you use and how your development team will build a AI data entry system and integrate it with your mobile and desktop apps and databases.

In this unit, you'll learn what Azure AI Document Intelligence does and how developers can configure it to support their forms and documents.

## What is Azure AI Document Intelligence?

Until recently, getting data from a completed form into a database or any other data store required someone to enter it manually. Manual data entry is a slow and intensive task and can be expensive, especially if you have thousands of forms to enter. Operators often make reading or typing errors that reduce the accuracy of your data.

Manual data entry was the only option because it was difficult for computers to recognize printed or hand-written text. Now, AI has become commonplace and has enabled computers to recognize patterns, such as letter shapes in a piece of text, with a high degree of accuracy. We can use AI as an alternative to manual data entry with lower costs and fewer errors in the extracted data.

Azure AI Document Intelligence is an Azure service that you can use to analyze forms completed by your customers, partners, employers, or others and extract the data that they contain.

![Screenshot showing that Azure AI Document Intelligence is an Azure service and can be found in the Azure Marketplace.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/02-search-marketplace.png)

## Responsible use of AI

AI technologies are powerful and have the potential to make great impacts on people's lives. To ensure that such impacts are positive, Microsoft uses the following principles when it designs and builds AI solutions. You should consider these principles whenever you make use of AI:

- **Fairness.** All AI systems should treat people fairly, regardless of race, belief, gender, sexuality, or other factors.
- **Reliability and safety.** All AI systems should give reliable answers with quantifiable confidence levels.
- **Privacy and security.** All AI systems should secure and protect sensitive data and operate within applicable data protection laws.
- **Inclusiveness.** All AI systems should be available to all users, regardless of their abilities.
- **Transparency.** All AI systems should operate understandably and openly.
- **Accountability.** All AI systems should be run by people who are accountable for the actions of those systems.

To conform to these principals, first you should take time to understand the AI system you're using and comprehend what it can do. For example, when using Document Intelligence, make sure you test your solution thoroughly with the forms you want it to read to ensure it extracts the data you expect. Ensure you collect only the data you need in forms and have the user's consent to store and analyze their information. Obtain legal advice on your solution, especially if the data it handles is personal or sensitive. Continue to use human agents to check on the deployed system and ensure your administrators can intervene in the solution to prevent harm. Continuously check the security of the system and its resilience against malicious attack and accidental data loss.

## Using models with Azure AI Document Intelligence

Use a model to inform Azure AI Document Intelligence about the type of data you expect to be in the documents you're analyzing. If your forms have a common structure or layout, you can increase the accuracy of the results and control the structure of the output data by using the most appropriate model. Azure AI Document Intelligence outputs data in JSON format, which is widely compatible with many databases, other storage locations, and programming languages.

Azure AI Document Intelligence includes several prebuilt models for common types of forms and documents. If your forms are of one of these types, you can extract information from them without training your own custom models. It's very quick to create and deploy an Azure AI Document Intelligence solution when you use prebuilt models.

In Azure AI Document Intelligence, three of the prebuilt models are for general document analysis:

- Read
- General document
- Layout

The other prebuilt models expect a common type of form or document:

- Invoice
- Receipt
- W-2 US tax declaration
- ID Document
- Business card
- Health insurance card

Important

This list shows the documented prebuilt models avaiable at the time of writing. More prebuilt models are in development will be deployed soon. Check the Azure AI Document Intelligence documentation for the latest models.

If you have an unusual or unique type of form, you can use the above general document analysis prebuilt models to extract information from them. However, if you want to extract more specific information than the prebuilt models support, you can create a **custom model** and train it by using examples of completed forms.

You can also associate multiple custom models, trained on different types of document, into a single model, known as a **composed model**. With a composed model, users can submit forms of different types to a single service, which identifies them and selects the most appropriate custom model to use in their analysis.

## Azure AI Document Intelligence and Azure AI Vision

As an Azure AI Service, Azure AI Document Intelligence is a high-level AI service that enables developers to access data in forms quickly. It's built on the lower level Azure AI Services, including Azure AI Vision.

If you use Azure AI Vision with its Optical Character Recognition (OCR) feature, you can submit photographed or scanned documents and extract their words and text in JSON format. This functionality is similar to Azure AI Document Intelligence and can make it difficult to choose from these services.

If you want to extract simple words and text from a picture of a form or document, without contextual information, Azure AI Vision OCR is an appropriate service to consider. You might want to use this service if you already have your own analysis code, for example. However, Azure AI Document Intelligence includes a more sophisticated analysis of documents. For example, it can identify key/value pairs, tables, and context-specific fields. If you want to deploy a complete document analysis solution that enables users to both extract and understand text, consider Azure AI Document Intelligence.

## Azure AI Document Intelligence tools

If you want to try many features of Azure AI Document Intelligence without writing any code, you can use [**Azure AI Document Intelligence Studio**](https://formrecognizer.appliedai.azure.com/). This provides a visual tool for exploring and understanding the capabilities of Azure AI Document Intelligence and its support for your forms.

For example, you can use Azure AI Document Intelligence Studio to try analyzing your sales invoices and to explore the data produced by the **Invoice** prebuilt model. Then you could decide whether the prebuilt model extracts the values you need or whether to create your own custom model for a more unusual type of invoice.

To integrate Azure AI Document Intelligence into your own applications you'll need to write code. For example, you could enable users of your sales mobile app to scan receipts with their device's camera and call Azure AI Document Intelligence to obtain prices, costs, and custom details. The app could store this information in your customer relationship management database.

Azure AI Document Intelligence includes Application Programming Interfaces (APIs) for each of the model types you've seen. The following languages are supported:

- C#/.NET
- Java
- Python
- JavaScript

If you prefer to use another language, you can call Azure AI Document Intelligence by using its RESTful web service.

## Learn more

- [What is Azure AI Document Intelligence?](https://learn.microsoft.com/en-us/azure/applied-ai-services/form-recognizer/overview)
- [Guidance for integration and responsible use with Azure AI Document Intelligence](https://learn.microsoft.com/en-us/legal/cognitive-services/document-intelligence/guidance-integration-responsible-use?toc=%2Fazure%2Fai-services%2Fdocument-intelligence%2Ftoc.json&bc=%2Fazure%2Fai-services%2Fdocument-intelligence%2Fbreadcrumb%2Ftoc.json)
- [Azure AI Document Intelligence models](https://learn.microsoft.com/en-us/azure/applied-ai-services/form-recognizer/concept-model-overview)
- [Azure AI Document Intelligence Studio (preview)](https://learn.microsoft.com/en-us/azure/applied-ai-services/form-recognizer/concept-form-recognizer-studio)
# Plan Azure AI Document Intelligence resources

Completed 100 XP

- 4 minutes

Choose your development language

To build an Azure AI Document Intelligence solution, you must create and configure the necessary resources in your Azure subscription.

In your polling company, you're assessing Azure AI Document Intelligence to see if it can streamline your data entry workflow. You've decided to deploy an Azure AI Document Intelligence solution that will analyze data from your polling forms and you must plan the deployment to support your requirements. You want to know what resources to create in your Azure subscription.

In this unit, you'll learn how to choose and create Azure AI Document Intelligence resources.

## Azure AI Document Intelligence resources

Azure AI Document Intelligence is an Azure service and conforms to Azure's resource management model. To create an Azure AI Document Intelligence solution, you start by adding a resource to your Azure subscription. When you create an Azure AI Document Intelligence resource, you can choose from **Free (F0)** or **Standard (S0)** tiers.

Important

If you're using the **Standard** tier, and find your requests are being throttled, you can submit an Azure Support Request to have the default limits increased. The **Free** tier is not available if you are using a multi-service resource.

## Create an Azure AI Document Intelligence resource

To create an Azure AI Document Intelligence resource in Azure and obtain connection details, complete these steps:

1. In the [Azure portal](https://portal.azure.com/#home), select **Create a resource**.
2. In the **Search services and marketplace** box, type **Document Intelligence** and then press **Enter**.
3. In the **Document intelligence** page, select **Create**.
4. In the **Create Document intelligence** page, under **Project Details**, select your **Subscription** and either select an existing **Resource group** or create a new one.
5. Under **Instance details**, select a **Region** near your users.
6. In the **Name** textbox, type a unique name for the resource.
7. Select a **Pricing tier** and then select **Review + create**.
8. If the validation tests pass, select **Create**. Azure deploys the new Azure AI Document Intelligence resource.

## Connect to Azure AI Document Intelligence

When you write an application that uses Azure AI Document Intelligence, you need two pieces of information to connect to the resource:

- **Endpoint.** This is the URL where the resource can be contacted.
- **Access key.** This is unique string that Azure uses to authenticate the call to Azure AI Document Intelligence.

To obtain these details:

1. In the [Azure portal](https://portal.azure.com/#home), navigate to the Azure AI Document Intelligence resource.
2. Under **Resource Management**, select **Keys and Endpoint**.
3. Copy either **KEY 1** or **KEY 2** and the **Endpoint** values and store them for use in your application code.

The following code shows how to use these connection details to connect your application to Azure AI Document Intelligence. In this example, a sample document at a specified URL is submitted for analysis to the general document model. Replace `<endpoint>` and `<access-key>` with the connection details you obtained from the Azure portal:

Python

```
from azure.core.credentials import AzureKeyCredential
from azure.ai.documentintelligence import DocumentIntelligenceClient
from azure.ai.documentintelligence.models import AnalyzeResult

endpoint = "<your-endpoint>"
key = "<your-key>"

docUrl = "<url-of-document-to-analyze>"

document_analysis_client = DocumentIntelligenceClient(endpoint=endpoint, 
    credential=AzureKeyCredential(key))

poller = document_analysis_client.begin_analyze_document_from_url(
    "prebuilt-document", docUrl)
result: AnalyzeResult = poller.result()
```

## Learn more

- [Create an Azure AI Document Intelligence resource](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/create-document-intelligence-resource)
- [Azure AI Document Intelligence Quickstart](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/quickstarts/get-started-sdks-rest-api)
- [Azure AI Document Intelligence service Quotas and Limits](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/service-limits)
# Choose a model type

Azure AI Document Intelligence uses models to describe the documents and forms to expect. You can either use one of the prebuilt models, if you have a common type of document, or create and train your own models.

In your polling company, you use many different forms for surveys for different clients. They have some fields in common, such as "Respondent Name" and "Contact Telephone" but other fields are unique to each client company or party. You want to choose which models to use in your Document Intelligence solution and plan how to create them.

In this unit, you'll learn about the prebuilt models available in Azure AI Document Intelligence and when to create your own custom and composed models.

## Prebuilt models

Document types such as invoices and receipts vary in different businesses and industry but have similar structures and key-value pairs. For example, a "Total cost" value is likely to appear on almost all invoices although it might be called "Total", "Sum", or some other name. Microsoft has provided a set of prebuilt models with Azure AI Document Intelligence to handle the most common types of documents. You don't have to train these models and you can create solutions using them very quickly.

### General document analysis models

Three of the prebuilt models are designed to handle general documents and extract words, lines, structure and other information such as the language the document is written in:

- **Read.** Use this model to extract words and lines from both printed and hand-written documents. It also detects the language used in the document.
    
    [![Screenshot showing the read model analyzing a document in German in Azure AI Document Intelligence Studio.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-read-model.png)](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-read-model.png#lightbox)
    
- **General document.** Use this model to extract key-value pairs and tables in your documents.
    
    [![Screenshot showing the general document model analyzing a document in Azure AI Document Intelligence Studio.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-general-document-model.png)](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-general-document-model.png#lightbox)
    
- **Layout.** Use this model to extract text, tables, and structure information from forms. It can also recognize selection marks such as check boxes and radio buttons.
    
    [![Screenshot showing the layout model analyzing a document in Azure AI Document Intelligence Studio.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-layout-model.png)](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-layout-model.png#lightbox)
    

Note

The model screenshots above show Document Intelligence models extracting data in Azure AI Document Intelligence Studio.

### Specific document type models

The other prebuilt models are each designed to handle, and trained on, a specific and commonly used type of document. Some examples include:

- **Invoice.** Use this model to extract key information from sales invoices in English and Spanish.
    
    [![Screenshot showing the invoice model analyzing a document in Azure AI Document Intelligence Studio.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-invoice-model.png)](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-invoice-model.png#lightbox)
    
- **Receipt.** Use this model to extract data from printed and handwritten receipts.
    
    [![Screenshot showing the receipt model analyzing a document in Azure AI Document Intelligence Studio.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-receipt-model.png)](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-receipt-model.png#lightbox)
    
- **W-2.** Use this model to extract data from United States government's W-2 tax declaration form.
    
    [![Screenshot showing the W-2 model analyzing a document in Azure AI Document Intelligence Studio.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-w2-model.png)](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-w2-model.png#lightbox)
    
- **ID document.** Use this model to extract data from United States driver's licenses and international passports.
    
- **Business card.** Use this model to extract names and contact details from business cards.
    
    [![Screenshot showing the business card model analyzing a document in Azure AI Document Intelligence Studio.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-business-card-model.png)](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-business-card-model.png#lightbox)
    

## Custom models

If the prebuilt models don't suit your purposes, you can create a custom model and train it to analyze the specific type of document users will send to your Azure AI Document Intelligence service. The general document analyzer prebuilt models can extract rich information from these forms and you might be able to use them if your requirements are to obtain general data. However, by using a custom model, trained on forms with similar structures and key-value pairs, you will obtain more predictable and standardized results from your unusual form types.

To train a custom model, you must supply at least five examples of the completed form but the more examples you supply, the greater the confidence levels Azure AI Document Intelligence will return when it analyzes input. The more varied your documents are in terms of structure and terminology, the greater the number of example documents you will need to supply to train a reliable model. You can either supply a labeled dataset to describe the expected data or allow the model to identify key-value pairs and table data based on what it finds in the example forms. Also, make sure your training forms include examples that span the full range of possible input. For example, if you are expecting both hand-written and printed entries, include them both in your training.

Once you have trained a custom model in this way, Azure AI Document Intelligence can accurately and predictably identify information in your unique forms.

[![Screenshot showing how to train a custom model on business-specific example forms in Azure AI Document Intelligence Studio.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-train-custom-model.png)](https://learn.microsoft.com/en-gb/training/wwl-data-ai/plan-form-recognizer-solution/media/04-train-custom-model.png#lightbox)

There are two kinds of custom model:

- **Custom template models.** A custom template model is most appropriate when the forms you want to analyze have a consistent visual template. If you remove all the user-entered data from the forms and find that the blank forms are identical, use a custom template model. Custom template models support 9 different languages for handwritten text and a wide range of languages for printed text. If you have a few different variations of the form templates, train a model for each of the variations and then compose the models together into a single model. The service will invoke the model best suited to analyze the document.
- **Custom neural models.** A custom neural model can work across the spectrum of structured to unstructured documents. Documents like contracts with no defined structure or highly structured forms can be analyzed with a neural model. Neural models work on English with the highest accuracy and a marginal drop in accuracy for Latin based languages like German, French, Italian, Spanish, and Dutch. Try using the custom neural model first if your scenario is addressed by the model.

## Composed models

A composed model is one that consists of multiple custom models. Typical scenarios where composed models help are when you don't know the submitted document type and want to classify and then analyze it. They are also useful if you have multiple variations of a form, each with a trained individual model. When a user submits a form to the composed model, Document Intelligence automatically classifies it to determine which of the custom models should be used in its analysis. In this approach, a user doesn't have to know what kind of document it is before submission. That can be helpful when you're using lots of similar forms or when you want to publish a single endpoint for all your form types.

Important

The results from a composed model include the `docType` property, which indicates the custom model that was chosen to analyze each form.

If you're using the Standard pricing tier, you can add up to 100 custom models into a single composed model. If you're using the Free pricing tier, you can only add up to 5 custom models.

## Learn more

- [Azure AI Document Intelligence models](https://learn.microsoft.com/en-us/azure/applied-ai-services/form-recognizer/concept-model-overview)
- [Azure AI Document Intelligence custom models](https://learn.microsoft.com/en-us/azure/applied-ai-services/form-recognizer/concept-custom)
- [Composed custom models](https://learn.microsoft.com/en-us/azure/applied-ai-services/form-recognizer/concept-composed-models)