---
title: Customize a Person model in Azure AI Video Indexer  
description: This article gives an overview of what is a Person model in Azure AI Video Indexer and how to customize it. 
ms.topic: conceptual
ms.date: 11/16/2023
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Customize a Person model in Azure AI Video Indexer 

[!INCLUDE [AMS AVI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

[!INCLUDE [Gate notice](./includes/face-limited-access.md)]

Azure AI Video Indexer supports celebrity recognition in your videos. The celebrity recognition feature covers approximately one million faces based on commonly requested data sources such as IMDB, Wikipedia, and top LinkedIn influencers. Faces that aren't recognized by Azure AI Video Indexer are still detected, but are left unnamed. You can build custom Person models and enable Azure AI Video Indexer to recognize faces that aren't recognized by default. You can build these Person models by pairing a person's name with image files of the person's face.

You can benefit from creating multiple Person models per account. For example, if the content in your account is meant to be sorted into different channels, you might want to create a separate Person model for each channel. 

> [!NOTE]
> Each Person model supports up to 1 million people and each account has a limit of 50 Person models. 

Once a model is created, you can use it by providing the model ID of a specific Person model when uploading/indexing or re-indexing a video. Training a new face for a video updates the associated custom model. 

> [!TIP]
> If you don't need the multiple Person model support, don't assign a Person model ID to your video when uploading/indexing or re-indexing. In this case, Azure AI Video Indexer will use the default Person model in your account. 

You can use the Azure AI Video Indexer website to edit faces that were detected in a video and to manage multiple custom Person models in your account, as described in the [Customize a Person model using the website](customize-person-model-with-website.md) article. You can also use the API, as described in [Customize a Person model using APIs](customize-person-model-with-api.md).

Here are some other custom Person model capabilities you can use:

## Get an indication of the quality of your people model

You can get an indication on the quality of your customized People model (poor, fair, good). The quality is determined by the number of images used for labeling with the more images you use to label a person, the higher the probability to identify the person correctly. For example, the probability of identifying a person with 24 labeled images is higher than the probability of identifying a person with 2 labeled images. You can see the number of images used for labeling each person in your customized People model page.

:::image type="content" source="media/common/people-model-quality.jpg" lightbox="media/common/people-model-quality.jpg" alt-text="Screenshot of the video indexer interface showing the quality of people model results":::

## Choose the custom people model as default

You can now choose a customized People model as default on the VI account user level, so you don't have to keep selecting the model name for every video upload. This will save you time and effort when you upload videos that need to be analyzed by your customized People model.

## Group unknown people in the video (Preview)
You can see the unknown people in your videos grouped by their appearance similarity. This will help you label the unknown people more easily and quickly, and to improve the accuracy of your customized People model. This could, for example, help you to label a local celebrity or a local politician. You can see the grouping of unknown people in your customization page.  Choose **people** and then navigate to the **unknown people** tab. 

:::image type="content" source="media/common/grouping-unknown.jpg" lightbox="media/common/grouping-unknown.jpg" alt-text="Screen shot of video indexer interface for grouping people identified in video":::

## Search results with max confidence score for identified person name: 
You can search for the name of an identified person and get the timestamp for when the person appears in the video along with the maximum confidence score. This helps you decide what are the most relevant videos to explore. For example, you can search for “John Smith” and get the videos where John Smith is recognized by your customized People model and the confidence score for each video.

:::image type="content" source="media/common/person-max-confidence.jpg" alt-text="screenshot of the video indexer infterface showing the max confidence of a result":::
