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

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

[!INCLUDE [Gate notice](./includes/face-limited-access.md)]

Azure AI Video Indexer supports celebrity recognition in your videos. The celebrity recognition feature covers approximately one million faces based on commonly requested data sources such as IMDB, Wikipedia, and top LinkedIn influencers. Faces that aren't recognized by Azure AI Video Indexer are still detected, but are left unnamed. You can build custom Person models and enable Azure AI Video Indexer to recognize faces that aren't recognized by default. You can build these Person models by pairing a person's name with image files of the person's face.

You can benefit from creating multiple Person models per account. For example, if the content in your account is meant to be sorted into different channels, you might want to create a separate Person model for each channel. 

> [!NOTE]
> Each Person model supports up to 1 million people and each account has a limit of 50 Person models. 

Once a model is created, you can use it by providing the model ID of a specific Person model when uploading/indexing or re-indexing a video. Training a new face for a video updates the associated custom model. 

> [!TIP]
> If you don't need the multiple Person model support, don't assign a Person model ID to your video when uploading/indexing or re-indexing. In this case, Azure AI Video Indexer will use the default Person model in your account. 

You can use the Azure AI Video Indexer website to edit faces that were detected in a video and to manage multiple custom Person models in your account, as described in the [Customize a Person model using the website](customize-person-model-with-website.md) article. You can also use the API, as described in [Customize a Person model using APIs](customize-person-model-with-api.md).
