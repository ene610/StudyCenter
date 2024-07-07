# Introduction

Azure AI Vision is a branch of artificial intelligence (AI) in which software interprets visual input, often from images or video feeds.

In this module, you'll learn how to use the **Azure AI Vision** service to extract information from images.

After completing this module, you’ll be able to:

- Provision an Azure AI Vision resource.
- Analyze an image.
- Remove an image background.
- Generate a smart cropped thumbnail.
# Provision an Azure AI Vision resource

The **Azure AI Vision** service is designed to help you extract information from images. It provides functionality that you can use for:

- _Description and tag generation_ - determining an appropriate caption for an image, and identifying relevant "tags" that can be used as keywords to indicate its subject.
- _Object detection_ - detecting the presence and location of specific objects within the image.
- _People detection_ - detecting the presence, location, and features of people in the image.
- _Image metadata, color, and type analysis_ - determining the format and size of an image, its dominant color palette, and whether it contains clip art.
- _Category identification_ - identifying an appropriate categorization for the image, and if it contains any known landmarks.
- _Background removal_ - detecting the background in an image and output the image with the background transparent or a greyscale alpha matte image.
- _Moderation rating_ - determine if the image includes any adult or violent content.
- _Optical character recognition_ - reading text in the image.
- _Smart thumbnail generation_ - identifying the main region of interest in the image to create a smaller "thumbnail" version.

![A conceptual image of the Azure AI Vision service](https://learn.microsoft.com/en-gb/training/wwl-data-ai/analyze-images/media/computer-vision.png)

You can provision **Azure AI Vision** as a single-service resource, or you can use the Azure AI Vision API in a multi-service **Azure AI Services** resource.

Note

In this module, we'll focus on the image analysis and thumbnail generation capabilities of the Azure AI Vision service. To learn how to use the Azure AI Vision service for optical character recognition, check out the [Read Text in images and documents with the Azure AI Vision service](https://learn.microsoft.com/en-us/training/modules/read-text-images-documents-with-computer-vision-service/) module.

# Analyze an image

Choose your development language

To analyze an image, you can use the **Analyze Image** REST method or the equivalent method in the SDK for your preferred programming language, specifying the visual features you want to include in the analysis (and if you select categories, whether or not to include details of celebrities or landmarks). This method returns a JSON document containing the requested information.

Note

Detection of celebrities will require getting approved through a [Limited Access policy](https://aka.ms/cog-services-limited-access). You can read more about the [addition of this policy](https://azure.microsoft.com/blog/responsible-ai-investments-and-safeguards-for-facial-recognition/) to our Responsible AI standard. Celebrity recognition is seen in some screenshots, however is not included in the lab.

Python

```
from azure.ai.vision.imageanalysis import ImageAnalysisClient
from azure.ai.vision.imageanalysis.models import VisualFeatures
from azure.core.credentials import AzureKeyCredential

client = ImageAnalysisClient(
    endpoint=os.environ["ENDPOINT"],
    credential=AzureKeyCredential(os.environ["KEY"])
)

result = client.analyze(
    image_url="<url>",
    visual_features=[VisualFeatures.CAPTION, VisualFeatures.READ],
    gender_neutral_caption=True,
    language="en",
)
```

Available visual features are contained in the `VisualFeatures` enum:

- VisualFeatures.TAGS: Identifies tags about the image, including objects, scenery, setting, and actions
- VisualFeatures.OBJECTS: Returns the bounding box for each detected object
- VisualFeatures.CAPTION: Generates a caption of the image in natural language
- VisualFeatures.DENSE_CAPTIONS: Generates more detailed captions for the objects detected
- VisualFeatures.PEOPLE: Returns the bounding box for detected people
- VisualFeatures.SMART_CROPS: Returns the bounding box of the specified aspect ratio for the area of interest
- VisualFeatures.READ: Extracts readable text

Specifying the visual features you want analyzed in the image determines what information the response will contain. Most responses will contain a bounding box (if a location in the image is reasonable) or a confidence score (for features such as tags or captions).

The JSON response for image analysis looks similar to this example, depending on your requested features:

JSON

```
{
  "apim-request-id": "abcde-1234-5678-9012-f1g2h3i4j5k6",
  "modelVersion": "<version>",
  "denseCaptionsResult": {
    "values": [
      {
        "text": "a house in the woods",
        "confidence": 0.7055229544639587,
        "boundingBox": {
          "x": 0,
          "y": 0,
          "w": 640,
          "h": 640
        }
      },
      {
        "text": "a trailer with a door and windows",
        "confidence": 0.6675070524215698,
        "boundingBox": {
          "x": 214,
          "y": 434,
          "w": 154,
          "h": 108
        }
      }
    ]
  },
  "metadata": {
    "width": 640,
    "height": 640
  }
}
```

# Generate a smart-cropped thumbnail and remove background

Thumbnails are often used to provide smaller versions of images in applications and websites. For example, a tourism site might display a list of tourist attractions in a city with a small, representative thumbnail image for each attraction; and only display the full image when the user selects the "details" page for an individual attraction.

The Azure AI Vision service enables you to create a thumbnail with different dimensions (and aspect ratio) from the source image, and optionally to use image analysis to determine the _region of interest_ in the image (its main subject) and make that the focus of the thumbnail. This ability to determine the region of interest is especially useful when cropping the image to change its aspect ratio.

![A large building cropped to show the region of interest.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/analyze-images/media/smart-cropping.png)

You can specify the aspect ratio of the cropped image (width / height), ranging from `0.75` to `1.80`.

## Remove image background

The background removal feature can split the image into the subject in the foreground, and everything else that is considered background. Azure AI Vision achieves this feature by creating an _alpha matte_ of the foreground subject, which is then used to return either the foreground or the background.

For example, take this image original of a skateboarder.

![A skateboarder performing a trick in front of a concrete wall.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/analyze-images/media/sample-skateboard.jpg)

With the background removed, we get just the skateboarder on a transparent background.

![A skateboarder performing a trick with a black background.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/analyze-images/media/sample-skateboard-no-background.png)

When creating an alpha matte of an image, the result is the foreground in all white, with a black background.

![A silhouette of a skateboarder performing a trick with a black background.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/analyze-images/media/sample-skateboard-alpha-matte.png)

Alpha matte images are helpful when client applications intend to do further processing of an image that requires separation of foreground and background objects.