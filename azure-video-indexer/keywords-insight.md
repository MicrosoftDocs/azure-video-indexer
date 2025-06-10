---
title: Get keywords extraction insights in Azure AI Video Indexer
description: Learn how to get Azure AI Video Indexer keywords extraction insights, view results in the portal or API, and see example JSON output.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/09/2025
ms.service: azure-video-indexer
ms.topic: how-to
# customer intent: As a user of Azure AI Video Indexer, I want to extract keywords from my media files and view the insights in the portal or API, so that I can analyze important keywords and their occurrences.
---

# Get keywords extraction insights

This article explains how to get keywords extraction insights from Azure AI Video Indexer (VI). Keywords extraction finds important keywords in media files and provides insights in both single-language and multi-language media files.

## Keywords extraction use cases

- Personalization of keywords to match customer interests. For example, websites about England posting promotions about English movies or festivals.
- Deep-searching archives for insights on specific keywords to create feature stories about companies, personas, or technologies, for example by a news agency.

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
    "keywords": [
      {
        "id": 1,
        "text": "office insider",
        "confidence": 1,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:00:00",
            "adjustedEnd": "0:00:05.75",
            "start": "0:00:00",
            "end": "0:00:05.75"
          },
          {
            "adjustedStart": "0:01:21.82",
            "adjustedEnd": "0:01:24.7",
            "start": "0:01:21.82",
            "end": "0:01:24.7"
          },
          {
            "adjustedStart": "0:01:31.32",
            "adjustedEnd": "0:01:32.76",
            "start": "0:01:31.32",
            "end": "0:01:32.76"
          },
          {
            "adjustedStart": "0:01:35.8",
            "adjustedEnd": "0:01:37.84",
            "start": "0:01:35.8",
            "end": "0:01:37.84"
          }
        ]
      },
      {
        "id": 2,
        "text": "insider tip",
        "confidence": 0.9975,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:01:14.91",
            "adjustedEnd": "0:01:19.51",
            "start": "0:01:14.91",
            "end": "0:01:19.51"
          }
        ]
      }
```

> [!IMPORTANT]
> Read the [transparency note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context) for all VI features. Each insight also has its own transparency note.

[!INCLUDE [transparency-keywords-extraction](includes/transparency-keywords-extraction.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

## Related content

- [Azure AI Video Indexer documentation](index.yml)