# Introduction

_Image classification_ is a common computer vision problem that requires software to analyze an image in order to categorize (or _classify_) it. In this module, you will learn how the **Azure AI Custom Vision** service enables you to build your own computer vision models for image classification.

After completing this module, you’ll be able to:

- Provision Azure resources for Azure AI Custom Vision.
- Describe image classification.
- Train an image classifier.
# Provision Azure resources for Azure AI Custom Vision

Completed 100 XP

- 3 minutes

The **Azure AI Custom Vision** service enables you to build your own computer vision models for _image classification_ or _object detection_.

Creating an Azure AI Custom Vision solution involves two tasks:

![An Azure AI Custom Vision service model being trained from existing images, and predicting classes for new images](https://learn.microsoft.com/en-gb/training/wwl-data-ai/classify-images/media/image-classification.png)

1. Use existing (labeled) images to train an Azure AI Custom Vision model.
2. Create a client application that submits new images to your model to generate predictions.

To use the Azure AI Custom Vision service, you must provision two kinds of Azure resource:

- A _training_ resource (used to train your models). This can be:
    - An **Azure AI Services** resource.
    - An **Azure AI Custom Vision (Training)** resource.
- A _prediction_ resource, used by client applications to get predictions from your model. This can be:
    - An **Azure AI Services** resource.
    - An **Azure AI Custom Vision (Prediction)** resource.

You can use a single **Azure AI Services** resource for both training and prediction, and you can mix-and-match resource types (for example, using an **Azure AI Custom Vision (Training)** resource to train a model that you then publish using an **Azure AI Services** resource).

---
# Understand image classification

Completed 100 XP

- 3 minutes

_Image classification_ is a computer vision technique in which a model is trained to predict a class label for an image based on its contents. Usually, the class label relates to the main _subject_ of the image.

For example, the following images have been classified based on the type of fruit they contain.

![Images of fruit, classified as Apple, Banana, and Orange](https://learn.microsoft.com/en-gb/training/wwl-data-ai/classify-images/media/classified-fruit.png)

Models can be trained for multiclass classification (in other words, there are multiple classes, but each image can belong to only one class) or multilabel classification (in other words, an image might be associated with multiple labels).

# Train an image classifier

Completed 100 XP

- 3 minutes

To train an image classification model with the Azure AI Custom Vision service, you can use the Azure AI Custom Vision portal, the Azure AI Custom Vision REST API or SDK, or a combination of both approaches.

In most cases, you'll typically use the Azure AI Custom Vision portal to train your model.

![The Azure AI Custom Vision portal](https://learn.microsoft.com/en-gb/training/wwl-data-ai/classify-images/media/custom-vision-portal.png)

The portal provides a graphical interface that you can use to:

1. Create an image classification project for your model and associate it with a training resource.
2. Upload images, assigning class label tags to them.
3. Review and edit tagged images.
4. Train and evaluate a classification model.
5. Test a trained model.
6. Publish a trained model to a prediction resource.

The REST API and SDKs enable you to perform the same tasks by writing code, which is useful if you need to automate model training and publishing as part of a DevOps process.