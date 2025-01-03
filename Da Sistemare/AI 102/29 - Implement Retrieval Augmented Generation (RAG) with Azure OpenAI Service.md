# Introduction

Azure OpenAI enables developers to implement Retrieval Augmented Generation (RAG) by connecting supporting AI chat models to your own data. Those models can reference specific sources of data to ground the response, augmenting the capabilities of the AI model when it creates a response.

In this module, you'll learn how to implement RAG by adding your own data with Azure OpenAI and generate responses based on both that data.

Note

Azure OpenAI Access is restricted to Azure subscriptions for which access has been requested and approved. Users need to [apply for access](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/overview#how-do-i-get-access-to-azure-openai?azure-portal=true) and be approved before they can create an Azure OpenAI resource.
# Understand Retrieval Augmented Generation (RAG) with Azure OpenAI Service

RAG with Azure OpenAI allows developers to use supported AI chat models that can reference specific sources of information to ground the response. Adding this information allows the model to reference both the specific data provided and its pretrained knowledge to provide more effective responses.

Azure OpenAI enables RAG by connecting pretrained models to your own data sources. Azure OpenAI on your data utilizes the search ability of Azure AI Search to add the relevant data chunks to the prompt. Once your data is in a AI Search index, Azure OpenAI on your data goes through the following steps:

1. Receive user prompt.
2. Determine relevant content and intent of the prompt.
3. Query the search index with that content and intent.
4. Insert search result chunk into the Azure OpenAI prompt, along with system message and user prompt.
5. Send entire prompt to Azure OpenAI.
6. Return response and data reference (if any) to the user.

By default, Azure OpenAI on your data encourages, but doesn't require, the model to respond only using your data. This setting can be unselected when connecting your data, which may result in the model choosing to use its pretrained knowledge over your data.

## Fine-tuning vs. RAG

Fine-tuning is a technique used to create a custom model by training an existing foundational model such as `gpt-35-turbo` with a dataset of additional training data. Fine-tuning can result in higher quality requests than prompt engineering alone, customize the model on examples larger than can fit in a prompt, and allow the user to provide fewer examples to get the same high quality response. However, the process for fine-tuning is both costly and time intensive, and should only be used for use cases where it's necessary.

RAG with Azure OpenAI on your data still uses the stateless API to connect to the model, which removes the requirement of training a custom model with your data and simplifies the interaction with the AI model. AI Search first finds the useful information to answer the prompt, adds that to the prompt as grounding data, and Azure OpenAI forms the response based on that information.
# Add your own data source

Adding your data is done through the Azure OpenAI Studio, in the **Chat** playground. The data source you add is then used to augment the prompt sent to the model. When adding your data, you can choose to upload your data files, use data in a blob storage account, or connect to an existing AI Search index.

If you're uploading or using files already in a storage account, Azure OpenAI on your data supports `.md`, `.txt`, `.html`, `.pdf`, and Microsoft Word or PowerPoint files. If any of these files contain graphics or images, the response quality depends on how well text can be extracted from the visual content.

When uploading data or connecting to files in a storage account, it's recommended to use the Azure OpenAI Studio to create the search resource and index. Adding data this way allows the appropriate chunking to happen when inserting into the index, yielding better responses. If you're using large text files or forms, you should use the available [data preparation script](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/concepts/use-your-data#ingesting-your-data-into-azure-cognitive-search?azure-portal=true) to improve the AI model's accuracy.

Enabling [semantic search](https://learn.microsoft.com/en-us/azure/search/semantic-search-overview) for your AI Search service can improve the result of searching your data index and you're likely to receive higher quality responses and citations. However, enabling semantic search may increase the cost of the search service.

## Connect your data

To connect your data, navigate to the **Chat** playground in Azure OpenAI Studio and select the **Add your data** tab in the **Assistant setup** pane. Select the **Add a data source** button to get your data connected. The prompts guide you through setting up the connection to each data source, and getting that data into a search index.

If you're using your own index that wasn't created through Azure OpenAI Studio, one of the pages allows you to specify your column mapping. It's important to provide accurate fields, to enable the model to provide a better response, especially for **Content data**.

![Screenshot of Azure OpenAI Studio index field mapping.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/use-own-data-azure-openai/media/index-data-mapping.png)# Chat with your model using your own data

Completed 100 XP

- 3 minutes

RAG with Azure OpenAI on your own data can be used in Azure OpenAI Studio with the **Chat** playground, or by using the API.

## Token considerations and recommended settings

Since RAG with Azure OpenAI on your data includes search results on your index in the prompt, it's important to understand how that impacts your token allotment. Each call to the model includes tokens for the system message, the user prompt, conversation history, retrieved search documents, internal prompts, and the model's response.

The system message, for example, is a useful reference for instructions for the model and is included with every call. While there's no token limit for the system message, when using your own data the system message gets truncated if it exceeds 200 tokens. The response from the model is also limited when using your own data is 1500 tokens.

Due to these token limitations, it's recommended that you limit both the question length and the conversation history length in your call. [Prompt engineering techniques](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/concepts/advanced-prompt-engineering) such as breaking down the task and chain of thought prompting can help the model respond more effectively.

## Using the API

Using the API with your own data, you need to specify the data source where your data is stored. With each call you need to include the `endpoint`, `key`, and `indexName` for your AI Search resource.

Your request body will be similar to the following JSON.

JSON

```
{
    "dataSources": [
        {
            "type": "AzureCognitiveSearch",
            "parameters": {
                "endpoint": "<your_search_endpoint>",
                "key": "<your_search_endpoint>",
                "indexName": "<your_search_index>"
            }
        }
    ],
    "messages":[
        {
            "role": "system", 
            "content": "You are a helpful assistant assisting users with travel recommendations."
        },
        {
            "role": "user", 
            "content": "I want to go to New York. Where should I stay?"
        }
    ]
}
```

The call when using your own data needs to be sent to a different endpoint than is used when calling a base model, which includes `extensions`. Your call will be sent to a URL similar to the following.

HTTP

```
<your_azure_openai_resource>/openai/deployments/<deployment_name>/chat/completions?api-version=<version>
```

The request will also need to include the `Content-Type` and `api-key`.
