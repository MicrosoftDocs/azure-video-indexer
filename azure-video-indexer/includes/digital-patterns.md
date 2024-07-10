---
title: Slate detection
ms.service: azure-video-indexer
ms.topic: include
ms.date: 07/09/2024
ms.author: inhenkel
---

## Post-production: digital patterns

Digital patterns detection detects [color bars](https://en.wikipedia.org/wiki/SMPTE_color_bars) used during filming. Digital patterns is part of the post-production insights that you can select in the web portal [advanced settings](../indexing-configuration-guide.md?#advanced-settings) when you upload and index the file.

## Digital patterns use cases

Digital patterns detection is most commonly used for color correction during post-production editing of visual media.

[!INCLUDE [Insights introductory paragraph](insights-intro-paragraph.md)]

### [Example responses](#tab/patternsresponse)

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
|`name`|The name of the element. For example, "SMPTE color bars".|
|`displayName`| The friendly/display name.
|`thumbnailId`|The ID of the thumbnail.|
|`instances`|A list of time ranges where this element appeared.|

### [Components](#tab/patternscomponents)

No components defined.

### [Transparency notes](#tab/patternstransnote)

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

- There can be a mismatch if the input video is of low quality (for example – old Analog recordings). 
- The digital patterns will be identified over the 10 min of the beginning and 10 min of the ending part of the video.

### [Sample code](#tab/patternssamplecode)

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

---