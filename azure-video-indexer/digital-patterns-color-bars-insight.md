---
title: Get digital patterns with color bars insights in Azure AI Video Indexer
description: Learn how to get digital patterns with color bars insights with Azure AI Video Indexer.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/03/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
#customer intent: As an Azure AI Video Indexer user, I want to learn how get color bar insights with Azure AI Video Indexer.
---

# Get digital patterns with color bars insights

This article describes how to get insights for view digital patterns with color bars in Azure AI Video Indexer. Digital patterns detection is a post-production insight that identifies color bars used during filming, which can be useful for color correction and other post-production tasks.

## Post-production: digital patterns

Digital patterns detection finds [color bars](https://en.wikipedia.org/wiki/SMPTE_color_bars) used during filming. Digital patterns are part of post-production insights that you select in the web portal using **Slate detection** in [advanced settings](indexing-configuration-guide.md?#advanced-settings) when you upload and index the file.

## Digital patterns use cases

Digital patterns detection is most commonly used for color correction during post-production editing of visual media.

## View the insight JSON with the web portal

After you upload and index a video, download insights in JSON format from the web portal.

1. Select the **Library** tab.
1. Select the media you want.
1. Select **Download**, and then select **Insights (JSON)**. The JSON file opens in a new browser tab.
1. Find the key pair described in the example response.

## Use the API

1. Use a [Get Video Index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Index) request. Pass `&includeSummarizedInsights=false`.
2. Find the key pairs described in the example response.

## Example responses

You can use digital patterns detection for detecting color bars and test cards.

```json
  "framePatterns": [
        {
        "id": 1,
        "patternType": "ColorBars",
        "name": "SMPTE color bars",
        "displayName": "null",
        "thumbnailId": "47979a6b-63bc-44bb-b917-0600f78ec9ed",
        "instances": [
                        {
                            "confidence": 0.512,
                            "adjustedStart": "0:00:04.906261",
                            "adjustedEnd": "0:00:05.321406",
                            "start": "0:00:04.906261",
                            "end": "0:00:05.321406"
                        }
                    ]
                },
```

|Name|Description|
|---|---|
|`id`|The digital pattern ID.|
|`patternType`|The following types are supported: ColorBars, TestCards.|
|`confidence`|The confidence level for color bar accuracy.|
|`name`|The name of the element. For example, `SMPTE color bars`.|
|`displayName`| The friendly/display name.
|`thumbnailId`|The ID of the thumbnail.|
|`instances`|A list of time ranges where this element appeared.|

## Components

No components defined.

## Transparency notes

> [!IMPORTANT]
> Read the [transparency note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context) for all VI features. Each insight also has its own transparency note.

- There can be a mismatch if the input video is of low quality (for example – old Analog recordings). 
- The digital patterns are identified over the 10 min of the beginning and 10 min of the ending part of the video.

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

## Related content

- [Azure AI Video Indexer documentation](index.yml)