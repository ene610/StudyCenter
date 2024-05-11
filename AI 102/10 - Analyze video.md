# Introduction

It's increasingly common for organizations and individuals to generate content in video format. For example, you might use a cellphone to capture a live event, or you might record a teleconference that combines webcam footage and presentation of slides or documents. As a result, a great deal of information is encapsulated in video files, and you may need to extract this information for analysis or to support indexing for searchability.

In this module, you will learn how to use the **Azure Video Indexer** service to analyze videos.

After completing this module, you’ll be able to:

- Describe Azure Video Indexer capabilities.
- Extract custom insights.
- Use Azure Video Indexer widgets and APIs.
# Understand Azure Video Indexer capabilities

Completed 100 XP

- 3 minutes

The **Azure Video Indexer** service is designed to help you extract information from videos. It provides functionality that you can use for:

- _Facial recognition_ - detecting the presence of individual people in the image. This requires [Limited Access](https://aka.ms/cog-services-limited-access) approval.
- _Optical character recognition_ - reading text in the video.
- _Speech transcription_ - creating a text transcript of spoken dialog in the video.
- _Topics_ - identification of key topics discussed in the video.
- _Sentiment_ - analysis of how positive or negative segments within the video are.
- _Labels_ - label tags that identify key objects or themes throughout the video.
- _Content moderation_ - detection of adult or violent themes in the video.
- _Scene segmentation_ - a breakdown of the video into its constituent scenes.

The Video Analyzer service provides a portal website that you can use to upload, view, and analyze videos interactively.

![The Video Analyzer portal](https://learn.microsoft.com/en-gb/training/wwl-data-ai/analyze-video/media/video-indexer-portal.png)
# Extract custom insights

Completed 100 XP

- 3 minutes

Azure Video Indexer includes predefined models that can recognize well-known celebrities, do OCR, and transcribe spoken phrases into text. You can extend the recognition capabilities of Video Analyzer by creating custom models for:

- **People**. Add images of the faces of people you want to recognize in videos, and train a model. Video Indexer will then recognize these people in all of your videos.
    
    Note
    
    This only works after [Limited Access](https://aka.ms/cog-services-limited-access) approval, adhering to our Responsible AI standard.
    
- **Language**. If your organization uses specific terminology that may not be in common usage, you can train a custom model to detect and transcribe it.
- **Brands**. You can train a model to recognize specific names as brands, for example to identify products, projects, or companies that are relevant to your business.
# Use Video Analyzer widgets and APIs

Completed 100 XP

- 3 minutes

While you can perform all video analysis tasks in the Azure Video Indexer portal, you may want to incorporate the service into custom applications. There are two ways you can accomplish this.

## Azure Video Indexer widgets

The widgets used in the Azure Video Indexer portal to play, analyze, and edit videos can be embedded in your own custom HTML interfaces. You can use this technique to share insights from specific videos with others without giving them full access to your account in the Azure Video Indexer portal.

![Video Analyzer widgets in a custom web page](https://learn.microsoft.com/en-gb/training/wwl-data-ai/analyze-video/media/widgets.png)

## Azure Video Indexer API

Azure Video Indexer provides a REST API that you can use to obtain information about your account, including an access token.

HTTP

```
https://api.videoindexer.ai/Auth/<location>/Accounts/<accountId>/AccessToken
```

You can then use your token to consume the REST API and automate video indexing tasks, creating projects, retrieving insights, and creating or deleting custom models.

For example, a GET call to `https://api.videoindexer.ai/<location>/Accounts/<accountId>/Customization/CustomLogos/Logos/<logoId>?<accessToken>` REST endpoint returns the specified logo. In another example, you can send a GET request to `https://api.videoindexer.ai/<location>/Accounts/<accountId>/Videos?<accessToken>`, which returns details of videos in your account, similar to the following JSON example:

JSON

```
{
    "accountId": "SampleAccountId",
    "id": "30e66ec1b1",
    "partition": null,
    "externalId": null,
    "metadata": null,
    "name": "test3",
    "description": null,
    "created": "2018-04-25T16=50=00.967+00=00",
    "lastModified": "2018-04-25T16=58=13.409+00=00",
    "lastIndexed": "2018-04-25T16=50=12.991+00=00",
    "privacyMode": "Private",
    "userName": "SampleUserName",
    "isOwned": true,
    "isBase": true,
    "state": "Processing",
    "processingProgress": "",
    "durationInSeconds": 13,
    "thumbnailVideoId": "30e66ec1b1",
    "thumbnailId": "55848b7b-8be7-4285-893e-cdc366e09133",
    "social": {
        "likedByUser": false,
        "likes": 0,
        "views": 0
    },
    "searchMatches": [],
    "indexingPreset": "Default",
    "streamingPreset": "Default",
    "sourceLanguage": "en-US"
}
```

## Deploy with ARM template

Azure Resource Manager (ARM) templates are available to create the Azure AI Video Indexer resource in your subscription, based on the parameters specified in the template file.

For a full list of available APIs, see the [Video Indexer Developer Portal](https://api-portal.videoindexer.ai/).