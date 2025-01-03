# Introduction

Face detection, analysis, and recognition are all common computer vision challenges for AI systems. The ability to detect when a person is present, identify a person's facial location, or recognize an individual based on their facial features is a key way in which AI systems can exhibit human-like behavior and build empathy with users.

In this module, you'll learn how to detect, analyze, and recognize faces using Azure AI Services.

After completing this module, you’ll be able to:

- Identify options for face detection analysis.
- Describe considerations for face analysis.
- Detect faces with the Azure AI Vision service.
- Describe the capabilities of the Face service.
- Learn about facial recognition.
# Identify options for face detection analysis and identification

There are two Azure AI services that you can use to build solutions that detect faces or people in images.

![The Azure AI Vision and Face services offer facial analysis capabilities](https://learn.microsoft.com/en-gb/training/wwl-data-ai/detect-analyze-recognize-faces/media/face-options.png)

## The Azure AI Vision service

The **Azure AI Vision** service enables you to detect people in an image, as well as returning a bounding box for its location.

## The Face service

The **Face** service offers more comprehensive facial analysis capabilities than the Azure AI Vision service, including:

- Face detection (with bounding box).
- Comprehensive facial feature analysis (including head pose, presence of spectacles, blur, facial landmarks, occlusion and others).
- Face comparison and verification.
- Facial recognition.

Important

Usage of facial recognition, identification, comparison, and verification will require getting approved through a [Limited Access policy](https://aka.ms/cog-services-limited-access). You can read more about the [addition of this policy](https://azure.microsoft.com/blog/responsible-ai-investments-and-safeguards-for-facial-recognition/) to our Responsible AI standard. Facial recognition will be touched on in the rest of this module, but will be unavailable without applying for Limited Access.
# Understand considerations for face analysis

While all applications of artificial intelligence require considerations for responsible and ethical use, system that rely on facial data can be particularly problematic.

When building a solution that uses facial data, considerations include (but aren't limited to):

- **Data privacy and security**. Facial data is personally identifiable, and should be considered sensitive and private. You should ensure that you have implemented adequate protection for facial data used for model training and inferencing.
- **Transparency**. Ensure that users are informed about how their facial data is used, and who will have access to it.
- **Fairness and inclusiveness**. Ensure that your face-based system can't be used in a manner that is prejudicial to individuals based on their appearance, or to unfairly target individuals.


# Detect faces with the Azure AI Vision service

To detect and analyze faces with the Azure AI Vision service, call the **Analyze Image** function (SDK or equivalent REST method), specifying **People** as one of the visual features to be returned.

In images that contain one or more people, the response includes details of their location in the image and the attributes of the detected person, like this:

JSON

```
{ 
  "modelVersion": "2023-10-01",
  "metadata": {
    "width": 400,
    "height": 600
  },
  "peopleResult": {
    "values": [
      {
        "boundingBox": {
          "x": 0,
          "y": 56,
          "w": 101,
          "h": 189
        },
        "confidence": 0.9474349617958069
      },
      {
        "boundingBox": {
          "x": 402,
          "y": 96,
          "w": 124,
          "h": 156
        },
        "confidence": 0.9310565276194865
      },
    ...
    ]
  }
}
```

For more information on Azure AI Vision people detection, see the [People detection concept page](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-people-detection)

Note

Azure AI Vision previously included age and gender prediction, however that has been removed as a safeguard for responsible use. You can read more about our [Responsible AI Investments here](https://azure.microsoft.com/blog/responsible-ai-investments-and-safeguards-for-facial-recognition/).

# Understand capabilities of the face service

The **Face** service provides comprehensive facial detection, analysis, and recognition capabilities.

![The Face service provides a wide range of facial analysis capabilities](https://learn.microsoft.com/en-gb/training/wwl-data-ai/detect-analyze-recognize-faces/media/face-service.png)

The Face service provides functionality that you can use for:

- _Face detection_ - for each detected face, the results include an ID that identifies the face and the bounding box coordinates indicating its location in the image.
- _Face attribute analysis_ - you can return a wide range of facial attributes, including:
    - Head pose (_pitch_, _roll_, and _yaw_ orientation in 3D space)
    - Glasses (_NoGlasses_, _ReadingGlasses_, _Sunglasses_, or _Swimming Goggles_)
    - Blur (_low_, _medium_, or _high_)
    - Exposure (_underExposure_, _goodExposure_, or _overExposure_)
    - Noise (visual noise in the image)
    - Occlusion (objects obscuring the face)
    - Accessories (glasses, headwear, mask)
    - QualityForRecognition (_low_, _medium_, or _high_)
- _Facial landmark location_ - coordinates for key landmarks in relation to facial features (for example, eye corners, pupils, tip of nose, and so on)
- _Face comparison_ - you can compare faces across multiple images for similarity (to find individuals with similar facial features) and verification (to determine that a face in one image is the same person as a face in another image)
- _Facial recognition_ - you can train a model with a collection of faces belonging to specific individuals, and use the model to identify those people in new images.
- _Facial liveness_ - liveness can be used to determine if the input video is a real stream or a fake to prevent bad intentioned individuals from spoofing the recognition system.

You can provision **Face** as a single-service resource, or you can use the Face API in a multi-service **Azure AI Services** resource.

If you want to use the identification, recognition, and verification features of **Face**, you'll need to apply for the [Limited Access policy](https://aka.ms/cog-services-limited-access) and get approval before these features are available.
# Compare and match detected faces

When a face is detected by the Face service, a unique ID is assigned to it and retained in the service resource for 24 hours. The ID is a GUID, with no indication of the individual's identity other than their facial features.

Important

Usage of facial recognition, comparison, and verification will require getting approved through a [Limited Access policy](https://aka.ms/cog-services-limited-access). You can read more about the [addition of this policy](https://azure.microsoft.com/blog/responsible-ai-investments-and-safeguards-for-facial-recognition/) to our Responsible AI standard. Facial recognition will be unavailable to new customers until they are granted the Limited Access policy.

While the detected face ID is cached, subsequent images can be used to compare the new faces to the cached identity and determine if they are _similar_ (in other words, they share similar facial features) or to _verify_ that the same person appears in two images.

![A detected face matched in two images](https://learn.microsoft.com/en-gb/training/wwl-data-ai/detect-analyze-recognize-faces/media/face-matching.png)

This ability to compare faces anonymously can be useful in systems where it's important to confirm that the same person is present on two occasions, without the need to know the actual identity of the person. For example, by taking images of people as they enter and leave a secured space to verify that everyone who entered leaves.

# Implement facial recognition

For scenarios where you need to positively identify individuals, you can train a facial recognition model using face images.

Note

As mentioned in the previous unit, recognition models will require getting approved through a [Limited Access policy](https://aka.ms/cog-services-limited-access).

To train a facial recognition model with the Face service:

1. Create a **Person Group** that defines the set of individuals you want to identify (for example, _employees_).
2. Add a **Person** to the **Person Group** for each individual you want to identify.
3. Add detected faces from multiple images to each **person**, preferably in various poses. The IDs of these faces will no longer expire after 24 hours (so they're now referred to as _persisted_ faces).
4. Train the model.

![Person groups containing Person records with persisted faces](https://learn.microsoft.com/en-gb/training/wwl-data-ai/detect-analyze-recognize-faces/media/person-groups.png)

The trained model is stored in your Face (or Azure AI Services) resource, and can be used by client applications to:

- _Identify_ individuals in images.
- _Verify_ the identity of a detected face.
- Analyze new images to find faces that are _similar_ to a known, persisted face.

---