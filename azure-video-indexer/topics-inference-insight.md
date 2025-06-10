---
title: Get topics inference insights in Azure AI Video Indexer
description: Get topics inference insights from Azure AI Video Indexer to enhance personalization, deep search, and monetization. See steps and sample code.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/09/2025
ms.service: azure-video-indexer
ms.topic: how-to
#customer intent: As an Azure user, I want to get topics inference insights from Azure AI Video Indexer to enhance personalization, deep search, and monetization.
---

# Get topics inference insights

Topics inference creates inferred insights from transcribed audio, OCR content in visual text, and celebrities the Video Indexer facial recognition model recognizes in the video.

In the web portal, the extracted Topics and categories (when available) are listed in the Insights tab. To jump to the topic in the media file, select a Topic -> Play Previous or Play Next.

## Topics inference use cases

- Personalization using topics inference to match customer interests, for example websites about England posting promotions about English movies or festivals.
- Deep-searching archives for insights on specific topics to create feature stories about companies, personas, or technologies, for example by a news agency. 
- Monetization, increasing the worth of extracted insights. For example, industries like the news or social media that rely on ad revenue can deliver relevant ads by using the extracted insights as other signals to the ad server.

## View the insight JSON with the web portal

After you upload and index a video, download insights in JSON format from the web portal.

1. Select the **Library** tab.
1. Select the media you want.
1. Select **Download**, and then select **Insights (JSON)**. The JSON file opens in a new browser tab.
1. Find the key pair described in the example response.

## Use the API

1. Use a [Get Video Index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Index) request. Pass `&includeSummarizedInsights=false`.
2. Find the key pairs described in the following example response.

## Example response

```json
    "topics": [
      {
        "id": 1,
        "name": "Pens",
        "referenceId": "Category:Pens",
        "referenceUrl": "https://en.wikipedia.org/wiki/Category:Pens",
        "referenceType": "Wikipedia",
        "confidence": 0.6833,
        "iabName": null,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:00:30",
            "adjustedEnd": "0:01:17.5",
            "start": "0:00:30",
            "end": "0:01:17.5"
          }
        ]
      },
      {
        "id": 2,
        "name": "Musical groups",
        "referenceId": "Category:Musical_groups",
        "referenceUrl": "https://en.wikipedia.org/wiki/Category:Musical_groups",
        "referenceType": "Wikipedia",
        "confidence": 0.6812,
        "iabName": null,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:01:10",
            "adjustedEnd": "0:01:17.5",
            "start": "0:01:10",
            "end": "0:01:17.5"
          }
        ]
      },
```

> [!IMPORTANT]
> Read the [transparency note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context) for all VI features. Each insight also has its own transparency note.

[!INCLUDE [transparency-topics-inference](./includes/transparency-topics-inference.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

## Related content

- [Azure AI Video Indexer documentation](index.yml)