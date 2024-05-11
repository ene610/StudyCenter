# Introduction

Forms are used to communicate information in every industry, every day. Many people still manually extract data from forms to exchange information.

![Screenshot of person handing a form to another person.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/work-form-recognizer/media/introduction-image.png)

Consider some of the instances when a person needs to process form data:

- When filing claims
- When enrolling new patients in an online management system
- When entering data from receipts to an expense report
- When reviewing an operations report for anomalies
- When selecting data from a report to give to a stakeholder

Without AI services, people need to manually sort through form documents to identify important information and then manually reenter data to record it. Some may also need to complete these tasks in real-time with a customer.

Azure Document Intelligence services provide the building blocks for automation by using intelligent services to extract data at scale and with accuracy. _Azure Document Intelligence_ is a Vision API that extracts key-value pairs and table data from form documents.

**Uses of the Azure Document Intelligence service include**:

- Process automation
- Knowledge mining
- Industry-specific applications

**In this module, you'll learn how to**:

- Identify how Azure Document Intelligence's document analysis, prebuilt, and custom models can automate processes
- Use Azure Document Intelligence's Optical Character Recognition (OCR) capabilities with SDKs and REST API
- Develop and test a custom Azure Document Intelligence model

To complete this module, you'll need a Microsoft Azure subscription. If you don't already have one, you can sign up for a free trial at [https://azure.microsoft.com](https://azure.microsoft.com/).
# What is Azure Document Intelligence?

Completed 100 XP

- 4 minutes

Azure Document Intelligence is one of many Azure AI Services, cloud-based artificial intelligence (AI) services with REST APIs and client library SDKs that can be used to build intelligence into your applications.

Azure Document Intelligence uses Optical Character Recognition (OCR) capabilities and deep learning models to extract text, key-value pairs, selection marks, and tables from documents.

![Screenshot of how OCR works.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/work-form-recognizer/media/how-optical-character-recognition-works.png)

OCR captures document structure by creating bounding boxes around detected objects in an image. The locations of the bounding boxes are recorded as coordinates in relation to the rest of the page. Azure Document Intelligence services return bounding box data and other information in a structured form with the relationships from the original file.

![Screenshot of JSON output sample.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/work-form-recognizer/media/json-output-sample.png)

To build a high-accuracy model from scratch, people need to build deep learning models, use a large amount of compute resources, and face long model training times. These factors could make a project infeasible. Azure Document Intelligence provides underlying models that have been trained on thousands of form examples. The underlying models enable you to do high-accuracy data extraction from your forms with little to no model training.

## Azure Document Intelligence service components

Azure Document Intelligence is composed of the following services:

- **Document analysis models**: which take an input of JPEG, PNG, PDF, and TIFF files and return a JSON file with the location of text in bounding boxes, text content, tables, selection marks (also known as checkboxes or radio buttons), and document structure.
    
- **Prebuilt models**: which detect and extract information from document images and return the extracted data in a structured JSON output. Azure Document Intelligence currently supports prebuilt models for several forms, including:
    
    - W-2 forms
    - Invoices
    - Receipts
    - ID documents
    - Business cards
- **Custom models**: custom models extract data from forms specific to your business. Custom models can be trained through the [Azure Document Intelligence Studio](https://formrecognizer.appliedai.azure.com/studio).
    

Note

Some Azure Document Intelligence features are in preview, as of the time this content was authored, and as a result, features and usage details might change. You should refer to the [official page](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/overview) for up-to-date information.

## Access services with the client library SDKs or REST API

You can access Azure Document Intelligence services by using a REST API, client library SDKs, and through the Azure Document Intelligence Studio to integrate the services into your workflow or application.

Tip

This module's exercise focuses on the Python and .NET SDKs. The underlying REST services can be used by any language.

Check out the [documentation](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/quickstarts/get-started-sdks-rest-api) for quick start guides on all the available SDKs and the REST API.
# Get started with Azure Document Intelligence

To start a project with Azure Document Intelligence services, you need to prepare the following:

- An Azure resource subscription
- A selection of form files for data extraction

## Subscribe to a resource

You can access Azure Document Intelligence services via:

- An **Azure AI Service resource**: a multi-service subscription key (used across multiple Azure AI Services)

**OR**

- An **Azure Document Intelligence resource**: a single-service subscription key (used only with a specific Azure AI Service)

Note

Create an Azure AI Services resource if you plan to access multiple Azure AI services under a single endpoint/key. For Azure Document Intelligence access only, create an Azure Document Intelligence resource. Please note that you'll need a single-service resource if you intend to use Microsoft Entra authentication.

You can subscribe to a service in the Azure portal or with the Azure Command Line Interface (CLI). You can learn more about the CLI commands [here](https://learn.microsoft.com/en-us/cli/azure/cognitiveservices/account#commands).

## Understand Azure Document Intelligence file input requirements

Azure Document Intelligence works on input documents that meet these requirements:

- Format must be JPG, PNG, BMP, PDF (text or scanned), or TIFF.
- The file size must be less than 500 MB for paid (S0) tier and 4 MB for free (F0) tier.
- Image dimensions must be between 50 x 50 pixels and 10000 x 10000 pixels.
- The total size of the training data set must be 500 pages or less.

More input requirements can be found in the [documentation](https://learn.microsoft.com/en-us/azure/cognitive-services/form-recognizer/overview) for specific models.

## Decide what component of Azure Document Intelligence to use

After you have collected your files, decide what you need to accomplish.

- To use OCR capabilities to capture document analysis, use the [Layout model](https://learn.microsoft.com/en-us/azure/applied-ai-services/form-recognizer/concept-model-overview#layout), [Read model](https://learn.microsoft.com/en-us/azure/applied-ai-services/form-recognizer/concept-model-overview#read-preview), or [General Document model](https://learn.microsoft.com/en-us/azure/applied-ai-services/form-recognizer/concept-model-overview#general-document-preview).
    
- To create an application that extracts data from W-2s, Invoices, Receipts, ID documents, Health insurance, vaccination, and business cards, use a prebuilt model. These models do not need to be trained. Azure Document Intelligence services analyze the documents and return a JSON output.
    
- To create an application to extract data from your industry-specific forms, create a custom model. This model needs to be trained on sample documents. After training, the custom model can analyze new documents and return a JSON output.
# Train custom models

Azure's Azure Document Intelligence service supports supervised machine learning. You can train custom models and create composite models with form documents _and_ JSON documents that contain labeled fields.

![Screenshot of a sample form document needed for custom model training.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/work-form-recognizer/media/labeled-form-documents.png)

To train a custom model:

1. Store sample forms in an Azure blob container, along with JSON files containing layout and label field information.
    - You can generate an **ocr.json** file for each sample form using the Azure Document Intelligence's **Analyze document** function. Additionally, you need a single **fields.json** file describing the fields you want to extract, and a **labels.json** file for each sample form mapping the fields to their location in that form.
2. Generate a shared access security (SAS) URL for the container.
3. Use the **Build model** REST API function (or equivalent SDK method).
4. Use the **Get model** REST API function (or equivalent SDK method) to get the trained **model ID**.

**OR**

5. Use the Azure Document Intelligence Studio to label and train. There are two types of underlying models for custom forms _custom template models_ or _custom neural models_.
    - **Custom template models** accurately extract labeled key-value pairs, selection marks, tables, regions, and signatures from documents. Training only takes a few minutes, and more than 100 languages are supported.
    - **Custom neural models** are deep learned models that combine layout and language features to accurately extract labeled fields from documents.This model is best for semi-structured or unstructured documents.
# Use Azure Document Intelligence models

## Using the API

To extract form data using a custom model, use the **analyze document** function of either a supported SDK, or the REST API, while supplying model ID (generated during model training). This function starts the form analysis. which you can then request the result to get the analysis.

Example code to call your model:

**C#**

C#

```
string endpoint = "<endpoint>";
string apiKey = "<apiKey>";
AzureKeyCredential credential = new AzureKeyCredential(apiKey);
DocumentAnalysisClient client = new DocumentAnalysisClient(new Uri(endpoint), credential);

string modelId = "<modelId>";
Uri fileUri = new Uri("<fileUri>");

AnalyzeDocumentOperation operation = await client.AnalyzeDocumentFromUriAsync(WaitUntil.Completed, modelId, fileUri);
AnalyzeResult result = operation.Value;
```

**Python**

Python

```
endpoint = "YOUR_DOC_INTELLIGENCE_ENDPOINT"
key = "YOUR_DOC_INTELLIGENCE_KEY"

model_id = "YOUR_CUSTOM_BUILT_MODEL_ID"
formUrl = "YOUR_DOCUMENT"

document_analysis_client = DocumentAnalysisClient(
    endpoint=endpoint, credential=AzureKeyCredential(key)
)

# Make sure your document's type is included in the list of document types the custom model can analyze
task = document_analysis_client.begin_analyze_document_from_url(model_id, formUrl)
result = task.result()
```

A successful JSON response contains **analyzeResult** that contains the content extracted and an array of pages containing information about the document content.

Example **analyze document** JSON response:

JSON

```
{
	"status": "succeeded",
	"createdDateTime": "2023-10-18T23:39:50Z",
	"lastUpdatedDateTime": "2023-10-18T23:39:54Z",
	"analyzeResult": {
		"apiVersion": "2022-08-31",
		"modelId": "DocIntelModel",
		"stringIndexType": "utf16CodeUnit",
		"content": "Purchase Order\nHero Limited\nCompany Phone: 555-348-6512 Website: www.herolimited.com Email: accounts@herolimited.com\nPurchase Order\nDated As: 12/20/2020 Purchase Order #: 948284\nShipped To Vendor Name: Balozi Khamisi Company Name: Higgly Wiggly Books Address: 938 NE Burner Road Boulder City, CO 92848 Phone: 938-294-2949\nShipped From Name: Kidane Tsehaye Company Name: Jupiter Book Supply Address: 383 N Kinnick Road Seattle, WA 38383\nPhone: 932-299-0292\nDetails\nQuantity\nUnit Price\nTotal\nBindings\n20\n1.00\n20.00\nCovers Small\n20\n1.00\n20.00\nFeather Bookmark\n20\n5.00\n100.00\nCopper Swirl Marker\n20\n5.00\n100.00\nSUBTOTAL\n$140.00\nTAX\n$4.00\nTOTAL\n$144.00\nKidane Tsehaye\nManager\nKidane Tsehaye\nAdditional Notes: Do not Jostle Box. Unpack carefully. Enjoy. Jupiter Book Supply will refund you 50% per book if returned within 60 days of reading and offer you 25% off you next total purchase.",
		"pages": [
			{
				"pageNumber": 1,
				"angle": 0,
				"width": 1159,
				"height": 1486,
				"unit": "pixel",
				"words": [
					{
						"content": "Purchase",
						"polygon": [
							89,
							90,
							174,
							91,
							174,
							112,
							88,
							112
						],
						"confidence": 0.996,
						"span": {
							"offset": 0,
							"length": 8
						}
					},
					{
						"content": "Order",
						"polygon": [
							178,
							91,
							237,
							91,
							236,
							113,
							178,
							112
						],
						"confidence": 0.997,
						"span": {
							"offset": 9,
							"length": 5
						}
					},
                    ...
```

Explore the documentation for [supported language quickstarts](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/quickstarts/get-started-sdks-rest-api).

## Understanding confidence scores

If the confidence values of the **analyzeResult** are low, try to improve the quality of your input documents.

You want to make sure that the form you're analyzing has a similar appearance to forms in the training set if the confidence values are low. If the form appearance varies, consider training more than one model, with each model focused on one form format.

Depending on the use case, you might find that a confidence score of 80% or higher is acceptable for a low-risk application. For more sensitive cases, like reading medical records or billing statements, a score of 100% is recommended.
# Use the Azure Document Intelligence Studio

In addition to SDKs and the REST API, Azure Document Intelligence services can be accessed through a user interface called the Azure Document Intelligence Studio (preview), an online tool for visually exploring, understanding, and integrating features from the Azure Document Intelligence service. The Studio can be used to analyze form layouts, extract data from prebuilt models, and train custom models.

![Gif of Azure Document Intelligence Studio capabilities.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/work-form-recognizer/media/doc-intelligence-studio.png)

The Azure Document Intelligence Studio currently supports the following projects:

- **Document analysis models**
    - Read: Extract printed and handwritten text lines, words, locations, and detected languages from documents and images.
    - Layout: Extract text, tables, selection marks, and structure information from documents (PDF and TIFF) and images (JPG, PNG, and BMP).
    - General Documents: Extract key-value pairs, selection marks, and entities from documents.
- **Prebuilt models**
- **Custom models**

### Build Document analysis model projects

To extract text, tables, structure, key-value pairs, and named entities with document analysis models:

- Create an Azure Document Intelligence or Azure AI Services resource
- Select either "Read", "Layout", or "General Documents" under the Document analysis models category
- Analyze your document. You'll need your Azure Document Intelligence or Azure AI service endpoint and key.

### Build prebuilt model projects

To extract data from common forms with prebuilt models:

- Create an Azure Document Intelligence or Azure AI Services resource
- Select one of the "prebuilt models" including W-2s, Invoices, Receipts, ID documents, Health insurance, vaccination, and business cards.
- Analyze your document. You'll need your Azure Document Intelligence or Azure AI service endpoint and key.

### Build custom model projects

You can use Azure Document Intelligence Studio's custom service for the entire process of training and testing custom models.

When you use Azure Document Intelligence Studio to build custom models, the **ocr.json** files, **labels.json** files, and **fields.json** file needed for training are automatically created and stored in your storage account.

To train a custom model and use it to extract data with custom models:

- Create an Azure Document Intelligence or Azure AI Services resource
- Collect at least 5-6 sample forms for training and upload them to your storage account container.
- Configure cross-domain resource sharing (CORS). CORS enables Azure Document Intelligence Studio to store labeled files in your storage container.
- Create a custom model project in Azure Document Intelligence Studio. You'll need to provide configurations linking your storage container and Azure Document Intelligence or Azure AI Service resource to the project.
- Use Azure Document Intelligence Studio to apply labels to text.
- Train your model. Once the model is trained, you'll receive a Model ID and Average Accuracy for tags.
- Test your model by analyzing a new form that wasn't used in training.