---
title: Get observed people detection and matched faces insights in Azure AI Video Indexer
description: Observed people detection and matched faces help you find, analyze, and summarize people in videos. Learn how to get insights and download results.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/10/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
# customer intent: As a video analyst, I want to detect and identify people in videos so that I can quickly find and analyze specific individuals.
---

# Get observed people detection and matched faces insights

> [!IMPORTANT]
> Face identification, customization, and celebrity recognition features access is limited based on eligibility and usage criteria in order to support our Responsible AI principles. Face identification, customization, and celebrity recognition features are only available to Microsoft managed customers and partners. Use the [Face Recognition intake form](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUQjA5SkYzNDM4TkcwQzNEOE1NVEdKUUlRRCQlQCN0PWcu) to apply for access.

Observed people detection and matched faces automatically detect and match people in media files. Observed people detection and matched faces can be set to display insights on people, their clothing, and the exact timeframe of their appearance.

In the web portal, the resulting insights are displayed in a categorized list in the Insights tab. The tab includes a thumbnail of each person and their ID. Clicking the thumbnail of a person displays the matched person (the corresponding face in the People insight). Insights are also generated in a categorized list in a JSON file. The file includes the thumbnail ID of the person, the percentage of time appearing in the file, a Wiki link (if they're a celebrity), and confidence level.

## Observed people detection, detected clothing, and matched faces use cases

- Improving efficiency by deep searching for matched people in organizational archives for insight on specific celebrities, for example when creating promos and trailers.
- Improved efficiency when creating feature stories, for example, searching for people wearing a red shirt in the archives of a football game at a News or Sports agency.  
- Create a summary out of a long video, like court evidence of a specific person’s appearance in a video, using the same detected person’s ID.
- Learn and analyze trends over time, for example—how customers move across aisles in a shopping mall or how much time they spend in checkout lines.

The **matched faces** and **detected clothing** features are available when indexing your file by choosing the **Advanced** -> **Video + audio indexing** preset.

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
"observedPeople": [
    {
        "id": 1,
        "thumbnailId": "d09ad62e-e0a4-42e5-8ca9-9a640c686596",
        "clothing": [
            {
                "id": 1,
                "type": "sleeve",
                "properties": {
                    "length": "short"
                }
            },
            {
                "id": 2,
                "type": "pants",
                "properties": {
                    "length": "short"
                }
            }
        ],
        "matchingFace": {
            "id": 1310,
            "confidence": 0.3819
        },
        "instances": [
            {
                "adjustedStart": "0:00:34.8681666",
                "adjustedEnd": "0:00:36.0026333",
                "start": "0:00:34.8681666",
                "end": "0:00:36.0026333"
            },
            {
                "adjustedStart": "0:00:36.6699666",
                "adjustedEnd": "0:00:36.7367",
                "start": "0:00:36.6699666",
                "end": "0:00:36.7367"
            },
            {
                "adjustedStart": "0:00:37.2038333",
                "adjustedEnd": "0:00:39.6729666",
                "start": "0:00:37.2038333",
                "end": "0:00:39.6729666"
            }
        ]
    }
]
```

> [!IMPORTANT]
> Read the [transparency note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context) for all VI features. Each insight also has its own transparency note.

[!INCLUDE [transparency-observed-people-detection-matched-faces](./includes/transparency-observed-people-detection-matched-faces.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

## Related content

- [Azure AI Video Indexer documentation](index.yml)