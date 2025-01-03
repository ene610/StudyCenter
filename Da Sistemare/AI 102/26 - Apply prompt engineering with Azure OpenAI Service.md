# Introduction

Response quality from AI models in Azure OpenAI depends on the quality of the prompt provided. Improving prompt quality through various techniques is called prompt engineering.

In this module, you'll learn about prompt engineering and how it can be used to optimize the performance of Azure OpenAI models. Prompt engineering involves designing and optimizing prompts to better utilize Azure OpenAI models.

# Understand prompt engineering

The quality of the input prompts we send to an AI model, like those available in Azure OpenAI, directly influences the quality of what we get back. By carefully constructing the prompts we send to the model, the model can provide better and more interesting responses.

## What is prompt engineering

Generative AI models trained on huge amounts of data and can generate text, images, code, and creative content based on the most likely continuation of the prompt.

Prompt engineering is the process of designing and optimizing prompts to better utilize AI models. Designing effective prompts is critical to the success of prompt engineering, and it can significantly improve the AI model's performance on specific tasks. Providing relevant, specific, unambiguous, and well structured prompts can help the model better understand the context and generate more accurate responses.

For example, if we want an OpenAI model to generate product descriptions, we can provide it with a detailed description that describes the features and benefits of the product. By providing this context, the model can generate more accurate and relevant product descriptions.

Prompt engineering can also help mitigate bias and improve fairness in AI models. By designing prompts that are diverse and inclusive, we can ensure that the model isn't biased towards a particular group or perspective.

Important

