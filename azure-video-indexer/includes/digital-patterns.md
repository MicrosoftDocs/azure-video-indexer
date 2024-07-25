---
title: Digital patterns
ms.service: azure-video-indexer
ms.topic: include
ms.date: 07/25/2024
ms.author: inhenkel
---

## Post-production: digital patterns

[!INCLUDE [digital patterns description](digital-patterns-description.md)]

## Digital patterns use cases

Digital patterns detection is most commonly used for color correction during post-production editing of visual media.

[!INCLUDE [get insights with the web portal](get-insights-web-portal.md)]
[!INCLUDE [get insights with the API](get-insights-api.md)]

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
|`name`|The name of the element. For example, "SMPTE color bars".|
|`displayName`| The friendly/display name.
|`thumbnailId`|The ID of the thumbnail.|
|`instances`|A list of time ranges where this element appeared.|

## Components

No components defined.

## Transparency notes

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

- There can be a mismatch if the input video is of low quality (for example – old Analog recordings). 
- The digital patterns will be identified over the 10 min of the beginning and 10 min of the ending part of the video.

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)
