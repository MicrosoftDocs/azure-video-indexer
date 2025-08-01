---
title: Things to consider when using Azure AI Video Indexer at scale - Azure
description: This article explains what things to consider when using Azure AI Video Indexer at scale.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 05/30/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
---

# Things to consider when using Azure AI Video Indexer at scale

When using Azure AI Video Indexer to index videos and your archive of videos is growing, consider scaling.

This article answers questions like:

* Are there any technological constraints I need to take into account?
* Is there a smart and efficient way of doing it?
* Can I prevent spending excess money in the process?

The article provides six best practices of how to use Azure AI Video Indexer at scale.

## Consider using a URL over byte array when you upload videos

Azure AI Video Indexer gives you the choice to upload videos from a URL or directly by sending the file as a byte array, the latter comes with some constraints.

First, it has file size limitations. The size of the byte array file is limited to 2 GB compared to the 30-GB upload size limitation while using URL.

Second, consider just some of the issues that can affect your performance and hence your ability to scale:

* Sending files using multi-part means high dependency on your network,
* service reliability,
* connectivity,
* upload speed,
* lost packets somewhere in the world wide web.

:::image type="content" source="./media/considerations-when-use-at-scale/first-consideration.png" alt-text="Diagram for the First consideration for using Azure AI Video Indexer at scale." border="false" lightbox="./media/considerations-when-use-at-scale/first-consideration.png":::

When you upload videos using URL, you just need to provide a path to the location of a media file and Video Indexer takes care of the rest (see the `videoUrl` field in the [upload video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video) API).

> [!TIP]
> Use the `videoUrl` optional parameter of the upload video API. Additionally, you can use [AzCopy](/azure/storage/common/storage-use-azcopy-v10) for a fast and reliable way to get your content to a storage account from which you can submit it to Azure AI Video Indexer using [SAS URL](/azure/storage/common/storage-sas-overview). Azure AI Video Indexer recommends using *readonly* SAS URLs.

## Respect throttling

Azure AI Video Indexer is built to deal with indexing at scale. When you want to get the most out of it, you should also be aware of the system's capabilities and design your integration accordingly. You don't want to send an upload request for a batch of videos just to discover that some of the movies didn't upload and you're receiving an HTTP 429 response code (too many requests). There's an API request limit of 10 requests per second and up to 120 requests per minute.

Azure AI Video Indexer adds a `retry-after` header in the HTTP response. The header specifies when you should attempt your next retry. Make sure you respect it before trying your next request.

:::image type="content" source="./media/considerations-when-use-at-scale/respect-throttling.png" alt-text="Screenshot showing the Too many requests options." border="true" lightbox="./media/considerations-when-use-at-scale/respect-throttling.png":::

## Use callback URL

Instead of repeatedly polling the status of your request upload request, you can add a callback URL and wait for Azure AI Video Indexer to update you. When there's a status change in your upload request, you get a POST notification to the URL you specified.


You can add a callback URL as one of the parameters of the [upload video API](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video). Check out the code samples in [GitHub repo](https://github.com/Azure-Samples/media-services-video-indexer/tree/master/).

For callback URL, you can also use Azure Functions. It's a serverless event-driven platform that can get triggered by HTTP and implement a following flow.

### callBack URL definition

A callback URL is used to notify the customer (through a POST request) about the following events:

- Indexing state change: 
   - Properties:    
    
      |Name|Description|
      |---|---|
      |`id`|The video ID|
      |`state`|The video state|  

   - Example: https:\//test.com/notifyme?projectName=MyProject&id=1234abcd&state=Processed

- Person identified in video:
  - Properties
    
      |Name|Description|
      |---|---|
      |`id`| The video ID|
      |`faceId`|The face ID that appears in the video index|
      |`knownPersonId`|The person ID that is unique within a face model|
      |`personName`|The name of the person|
        
   - Example: https:\//test.com/notifyme?projectName=MyProject&id=1234abcd&faceid=12&knownPersonId=CCA84350-89B7-4262-861C-3CAC796542A5&personName=Inigo_Montoya 

## Use the right indexing parameters for you

When making decisions related to using Azure AI Video Indexer at scale, look at how to get the most out of it with the right parameters for your needs. Think about your use case, by defining different parameters you can save money and make the indexing process for your videos faster. For example, don’t set the preset to streaming if you don't plan to watch the video, don't index video insights if you only need audio insights.

## Index in optimal resolution, not highest resolution

You might be asking, what video quality do you need for indexing your videos?

In many cases, indexing performance has almost no difference between HD (720p) videos and 4K videos. Eventually, you get almost the same insights with the same confidence. The higher the quality of the movie you upload means the higher the file size, and it leads to higher computing power and time needed to upload the video.

For example, for the face detection feature, a higher resolution can help with the scenario where there are many small but contextually important faces. However, it comes with a quadratic increase in runtime and an increased risk of false positives.

Therefore, we recommend you to verify that you get the right results for your use case and to first test it locally. Upload the same video in 720p and in 4K and compare the insights you get.