No matter how good of a prompt you can design, responses from AI models should never be taken as fact or completely free from bias. Always use AI responsibly. For more information, see Microsoft's [transparency note](https://learn.microsoft.com/en-us/legal/cognitive-services/openai/transparency-note) on Azure OpenAI and [Microsoft's AI principles](https://www.microsoft.com/ai/responsible-ai).

In addition, prompt engineering can help us understand which references the model uses to generate its response. Generative AI models have a ton of parameters and the logic it follows is largely unknown to users, so it can be confusing how it arrives at the response it gives. By designing prompts that are easy to understand and interpret, we can help humans better understand how the model is generating its responses. This can be particularly important in domains such as healthcare, where it's critical to understand how the model is making decisions.

There are different methods to utilize when engineering your own prompts, many of which are covered in upcoming units of this module. These include providing instructions, contextual content, cues or few-shot examples, and correctly ordering content in your prompt. The methods covered here aren't exhaustive as this area is a nuanced and fluid topic.

## Considerations for API endpoints

The examples in the rest of this module will be focused on `ChatCompletion`. It's worth noting that `ChatCompletion` can also be used for non chat scenarios, where any instructions are included in the system message and user content is provided in the user role message. Most of these examples can be altered to use the `Completion` endpoint, if desired.

In terms of model availability, the `Completion` endpoint can be used with `gpt-3` and earlier, and `ChatCompletion` can be used with `gpt-35-turbo` and later models.

## Adjusting model parameters

In addition to techniques discussed in this module, adjusting parameters of the model can have a significant impact on the response. In particular, `temperature` and `top_p` (top_probability) are the most likely to impact a model's response as they both control randomness in the model, but in different ways.

Higher values produce more creative and random responses, but will likely be less consistent or focused. Responses expected to be fictional or unique benefit from higher values for these parameters, whereas content desired to be more consistent and concrete should use lower values.

Try adjusting these parameters with the same prompt to see how they impact the response. It's recommended to change either `temperature` or `top_p` at a time, but not both.
# Write more effective prompts

Azure OpenAI models are capable of generating responses to natural language queries with remarkable accuracy. However, the quality of the responses depends largely on how well the prompt is written. Developers can optimize the performance of Azure OpenAI models by using different techniques in their prompts, resulting in more accurate and relevant responses.

## Provide clear instructions

Asking the Azure OpenAI model clearly for what you want is one way to get desired results. By being as descriptive as possible, the model can generate a response that most closely matches what you're looking for.

For example, say you want to create a product description for a new water bottle. Consider the answer associated with each prompt:

**Prompt**

code

```
Write a product description for a new water bottle
```

**Response**

code

```
Introducing the latest addition to our product line - the innovative and eco-friendly water bottle.
Made from high-quality, BPA-free materials, this bottle is designed to keep your beverages at the
perfect temperature for hours. Its sleek and stylish design makes it the perfect accessory for any
outdoor activity or workout session. With its convenient carrying handle and leak-proof lid, you 
can take it with you wherever you go, without worrying about spills or leaks. Plus, its easy-to-clean
design ensures that you can use it again and again, making it the perfect choice for anyone looking 
for a reliable and sustainable water bottle.
```

Versus a similar prompt, with clear instructions.

**Prompt**

code

```
Write a product description for a new water bottle that is 100% recycled. Be sure to include that
it comes in natural colors with no dyes, and each purchase removes 10 pounds of plastic from our 
oceans
```

**Response**

code

```
Introducing our newest water bottle, the eco-friendly choice for the conscious consumer. Made from 
100% recycled materials and available in natural colors with no dyes, this bottle is not only 
stylish but also sustainable. Each purchase of this bottle removes 10 pounds of plastic from 
our oceans, making it a responsible choice for those who care about the environment. Its durable 
and leak-proof design makes it perfect for outdoor activities, while its easy-to-carry handle 
makes it convenient to take on the go. Join us in our mission to reduce plastic waste and choose 
this eco-friendly water bottle for your daily hydration needs.
```

Including specifics that need to be included lets the model know what information to add to the description, making it more accurate to the new product.

This method can be extrapolated to include complex instructions, such as a bulleted list of details to include, length of response, or desired formats to be included in the output. Try asking for exactly what you want to see in the result, and you may be surprised at how well the model satisfies your request.

## Format of instructions

How instructions are formatted can impact how the model interprets the prompt. Recency bias can affect models, where information located towards the end of the prompt can have more influence on the output than information at the beginning. You may get better responses by repeating the instructions at the end of the prompt and assessing how that affects the generated response.

This recency bias can also come into play when using `ChatCompletion` in a chat scenario, where more recent messages in the conversation included in the prompt have a greater impact on the response. The next unit goes more in depth on using conversations to improve response quality, but putting important information closer to the end of the prompt may result in a better response.

### Use section markers

A specific technique for formatting instructions is to split the instructions at the beginning or end of the prompt, and have the user content contained within `---` or `###` blocks. These tags allow the model to more clearly differentiate between instructions and content. For example:

code

```
Translate the text into French

---
What's the weather going to be like today?
---
```

Note

Best practices for section markers may change with future versions.

## Primary, supporting, and grounding content

Including content for the model to use to respond with allows it to answer with greater accuracy. This content can be thought of in two ways: primary and supporting content.

Primary content refers to content that is the subject of the query, such as a sentence to translate or an article to summarize. This content is often included at the beginning or end of the prompt (as an instruction and differentiated by `---` blocks), with instructions explaining what to do with it.

For example, say we have a long article that we want to summarize. We could put it in a `---` block in the prompt, then end with the instruction.

code

```
---
<insert full article here, as primary content>
---

Summarize this article and identify three takeaways in a bulleted list
```

Supporting content is content that may alter the response, but isn't the focus or subject of the prompt. Examples of supporting content include things like names, preferences, future date to include in the response, and so on. Providing supporting content allows the model to respond more completely, accurately, and be more likely to include the desired information.

For example, given a very long promotional email, the model is able to extract key information. If you then add supporting content to the prompt specifying something specific you're looking for, the model can provide a more useful response. In this case the email is the primary content, with the specifics of what you're interested in as the supporting content

code

```
---
<insert full email here, as primary content>
---
<the next line is the supporting content>
Topics I'm very interested in: AI, webinar dates, submission deadlines

Extract the key points from the above email, and put them in a bulleted list:
```

Grounding content allows the model to provide reliable answers by providing content for the model to draw answer from. Grounding content could be an essay or article that you then ask questions about, a company FAQ document, or information that is more recent than the data the model was trained on. If you need more reliable and current responses, or you need to reference unpublished or specific information, grounding content is highly recommended.

Grounding content differs from primary content as it's the source of information to answer the prompt query, instead of the content being operated on for things like summarization or translation. For example, when provided an unpublished research paper on the history of AI, it can then answer questions using that grounding content.

code

```
---
<insert unpublished paper on the history of AI here, as grounding content>
---

Where and when did the field of AI start?
```

This grounding data allows the model to give more accurate and informed answers that may not be part of the dataset it was trained on.

## Cues

Cues are leading words for the model to build upon, and often help shape the response in the right direction. They often are used with instructions, but don't always. Cues are particularly helpful if prompting the model for code generation. Current Azure OpenAI models can generate some interesting code snippets, however code generation will be covered in more depth in a future module.

For example, if you're wanting help creating a SQL query, provide instructions of what you need along with the beginning of the query:

code

```
Write a join query to get customer names with purchases in the past 30 days between tables named orders and customer on customer ID. 

SELECT
```

The model response picks up where the prompt left off, continuing in SQL, even though we never asked for a specific language. Other examples could be to help with python code, by giving code comments about the desired app and including `import` as a leading word at the end of the prompt, or similar in your desired language.

Another example, given a large collection of customer reviews in a prompt, and ending with:

code

```
Summarize the reviews above:
Most common complaints:
- 
```

The model then knows to complete the statements based off the context provided in the reviews.
# Provide context to improve accuracy

Choose your development language

By providing context to the AI model, it allows the model to better understand what you are asking for or what it should know to provide the best answer. Context can be provided in several ways.

## Request output composition

Specifying the structure of your output can have a large impact on your results. This could include something like asking the model to cite their sources, write the response as an email, format the response as a SQL query, classify sentiment into a specific structure, and so on. For example:

**Prompt**

code

```
Write a table in markdown with 6 animals in it, with their genus and species
```

**Response**

code

```
| Animal           | Genus          | Species        |
| ---------------- |:--------------:|:--------------:|
| Red Panda        | Ailurus        | fulgens        |
| African Elephant | Loxodonta      | africana       |
| Snow Leopard     | Panthera       | uncia          |
| Arctic Fox       | Vulpes         | lagopus        |
| Chimpanzee       | Pan            | troglodytes    |
| Siberian Tiger   | Panthera       | tigris altaica |
```

This technique can be used with custom formats, such as a JSON structure:

**Prompt**

code

```
Put two fictional characters into JSON of the following format

{
  firstNameFictional: 
  jobFictional:
}
```

**Response**

code

```
Here's an example of how you can put two fictional characters into JSON format:

{
  "firstNameFictional": "Henry",
  "jobFictional": "Wizard"
},
{
  "firstNameFictional": "Frank",
  "jobFictional": "Hero"
}
```

## System message

The system message is included at the beginning of a prompt and is designed to give the model instructions, perspective to answer from, or other information helpful to guide the model's response. This system message might include tone or personality, topics that shouldn't be included, or specifics (like formatting) of how to answer.

For example, you could give it some of the following system messages:

- "I want you to act like a command line terminal. Respond to commands exactly as cmd.exe would, in one unique code block, and nothing else."
- "I want you to be a translator, from English to Spanish. Don't respond to anything I say or ask, only translate between those two languages and reply with the translated text."
- "Act as a motivational speaker, freely giving out encouraging advice about goals and challenges. You should include lots of positive affirmations and suggested activities for reaching the user's end goal."

Other example system messages are available at the top of the chat window in [Azure OpenAI Studio](https://oai.azure.com/portal). Try defining your own system prompt that specifies a unique response, and chat with the model to see how responses differ.

The `ChatCompletion` endpoint enables including the system message by using the `System` chat role.

Python

```
response = openai.ChatCompletion.create(
    model="gpt-35-turbo",
    messages=[
        {"role": "system", "content": "You are a casual, helpful assistant. You will talk like an American old western film character."},
        {"role": "user", "content": "Can you direct me to the library?"}
    ]
)
```

**Response**

code

```
{
  "choices": [
    {
      "finish_reason": "stop",
      "index": 0,
      "message": {
        "content": "Well howdy there, stranger! The library, huh?
                    Y'all just head down the main road till you hit the town 
                    square. Once you're there, take a left and follow the street 
                    for a spell. You'll see the library on your right, can’t 
                    miss it. Happy trails!",
        "role": "assistant"
      }
    }
  ],
  ...
}
```

System messages can significantly change the response, both in format and content. Try defining a clear system message for the model that explains exactly what kind of response you expect, and what you do or don't want it to include.

## Conversation history

Along with the system message, other messages can be provided to the model to enhance the conversation. Conversation history enables the model to continue responding in a similar way (such as tone or formatting) and allow the user to reference previous content in subsequent queries. This history can be provided in two ways: from an actual chat history, or from a user defined example conversation.

Chat interfaces that use OpenAI models, such as ChatGPT and the chat playground in [Azure OpenAI Studio](https://oai.azure.com/portal/chat), include conversation history automatically which results in a richer, more meaningful conversation. In the **Parameters** section below the chat window of the Azure OpenAI Studio chat playground, you can specify how many past messages you want included. Try reducing that to 1 or increasing to max to see how different amounts of history impact the conversation.

Note

More conversation history included in the prompt means a larger number of input tokens are used. You will have to determine what the correct balance is for your use case, considering the token limit of the model you are using.

Chat systems can also utilize the summarization capabilities of the model to save on input tokens. An app can choose to summarize past messages and include that summary in the conversation history, then provide only the past couple messages verbatim to the model.

## Few shot learning

Using a user defined example conversation is what is called _few shot learning_, which provides the model examples of how it should respond to a given query. These examples serve to train the model how to respond.

For example, by providing the model a couple prompts and the expected response, it continues in the same pattern without instructing it what to do:

code

```
User: That was an awesome experience
Assistant: positive
User: I won't do that again
Assistant: negative
User: That was not worth my time
Assistant: negative
User: You can't miss this
Assistant:
```

If the model is provided with just `You can't miss this` with no additional context from few shot learning, the response isn't likely to be useful.

In practical terms, conversation history and few shot learning are sent to the model in the same way; each user message and assistant response is a discrete message in the message object. The `ChatCompletion` endpoint is optimized to include message history, regardless of if this message history is provided as few shot learning, or actual conversation history.

Python

```
response = openai.ChatCompletion.create(
    model="gpt-35-turbo",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "That was an awesome experience"},
        {"role": "assistant", "content": "positive"},
        {"role": "user", "content": "I won't do that again"},
        {"role": "assistant", "content": "negative"},
        {"role": "user", "content": "That was not worth my time"},
        {"role": "assistant", "content": "negative"},
        {"role": "user", "content": "You can't miss this"}
    ]
)
```

## Break down a complex task

Another technique for improved interaction is to divide complex prompts into multiple queries. This allows the model to better understand each individual part, and can improve the overall accuracy. Dividing your prompts also allows you to include the response from a previous prompt in a future prompt, and using that information in addition to the capabilities of the model to generate interesting responses.

For example, you could ask the model `Doug can ride down the zip line in 30 seconds, and takes 5 minutes to climb back up to the top. How many times can Doug ride the zip line in 17 minutes?`. The result is likely `3`, which if Doug starts at the top of the zip line is incorrect.

A more informative answer could come from asking it multiple questions, about the round trip time to get back to the top of the zip line, and how to account for the fact that Doug starts at the top. Breaking down this problem reveals that Doug can, in fact, ride the zip line four times.

### Chain of thought

One useful method to help you break down your task effectively is to ask the model to explain its chain of thought.

Asking a model to respond with the step by step process by which it determined the response is a helpful way to understand how the model is interpreting the prompt. By doing so, you can see where the model made an incorrect logical turn and better understand how to change your prompt to avoid the error. This technique can include asking it to cite its sources, like Bing chat does (which uses a GPT-4 generation model), and giving reasoning for why it determined its answer.

The chain of thought prompting technique is best used to help you iterate and improve on your prompts to get the highest quality answer from the model.

For example, asking the model `What sport is easiest to learn but hardest to master?` results in response with an answer, and a small explanation of why. However, when prompted with `What sport is easiest to learn but hardest to master? Give a step by step approach of your thoughts, ending in your answer`, the response is a complete explanation of how it arrived at its answer.

code

```
Sure, here's a step-by-step approach to answering the question:
1. Identify sports that are popular and have a large following.
2. Consider the basic mechanics of each sport and how easy they are to learn.
3. Think about the various techniques and skills required to play each sport at a high level, and how difficult they are to master.
4. Compare the relative ease of learning each sport to the difficulty of mastering it.
5. Based on the above analysis, determine which sport is easiest to learn but hardest to master.

Using this approach, I would say that the sport of golf is easiest to learn but hardest to master. Here's why:
1. Golf is a popular sport with a large following.
2. The basic mechanics of hitting a golf ball are relatively simple and can be learned quickly with some practice.
3. However, achieving consistency and mastering the various shots and techniques required to play at a high level can take years of practice and dedication.
4. Compared to other sports, the difference between a beginner and an intermediate golfer is relatively small, while the difference between an intermediate and an advanced golfer is much larger.
5. Therefore, I would say that golf is the sport that is easiest to learn but hardest to master.
```

Knowing the steps of reason the model used to form its response allows us to identify where we need to split the prompt, provide more information, or clarify instructions.