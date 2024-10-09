---
title: Labels identification
ms.service: azure-video-indexer
ms.topic: include
ms.date: 10/09/2024
ms.author: inhenkel
---

## Labels identification

[!INCLUDE [labels identification description](labels-identification-description.md)]

## Labels identification use cases 

- Extracting labels from frames for contextual advertising or branding. For example, placing an ad for beer following footage on a beach.
- Creating a verbal description of footage to enhance accessibility for the visually impaired, for example a background storyteller in movies. 
- Deep searching media archives for insights on specific objects to create feature stories for the news.
- Using relevant labels to create content for trailers, highlights reels, social media, or new clips.

[!INCLUDE [get insights with the web portal](get-insights-web-portal.md)]
[!INCLUDE [get insights with the API](get-insights-api.md)]

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
