---
title: Search for exact moments in videos with Azure AI Video Indexer
description: Learn how to search for exact moments in videos using Azure AI Video Indexer.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
ms.custom: sfi-image-nochange
appliesto:
  - Cloud-based Azure AI Video Indexer
---

# Search for exact moments in videos with Azure AI Video Indexer

This topic shows you how to use the Azure AI Video Indexer website to search for exact moments in videos.

1. Go to the [Azure AI Video Indexer](https://www.videoindexer.ai/) website and sign in.
1. Specify the search keywords and the search are performed among all videos in your account's library. 

    You can filter your search by selecting **Filters**. In the following example, you search for *Microsoft* that appears as an on-screen text only (OCR).

1. Press **Search** to see the result.

    If you select one of the results, the player brings you to that exact moment in the video.
1. View and search the summarized insights of the video by clicking **Play** on the video or selecting one of your original search results. 

    You can view, search, and edit the **insights**. When you select one of the insights, the player brings you to that exact moment in the video.

    If you embed the video through Azure AI Video Indexer widgets, you can achieve the player/insights view and synchronization in your app. For more information, see [Embed Azure AI Video Indexer widgets into your app](video-indexer-embed-widgets.md).

1. You can view, search, and edit the transcripts by clicking on the **Timeline** tab.

    To edit the text, select **Edit** from the top-right corner and change the text as you need. 

    You can also translate and download the transcripts by selecting the appropriate option from the top-right corner. 

## Embed, download, create projects

You can embed your video by selecting **</>Embed** under your video. For details, see [Embed visual widgets in your application](video-indexer-embed-widgets.md).

You can download the source video, insights of the video, transcripts by clicking **Download** under your video.

You can create a clip based on your video of specific lines and moments by clicking **Open in editor**. Then editing the video, and saving the project. For details, see [Use your videos' deep insights](use-editor-create-project.md).
