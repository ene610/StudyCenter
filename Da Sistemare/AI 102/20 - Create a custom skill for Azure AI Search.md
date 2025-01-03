# Introduction

You can use the predefined skills in Azure AI Search to greatly enrich an index by extracting additional information from the source data. However, there may be occasions when you have specific data extraction needs that cannot be met with the predefined skills and require some custom functionality.

For example:

- Integrate the Form Recognizer service to extract data from forms
- Consume an Azure Machine Learning model to integrate predicted values into an index
- Any other custom logic

To support these scenarios, you can implement custom skills as web-hosted services (such as Azure Functions) that support the required interface for integration into a skillset.

![A diagram showing how a skillset in an Azure AI Search solution connects to an Azure function to integrate a custom skill.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/create-enrichment-pipeline-azure-cognitive-search/media/enrichment-pipeline.png)

In this module you will learn how to:

- Implement a custom skill for Azure AI Search
- Integrate a custom skill into an Azure AI Search skillset

Note

This module assumes you already know how to create and use an Azure AI Search solution that includes built-in skills. If not, complete the [Create an Azure AI Search solution](https://learn.microsoft.com/en-us/training/modules/create-azure-cognitive-search-solution/) module first.
# Create a custom skill

Your custom skill must implement the expected schema for input and output data that is expected by skills in an Azure AI Search skillset.

## Input Schema

The input schema for a custom skill defines a JSON structure containing a record for each document to be processed. Each document has a unique identifier, and a data payload with one or more inputs, like this:

JSON

```
{
    "values": [
      {
        "recordId": "<unique_identifier>",
        "data":
           {
             "<input1_name>":  "<input1_value>",
             "<input2_name>": "<input2_value>",
             ...
           }
      },
      {
        "recordId": "<unique_identifier>",
        "data":
           {
             "<input1_name>":  "<input1_value>",
             "<input2_name>": "<input2_value>",
             ...
           }
      },
      ...
    ]
}
```

## Output schema

The schema for the results returned by your custom skill reflects the input schema. It is assumed that the output contains a record for each input record, with either the results produced by the skill or details of any errors that occurred.

JSON

```
{
    "values": [
      {
        "recordId": "<unique_identifier_from_input>",
        "data":
           {
             "<output1_name>":  "<output1_value>",
              ...
           },
         "errors": [...],
         "warnings": [...]
      },
      {
        "recordId": "< unique_identifier_from_input>",
        "data":
           {
             "<output1_name>":  "<output1_value>",
              ...
           },
         "errors": [...],
         "warnings": [...]
      },
      ...
    ]
}
```

The output value in this schema is a _property bag_ that can contain any JSON structure, reflecting the fact that index fields aren't necessarily simple data values, but can contain complex types.

# Add a custom skill to a skillset

To integrate a custom skill into your indexing solution, you must add a skill for it to a skillset using the **Custom.WebApiSkill** skill type.

The skill definition must:

- Specify the URI to your web API endpoint, including parameters and headers if necessary.
- Set the context to specify at which point in the document hierarchy the skill should be called
- Assign input values, usually from existing document fields
- Store output in a new field, optionally specifying a target field name (otherwise the output name is used)

JSON

```
{
    "skills": [
      ...,
      {
        "@odata.type": "#Microsoft.Skills.Custom.WebApiSkill",
        "description": "<custom skill description>",
        "uri": "https://<web_api_endpoint>?<params>",
        "httpHeaders": {
            "<header_name>": "<header_value>"
        },
        "context": "/document/<where_to_apply_skill>",
        "inputs": [
          {
            "name": "<input1_name>",
            "source": "/document/<path_to_input_field>"
          }
        ],
        "outputs": [
          {
            "name": "<output1_name>",
            "targetName": "<optional_field_name>"
          }
        ]
      }
  ]
}
```