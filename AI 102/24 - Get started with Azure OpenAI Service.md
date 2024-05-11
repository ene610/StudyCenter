# Introduction

Suppose you want to build a support application that summarizes text and suggest code. To build this app, you want to utilize the capabilities you see in ChatGPT, a chatbot built by the OpenAI research company that takes in natural language input from a user and returns a machine-created, human-like response.

Generative AI models power ChatGPT's ability to produce new content, such as text, code, and images, based on a natural language prompts. Many generative AI models are a subset of [deep learning algorithms](https://learn.microsoft.com/en-us/dotnet/machine-learning/deep-learning-overview). These algorithms support various workloads across vision, speech, language, decision, search, and more.

Azure OpenAI Service brings these generative AI models to the Azure platform, enabling you to develop powerful AI solutions that benefit from the security, scalability, and integration of other services provided by the Azure cloud platform. These models are available for building applications through a REST API, various SDKs, and a Studio interface. This module guides you through the Azure OpenAI Studio experience, giving you the foundation to further develop solutions with generative AI.
# Access Azure OpenAI Service

The first step in building a generative AI solution with Azure OpenAI is to provision an Azure OpenAI resource in your Azure subscription. Azure OpenAI Service is currently in limited access. Users need to apply for service access at [https://aka.ms/oai/access](https://aka.ms/oai/access).

Note

Azure OpenAI Service has been released with limited access to support the ethical use of the service. You can read Microsoft's Transparency note for Azure OpenAI Service [here](https://learn.microsoft.com/en-us/legal/cognitive-services/openai/transparency-note).

Once you have access to Azure OpenAI Service, you can get started by creating a resource in the [Azure portal](https://portal.azure.com/) or with the Azure command line interface (CLI).

## Create an Azure OpenAI Service resource in the Azure portal

When you create an Azure OpenAI Service resource, you need to provide a subscription name, resource group name, region, unique instance name, and select a pricing tier. ![Screenshot of the Azure portal's page to create an Azure OpenAI Service resource.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/get-started-openai/media/create-azure-openai-portal.png)

## Create an Azure OpenAI Service resource in Azure CLI

To create an Azure OpenAI Service resource from the CLI, refer to this example and replace the following variables with your own:

- MyOpenAIResource: _replace with a unique name for your resource_
- OAIResourceGroup: _replace with your resource group name_
- eastus: _replace with the region to deploy your resource_
- subscriptionID: _replace with your subscription ID_

.NET CLI

```
az cognitiveservices account create \
-n MyOpenAIResource \
-g OAIResourceGroup \
-l eastus \
--kind OpenAI \
--sku s0 \
--subscription subscriptionID
```

Note

You can find the regions available for a service through the CLI command `az account list-locations`. To see how to sign into Azure and create an Azure group via the CLI, you can refer to the [documentation here](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/how-to/create-resource?pivots=cli#sign-in-to-the-cli?azure-portal=true).

### Regional availability

Azure OpenAI Service provides access to many types of models. Certain models are only available in select regions. Consult the [Azure OpenAI model availability guide](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/concepts/models#model-summary-table-and-region-availability/?azure-portal=true) for region availability. You can create two Azure OpenAI resources per region.
# Use Azure OpenAI Studio

Azure OpenAI Studio provides access to model management, deployment, experimentation, customization, and learning resources.

You can access the Azure OpenAI Studio through the Azure portal after creating a resource, or at [https://oai.azure.com](https://oai.azure.com/) by logging in with your Azure OpenAI resource instance. During the sign-in workflow, select the appropriate directory, Azure subscription, and Azure OpenAI resource.

![Screenshot of the Azure OpenAI Studio portal which can be used to access several features.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/get-started-openai/media/studio-portal.png)

When you first open Azure OpenAI Studio, you'll see a call-to-action button at the top of the screen to deploy your first model. Selecting the option to create a new deployment opens the **Deployments** page, from where you can deploy a base model and start experimenting with it.

![Screenshot of the Azure OpenAI Studio portal menu of pages.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/get-started-openai/media/openai-portal-navigation.png)
# Explore types of generative AI models

To begin building with Azure OpenAI, you need to choose a base model and deploy it. Microsoft provides base models and the option to create customized base models. This module covers the currently available base models.

Azure OpenAI includes several types of model:

- **GPT-4 models** are the latest generation of _generative pretrained_ (GPT) models that can generate natural language and code completions based on natural language prompts.
- **GPT 3.5 models** can generate natural language and code completions based on natural language prompts. In particular, **GPT-35-turbo** models are optimized for chat-based interactions and work well in most generative AI scenarios.
- **Embeddings models** convert text into numeric vectors, and are useful in language analytics scenarios such as comparing text sources for similarities.
- **DALL-E models** are used to generate images based on natural language prompts. Currently, DALL-E models are in preview. DALL-E models aren't listed in the Azure OpenAI Studio interface and don't need to be explicitly deployed.

Models differ by speed, cost, and how well they complete specific tasks. You can learn more about the differences and latest models offered in the [Azure OpenAI Service documentation](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/concepts/models).

Note

Pricing is determined by tokens and by model type. Learn more about the latest [pricing here](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/).

In the Azure OpenAI Studio, the **Models** page lists the available base models (other than DALL-E models) and provides an option to create additional customized models by fine-tuning the base models. The models that have a _Succeeded_ status mean they're successfully trained and can be selected for deployment.

![Screenshot of the Azure OpenAI Studio portal's out-of-the-box generative AI models.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/get-started-openai/media/studio-models.png)
# Deploy generative AI models

You first need to deploy a model to make API calls to receive completions to prompts. When you create a new deployment, you need to indicate which base model to deploy. You can deploy any number of deployments in one or multiple Azure OpenAI resources as long as their TPM adds up to less than 240K total in that region. There are several ways you can deploy your base model.

## Deploy using Azure OpenAI Studio

In Azure OpenAI Studio's **Deployments** page, you can create a new deployment by selecting a model name from the menu. The available base models come from the list in the models page.

![Screenshot of the Azure OpenAI Studio portal's model deployment wizard.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/get-started-openai/media/studio-deployment.png)

From the _Deployments_ page in the Studio, you can also view information about all your deployments including deployment name, model name, model version, status, date created, and more.

## Deploy using Azure CLI

You can also deploy a model using the console. Using this example, replace the following variables with your own resource values:

- OAIResourceGroup: _replace with your resource group name_
- MyOpenAIResource: _replace with your resource name_
- MyModel: _replace with a unique name for your model_
- gpt-35-turbo: _replace with the base model you wish to deploy_

.NET CLI

```
az cognitiveservices account deployment create \
   -g OAIResourceGroup \
   -n MyOpenAIResource \
   --deployment-name MyModel \
   --model-name gpt-35-turbo \
   --model-version "0301"  \
   --model-format OpenAI \
   --sku-name "Standard" \
   --sku-capacity 1
```

## Deploy using the REST API

You can deploy a model using the REST API. In the request body, you specify the base model you wish to deploy. See an example in the [Azure OpenAI documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/).
# Use prompts to get completions from models

Once the model is deployed, you can test how it completes prompts. A prompt is the text portion of a request that is sent to the deployed model's completions endpoint. Responses are referred to as _completions_, which can come in form of text, code, or other formats.

## Prompt types

Prompts can be grouped into types of requests based on task.

|Task type|Prompt example|Completion example|
|---|---|---|
|**Classifying content**|Tweet: I enjoyed the trip.  <br>Sentiment:|Positive|
|**Generating new content**|List ways of traveling|1. Bike  <br>2. Car ...|
|**Holding a conversation**|A friendly AI assistant|[See examples](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/how-to/completions#conversation?portal=true)|
|**Transformation** (translation and symbol conversion)|English: Hello  <br>French:|bonjour|
|**Summarizing content**|Provide a summary of the content  <br>{text}|The content shares methods of machine learning.|
|**Picking up where you left off**|One way to grow tomatoes|is to plant seeds.|
|**Giving factual responses**|How many moons does Earth have?|One|

## Completion quality

Several factors affect the quality of completions you'll get from a generative AI solution.

- The way a prompt is engineered. Learn more about [prompt engineering here](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/concepts/prompt-engineering?portal=true).
- The model parameters (covered next)
- The data the model is trained on, which can be adapted through [model fine-tuning with customization](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/how-to/fine-tuning?pivots=programming-language-studio?portal=true)

You have more control over the completions returned by training a custom model than through prompt engineering and parameter adjustment.

## Making calls

You can start making calls to your deployed model via the REST API, Python, C#, or from the Studio. If your deployed model has a GPT-3.5 or GPT-4 model base, use the [Chat completions documentation](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/reference#chat-completions?azure-portal=true), which has different request endpoints and variables required than for other base models.
# Test models in Azure OpenAI Studio's playgrounds

Playgrounds are useful interfaces in Azure OpenAI Studio that you can use to experiment with your deployed models without needing to develop your own client application. Azure OpenAI Studio offers multiple playgrounds with different parameter tuning options.

## Completions playground

The Completions playground allows you to make calls to your deployed models through a text-in, text-out interface and to adjust parameters. You need to select the deployment name of your model under Deployments. Optionally, you can use the provided examples to get you started, and then you can enter your own prompts.

![Screenshot of the Azure OpenAI Studio portal's completions playground.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/get-started-openai/media/azure-openai-completions-playground.png)

#### Completions Playground parameters

There are many parameters that you can adjust to change the performance of your model:

- **Temperature**: Controls randomness. Lowering the temperature means that the model produces more repetitive and deterministic responses. Increasing the temperature results in more unexpected or creative responses. Try adjusting temperature or Top P but not both.
- **Max length (tokens)**: Set a limit on the number of tokens per model response. The API supports a maximum of 4000 tokens shared between the prompt (including system message, examples, message history, and user query) and the model's response. One token is roughly four characters for typical English text.
- **Stop sequences**: Make responses stop at a desired point, such as the end of a sentence or list. Specify up to four sequences where the model will stop generating further tokens in a response. The returned text won't contain the stop sequence.
- **Top probabilities (Top P)**: Similar to temperature, this controls randomness but uses a different method. Lowering Top P narrows the model’s token selection to likelier tokens. Increasing Top P lets the model choose from tokens with both high and low likelihood. Try adjusting temperature or Top P but not both.
- **Frequency penalty**: Reduce the chance of repeating a token proportionally based on how often it has appeared in the text so far. This decreases the likelihood of repeating the exact same text in a response.
- **Presence penalty**: Reduce the chance of repeating any token that has appeared in the text at all so far. This increases the likelihood of introducing new topics in a response.
- **Pre-response text**: Insert text after the user’s input and before the model’s response. This can help prepare the model for a response.
- **Post-response text**: Insert text after the model’s generated response to encourage further user input, as when modeling a conversation.

## Chat playground

The Chat playground is based on a conversation-in, message-out interface. You can initialize the session with a system message to set up the chat context.

In the Chat playground, you're able to add _few-shot examples_. The term few-shot refers to providing a few of examples to help the model learn what it needs to do. You can think of it in contrast to zero-shot, which refers to providing no examples.

In the _Assistant setup_, you can provide few-shot examples of what the user input may be, and what the assistant response should be. The assistant tries to mimic the responses you include here in tone, rules, and format you've defined in your system message.

![Screenshot of the Azure OpenAI Studio portal's Chat playground.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/get-started-openai/media/azure-openai-chat-playground.png)

#### Chat playground parameters

The Chat playground, like the Completions playground, also includes the Temperature parameter. The Chat playground also supports other parameters _not_ available in the Completions playground. These include:

- **Max response**: Set a limit on the number of tokens per model response. The API supports a maximum of 4000 tokens shared between the prompt (including system message, examples, message history, and user query) and the model's response. One token is roughly four characters for typical English text.
- **Top P**: Similar to temperature, this controls randomness but uses a different method. Lowering Top P narrows the model’s token selection to likelier tokens. Increasing Top P lets the model choose from tokens with both high and low likelihood. Try adjusting temperature or Top P but not both.
- **Past messages included**: Select the number of past messages to include in each new API request. Including past messages helps give the model context for new user queries. Setting this number to 10 will include five user queries and five system responses.

The **Current token count** is viewable from the Chat playground. Since the API calls are priced by token and it's possible to set a max response token limit, you'll want to keep an eye out for the current token count to make sure the conversation-in doesn't exceed the max response token count.