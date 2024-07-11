---
title: Labels identification
ms.service: azure-video-indexer
ms.topic: include
ms.date: 07/09/2024
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

### [Example response](#tab/labelsresponse)

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

### [Components](#tab/labelscomponents) 

During the Labels procedure, objects in a media file are processed, as follows:

|Component|Definition|
|---|---|
|Source	|The user uploads the source file for indexing. |
|Tagging|	Images are tagged and labeled. For example, door, chair, woman, headphones, jeans. |
|Filtering and aggregation	|Tags are filtered according to their confidence level and aggregated according to their category.|
|Confidence level|	The estimated confidence level of each label is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|

### [Transparency notes](#tab/labelstransnote)

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

- Carefully consider the accuracy of the results, to promote more accurate detections, check the quality of the video, low quality video might affect the detected insights. 
- Carefully consider when using for law enforcement that Labels potentially can't detect parts of the video. To ensure fair and high-quality decisions, combine Labels with human oversight. 
- Don't use labels identification for decisions that might have serious adverse impacts. Machine learning models can result in undetected or incorrect classification output. Decisions based on incorrect output could have serious adverse impacts. Additionally, it's advisable to include human review of decisions that have the potential for serious impacts on individuals. 

### [Sample code](#tab/labelssamplecode)

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

---
