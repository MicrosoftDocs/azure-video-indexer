---
title: Get labels identification insights
description: This article shows you how to get the Azure AI Video Indexer labels identification detection insights.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/03/2025
ms.service: azure-video-indexer
ms.topic: how-to
---

# Get labels identification insights

Labels identification is an Azure AI Video Indexer feature that identifies visual objects, like sunglasses, or actions, like swimming, in the video footage of a media file. The feature includes many label categories. After extraction, you see label instances in the Insights tab, and you can translate them into over 50 languages. Select a label to open the instance in the media file. Select **Play Previous** or **Play Next** to see more instances.

## Labels identification use cases 

- Extracting labels from frames for contextual advertising or branding. For example, placing an ad for beer following footage on a beach.
- Creating a verbal description of footage to enhance accessibility for the visually impaired, for example a background storyteller in movies. 
- Deep searching media archives for insights on specific objects to create feature stories for the news.
- Using relevant labels to create content for trailers, highlights reels, social media, or new clips.

## View the insight JSON with the web portal

After you upload and index a video, download insights in JSON format from the web portal.

1. Select the **Library** tab.
1. Select the media you want.
1. Select **Download**, and then select **Insights (JSON)**. The JSON file opens in a new browser tab.
1. Find the key pair described in the example response.

## Use the API

1. Use a [Get Video Index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Index) request. Pass `&includeSummarizedInsights=false`.
2. Find the key pairs described in the example response.

## Example response

```json
    "labels": [
        {
        "id": 1,
        "name": "human face",
        "language": "en-US",
        "instances": [
            {
            "confidence": 0.9987,
            "adjustedStart": "0:00:00",
            "adjustedEnd": "0:00:25.6",
            "start": "0:00:00",
            "end": "0:00:25.6"
            },
            {
            "confidence": 0.9989,
            "adjustedStart": "0:01:21.067",
            "adjustedEnd": "0:01:41.334",
            "start": "0:01:21.067",
            "end": "0:01:41.334"
            }
        ]
        },
        {
        "id": 2,
        "name": "person",
        "referenceId": "person",
        "language": "en-US",
        "instances": [
            {
            "confidence": 0.9959,
            "adjustedStart": "0:00:00",
            "adjustedEnd": "0:00:26.667",
            "start": "0:00:00",
            "end": "0:00:26.667"
            },
            {
            "confidence": 0.9974,
            "adjustedStart": "0:01:21.067",
            "adjustedEnd": "0:01:41.334",
            "start": "0:01:21.067",
            "end": "0:01:41.334"
            }
        ]
        },
``` 

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

[!INCLUDE [transparency-labels-identification](transparency-labels-identification.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

