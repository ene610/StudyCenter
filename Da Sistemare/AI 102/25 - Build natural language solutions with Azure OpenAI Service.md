# Introduction

Azure OpenAI provides a platform for developers to add artificial intelligence functionality to their applications with the help of both Python and C# SDKs and REST APIs. The platform has various AI models available, each specializing in different tasks, which can be deployed through the Azure OpenAI Service.

This module guides you through how to build Azure OpenAI into your own application, giving you a starting point for developing solutions with generative AI.
# Integrate Azure OpenAI into your app

Azure OpenAI offers both C# and Python SDKs and a REST API that developers can use to add AI functionality to their applications. Generative AI capabilities in Azure OpenAI are provided through _models_. The models available in the Azure OpenAI service belong to different families, each with their own focus. To use one of these models, you need to deploy through the Azure OpenAI Service.

Important

Azure OpenAI has been released with limited access to support the responsible use of the service. Users need to [apply for access](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/overview#how-do-i-get-access-to-azure-openai?azure-portal=true) and be approved before they can create an Azure OpenAI resource.

## Create an Azure OpenAI resource

An Azure OpenAI resource can be deployed through both the Azure command line interface (CLI) and the Azure portal. Creating the Azure OpenAI resource through the Azure portal is similar to deploying individual Azure AI Services resources, and is part of the Azure AI Services services.

1. Navigate to the [Azure portal](https://portal.azure.com/)
2. Search for **Azure OpenAI**, select it, and click **Create**
3. Enter the appropriate values for the empty fields, and create the resource.

The possible regions for Azure OpenAI are currently limited. Choose the region closest to your physical location.

Once the resource has been created, you'll have keys and an endpoint that you can use in your app.

## Choose and deploy a model

Each model family excels at different tasks, and there are different capabilities of the models within each family. Model families break down into three main families:

- **Generative Pre-trained Transformer (GPT)** - Models that understand and generate natural language and some code. These models are best at general tasks, conversations, and chat formats.
- **Code** (`gpt-3` and earlier) - Code models are built on top of GPT models, and trained on millions of lines of code. These models can understand and generate code, including interpreting comments or natural language to generate code. `gpt-35-turbo` and later models have this code functionality included without the need for a separate code model.
- **Embeddings** - These models can understand and use embeddings, which are a special format of data that can be used by machine learning models and algorithms.

This module focuses on general GPT models, with other models being covered in other modules.

For older models, the model family and capability is indicated in the name of the base model, such as `text-davinci-003`, which specifies that it's a text model, with `davinci` level capability, and identifier `3`. Details on models, capability levels, and naming conventions can be found on the [Azure OpenAI Models documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models) page.

More recent models specify which `gpt` generation, and if they are the `turbo` version, such as `gpt-35-turbo` representing the _GPT 3.5 Turbo_ model.

To deploy a model for you to use, navigate to the [Azure OpenAI Studio](https://oai.azure.com/) and go to the **Deployments** page. The lab later in this module covers exactly how to do that.

## Authentication and specification of deployed model

When you deploy a model in Azure OpenAI, you choose a deployment name to give it. When configuring your app, you need to specify your resource endpoint, key, and deployment name to specify which deploy model to send your request to. This enables you to deploy various models within the same resource, and make requests to the appropriate model depending on the task.

## Prompt engineering

How the input prompt is written plays a large part in how the AI model will respond. For example, if prompted with a simple request such as "What is Azure OpenAI", you often get a generic answer similar to using a search engine.

However, if you give it more details about what you want in your response, you get a more specific answer. For example, given this prompt:

text

```
Classify the following news headline into 1 of the following categories: Business, Tech, Politics, Sport, Entertainment

Headline 1: Donna Steffensen Is Cooking Up a New Kind of Perfection. The Internet’s most beloved cooking guru has a buzzy new book and a fresh new perspective
Category: Entertainment

Headline 2: Major Retailer Announces Plans to Close Over 100 Stores
Category:
```

You'll likely get the "Category:" under headline filled out with "Business".

Several examples similar to this one can be found in the Azure OpenAI Studio Playground, under the **Examples** dropdown. Try to be as specific as possible about what you want in response from the model, and you may be surprised at how insightful it can be!

Note

It is never safe to assume that answers from an AI model are factual or correct. Teams or individuals tasked with developing and deploying AI systems should work to identify, measure, and mitigate harm. It is your responsibility to verify any responses from an AI model, and to use AI responsibly. Check out [Microsoft's Transparency Notes on Azure OpenAI](https://learn.microsoft.com/en-us/legal/cognitive-services/openai/transparency-note) for further guidelines on how to use Azure OpenAI models responsibly.

Further details can be found at the [Prompt engineering](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/concepts/prompt-engineering) documentation page.

## Available endpoints

Azure OpenAI can be accessed via a REST API or an SDK currently available for Python and C#. The endpoints available for interacting with a deployed model are used differently, and certain endpoints can only use certain models. The available endpoints are:

- **Completion** - model takes an input prompt, and generates one or more predicted completions. You'll see this playground in the studio, but won't be covered in depth in this module.
- **ChatCompletion** - model takes input in the form of a chat conversation (where roles are specified with the message they send), and the next chat completion is generated.
- **Embeddings** - model takes input and returns a vector representation of that input.

For example, the input for `ChatCompletion` is a conversation with clearly defined roles for each message:

JSON

```
{"role": "system", "content": "You are a helpful assistant, teaching people about AI."},
{"role": "user", "content": "Does Azure OpenAI support multiple languages?"},
{"role": "assistant", "content": "Yes, Azure OpenAI supports several languages, and can translate between them."},
{"role": "user", "content": "Do other Azure AI Services support translation too?"}
```

When you give the AI model a real conversation, it can generate a better response with more accurate tone, phrasing, and context. The `ChatCompletion` endpoint enables the ChatGPT model to have a more realistic conversation by sending the history of the chat with the next user message.

`ChatCompletion` also allows for non-chat scenarios, such as summarization or entity extraction. This can be accomplished by providing a short conversation, specifying the system information and what you want, along with the user input. For example, if you want to generate a job description, provide `ChatCompletion` with something like the following conversation input.

JSON

```
{"role": "system", "content": "You are an assistant designed to write intriguing job descriptions. "},
{"role": "user", "content": "Write a job description for the following job title: 'Business Intelligence Analyst'. It should include responsibilities, required qualifications, and highlight benefits like time off and flexible hours."}
```

Note

`Completion` is available for all `gpt-3` generation models, while `ChatCompletion` is the only supported option for `gpt-4` models and is the preferred endpoint when using the `gpt-35-turbo` model. The lab in this module uses `gpt-35-turbo` with the `ChatCompletion` endpoint.

---
# Use Azure OpenAI REST API

Azure OpenAI offers a REST API for interacting and generating responses that developers can use to add AI functionality to their applications. This unit covers example usage, input and output from the API.

Note

Before interacting with the API, you must create an Azure OpenAI resource in the Azure portal, deploy a model in that resource, and retrieve your endpoint and keys. Check out the [Getting started with Azure OpenAI Service](https://learn.microsoft.com/en-us/training/modules/get-started-openai/) to learn how to do that.

For each call to the REST API, you need the endpoint and a key from your Azure OpenAI resource, and the name you gave for your deployed model. In the following examples, the following placeholders are used:

|Placeholder name|Value|
|---|---|
|`YOUR_ENDPOINT_NAME`|This base endpoint is found in the **Keys & Endpoint** section in the Azure portal. It's the base endpoint of your resource, such as `https://sample.openai.azure.com/`.|
|`YOUR_API_KEY`|Keys are found in the **Keys & Endpoint** section in the Azure portal. You can use either key for your resource.|
|`YOUR_DEPLOYMENT_NAME`|This deployment name is the name provided when you deployed your model in the Azure OpenAI Studio.|

## Chat completions

Once you've deployed a model in your Azure OpenAI resource, you can send a prompt to the service using a `POST` request.

rest

```
curl https://YOUR_ENDPOINT_NAME.openai.azure.com/openai/deployments/YOUR_DEPLOYMENT_NAME/chat/completions?api-version=2023-03-15-preview \
  -H "Content-Type: application/json" \
  -H "api-key: YOUR_API_KEY" \
  -d '{"messages":[{"role": "system", "content": "You are a helpful assistant, teaching people about AI."},
{"role": "user", "content": "Does Azure OpenAI support multiple languages?"},
{"role": "assistant", "content": "Yes, Azure OpenAI supports several languages, and can translate between them."},
{"role": "user", "content": "Do other Azure AI Services support translation too?"}]}'
```

The response from the API will be similar to the following JSON:

JSON

```
{
    "id": "chatcmpl-6v7mkQj980V1yBec6ETrKPRqFjNw9",
    "object": "chat.completion",
    "created": 1679001781,
    "model": "gpt-35-turbo",
    "usage": {
        "prompt_tokens": 95,
        "completion_tokens": 84,
        "total_tokens": 179
    },
    "choices": [
        {
            "message":
                {
                    "role": "assistant",
                    "content": "Yes, other Azure AI Services also support translation. Azure AI Services offer translation between multiple languages for text, documents, or custom translation through Azure AI Services Translator."
                },
            "finish_reason": "stop",
            "index": 0
        }
    ]
}
```

REST endpoints allow for specifying other optional input parameters, such as `temperature`, `max_tokens` and more. If you'd like to include any of those parameters in your request, add them to the input data with the request.

## Embeddings

Embeddings are helpful for specific formats that are easily consumed by machine learning models. To generate embeddings from the input text, `POST` a request to the `embeddings` endpoint.

rest

```
curl https://YOUR_ENDPOINT_NAME.openai.azure.com/openai/deployments/YOUR_DEPLOYMENT_NAME/embeddings?api-version=2022-12-01 \
  -H "Content-Type: application/json" \
  -H "api-key: YOUR_API_KEY" \
  -d "{\"input\": \"The food was delicious and the waiter...\"}"
```

When generating embeddings, be sure to use a model in Azure OpenAI meant for embeddings. Those models start with `text-embedding` or `text-similarity`, depending on what functionality you're looking for.

The response from the API will be similar to the following JSON:

JSON

```
{
  "object": "list",
  "data": [
    {
      "object": "embedding",
      "embedding": [
        0.0172990688066482523,
        -0.0291879814639389515,
        ....
        0.0134544348834753042,
      ],
      "index": 0
    }
  ],
  "model": "text-embedding-ada:002"
}
```
# Use Azure OpenAI SDK

Completed 100 XP

- 7 minutes

Choose your development language

In addition to REST APIs covered in the previous unit, users can also access Azure OpenAI models through C# and Python SDKs. The same functionality is available through both REST and these SDKs.

Note

Before interacting with the API using either SDK, you must create an Azure OpenAI resource in the Azure portal, deploy a model in that resource, and retrieve your endpoint and keys. Check out the [Getting started with Azure OpenAI Service](https://learn.microsoft.com/en-us/training/modules/get-started-openai/) to learn how to do that.

For both SDKs covered in this unit, you need the endpoint and a key from your Azure OpenAI resource, and the name you gave for your deployed model. In the following code snippets, the following placeholders are used:

|Placeholder name|Value|
|---|---|
|`YOUR_ENDPOINT_NAME`|This base endpoint is found in the **Keys & Endpoint** section in the Azure portal. It's the base endpoint of your resource, such as `https://sample.openai.azure.com/`.|
|`YOUR_API_KEY`|Keys are found in the **Keys & Endpoint** section in the Azure portal. You can use either key for your resource.|
|`YOUR_DEPLOYMENT_NAME`|This deployment name is the name provided when you deployed your model in the Azure OpenAI Studio.|

## Install libraries

First, install the client library for your preferred language. The C# SDK is a .NET adaptation of the REST APIs and built specifically for Azure OpenAI, however it can be used to connect to Azure OpenAI resources or non-Azure OpenAI endpoints. The Python SDK is built and maintained by OpenAI.

Console

```
pip install openai
```

## Configure app to access Azure OpenAI resource

Configuration for each language varies slightly, but both require the same parameters to be set. The necessary parameters are `endpoint`, `key`, and the name of your deployment, which is called the `engine` when sending your prompt to the model.

Add the library to your app, and set the required parameters for your client.

Python

```
# Add OpenAI library
from openai import AzureOpenAI

deployment_name = '<YOUR_DEPLOYMENT_NAME>' 

# Initialize the Azure OpenAI client
client = AzureOpenAI(
        azure_endpoint = '<YOUR_ENDPOINT_NAME>', 
        api_key='<YOUR_API_KEY>',  
        api_version="20xx-xx-xx" #  Target version of the API, such as 2024-02-15-preview
        )
```

## Call Azure OpenAI resource

Once you've configured your connection to Azure OpenAI, send your prompt to the model.

Python

```
response = client.chat.completions.create(
    model=deployment_name,
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "What is Azure OpenAI?"}
    ]
)
generated_text = response.choices[0].message.content

# Print the response
print("Response: " + generated_text + "\n")
```

The response object contains several values, such as `total_tokens` and `finish_reason`. The completion from the response object will be similar to the following completion:

Console

```
"Azure OpenAI is a cloud-based artificial intelligence (AI) service that offers a range of tools and services for developing and deploying AI applications. Azure OpenAI provides a variety of services for training and deploying machine learning models, including a managed service for training and deploying deep learning models, a managed service for deploying machine learning models, and a managed service for managing and deploying machine learning models."
```

In both C# and Python, your call can include optional parameters including `temperature` and `max_tokens`. Examples of using those parameters are included in this module's lab.