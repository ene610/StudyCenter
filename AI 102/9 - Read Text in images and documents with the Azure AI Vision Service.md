# Introduction

Suppose you are given thousands of images and asked to transfer the text on the images to a computer database. The scanned images have text organized in different formats and contain multiple languages. What are some ways you could complete the project in a reasonable time frame and make sure the data is entered with a high degree of accuracy?

Companies around the world are tackling similar scenarios every day. Without AI services, it would be challenging to complete the project, especially if it were to change in scale.

Using AI services, we can treat this project as an Azure AI Vision scenario and apply Optical Character Recognition (OCR). OCR allows you to extract text from images, such as photos of street signs and products, as well as from documents — such as handwritten or unstructured documents.

To build an automated AI solution, you need to train machine learning models to cover many use cases. Azure AI Vision service gives access to advanced algorithms for processing images and returns data to secure storage.

In this module, you'll learn how to:

- Identify how the Azure AI Vision service enables you to read text from images
- Use the Azure AI Vision service with SDKs and the REST API
- Develop an application that can read printed and handwritten text
# Explore Azure AI Vision options for reading text

Completed 100 XP

- 3 minutes

Azure AI provides two different features that read text from documents and images, one in the Azure AI Vision Service, the other in Azure AI Document Intelligence. There is overlap in what each service provides, however each is optimized for results depending on what the input is.

- **Image Analysis** Optical character recognition (OCR):
    - Use this feature for general, unstructured documents with smaller amount of text, or images that contain text.
    - Results are returned immediately (synchronous) from a single API call.
    - Has functionality for analyzing images past extracting text, including object detection, describing or categorizing an image, generating smart-cropped thumbnails and more.
    - Examples include: street signs, handwritten notes, and store signs.
- **Document Intelligence**:
    - Use this service to read small to large volumes of text from images and PDF documents.
    - This service uses context and structure of the document to improve accuracy.
    - The initial function call returns an asynchronous operation ID, which must be used in a subsequent call to retrieve the results.
    - Examples include: receipts, articles, and invoices.

You can access both technologies via the REST API or a client library. In this module, we'll focus on the OCR feature in **Image Analysis**. If you'd like to learn more about **Document Intelligence**, [reading this module](https://learn.microsoft.com/en-us/training/modules/use-prebuilt-form-recognizer-models/) will provide a good introduction.

# Use the Read API

Completed 100 XP

- 3 minutes

To use the Read OCR feature, call the **ImageAnalysis** function (REST API or equivalent SDK method), passing the image URL or binary data, and optionally specifying a gender neutral caption or the language the text is written in (with a default value of **en** for English).

To make an OCR request to **ImageAnalysis**, specify the visual feature as `READ`.

**C#**

C#

```
ImageAnalysisResult result = client.Analyze(
    <image-to-analyze>,
    VisualFeatures.Read);
```

**Python**

Python

```
result = client.analyze(
    image_url=<image_to_analyze>,
    visual_features=[VisualFeatures.READ]
)
```

If using the REST API, specify the feature as `read`.

rest

```
https://<endpoint>/computervision/imageanalysis:analyze?features=read&...
```

The results of the Read OCR function are returned synchronously, either as JSON or the language specific object of a similar structure. These results are broken down in _blocks_ (with the current service only using one block), then _lines_, and then _words_. Additionally, the text values are included at both the _line_ and _word_ levels, making it easier to read entire lines of text if you don't need to extract text at the individual _word_ level.

JSON

```
{
    "metadata":
    {
        "width": 500,
        "height": 430
    },
    "readResult":
    {
        "blocks":
        [
            {
                "lines":
                [
                    {
                        "text": "Hello World!",
                        "boundingPolygon":
                        [
                            {"x":251,"y":265},
                            {"x":673,"y":260},
                            {"x":674,"y":308},
                            {"x":252,"y":318}
                        ],
                        "words":
                        [
                            {
                                "text":"Hello",
                                "boundingPolygon":
                                [
                                    {"x":252,"y":267},
                                    {"x":307,"y":265},
                                    {"x":307,"y":318},
                                    {"x":253,"y":318}
                                ],
                            "confidence":0.996
                            },
                            {
                                "text":"World!",
                                "boundingPolygon":
                                [
                                    {"x":318,"y":264},
                                    {"x":386,"y":263},
                                    {"x":387,"y":316},
                                    {"x":319,"y":318}
                                ],
                                "confidence":0.99
                            }
                        ]
                    },
                ]
            }
        ]
    }
}
```
