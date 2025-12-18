---
title: Get object detection insights
description: This article shows you how to get the Azure AI Video Indexer object detection insights.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
appliesto:
  - Azure AI Video Indexer enabled by Azure Arc
  - Cloud-based Azure AI Video Indexer
---

# Get object detection insights

This article shows you how to get the Azure AI Video Indexer object detection insights. Object detection is a feature that detects and tracks objects in videos. It can be used to find objects like cars, handbags, backpacks, and laptops.

## Supported objects

:::row:::
    :::column:::
        - airplane
        - apple
        - backpack
        - banana
        - baseball glove
        - bed
        - bench
        - bicycle
        - boat
        - book
        - bottle
        - bowl
        - broccoli
        - bus
        - cake
    :::column-end:::
    :::column:::
        - car
        - carrot
        - cell phone
        - chair
        - clock
        - computer mouse
        - couch
        - cup
        - dining table
        - donut
        - fire hydrant
        - fork
        - frisbee
    :::column-end:::
    :::column:::
        - hair dryer
        - handbag
        - hot dog
        - keyboard
        - kite
        - knife
        - laptop
        - microwave
        - motorcycle
        - computer mouse
        - necktie
        - orange
        - oven
        - parking meter
        - pizza
        - potted plant
    :::column-end:::
    :::column:::
        - sandwich
        - scissors
        - sink
        - skateboard
        - skis
        - snowboard
        - spoon
        - sports ball
        - stop sign
        - suitcase
        - surfboard
        - teddy bear
    :::column-end:::
    :::column:::
        - tennis racket
        - toaster
        - toilet
        - toothbrush
        - traffic light
        - train
        - umbrella
        - vase
        - wine glass
    :::column-end:::
:::row-end:::

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

Detected and tracked objects appear under `detectedObjects` in the downloaded *insights.json* file. Every time a unique object is detected, the object is given an ID. That object is also tracked, meaning that the model watches for the detected object to return to the frame. If it does, another instance is added to the instances for the object with different start and end times.

In this example, the first car was detected and given an ID of 1 since it was also the first object detected. Then, a different car was detected and that car was given the ID of 23 since it was the twenty-third object detected. Later, the first car appeared again and another instance was added to the JSON. Here's the resulting JSON:

```json
detectedObjects: [
    {
    id: 1,
    type: "Car",
    thumbnailId: "1c0b9fbb-6e05-42e3-96c1-abe2cd48t33",
    displayName: "car",
    wikiDataId: "Q1420",
    instances: [
        {
        confidence: 0.468,
        adjustedStart: "0:00:00",
        adjustedEnd: "0:00:02.44",
        start: "0:00:00",
        end: "0:00:02.44"
        },
        {
        confidence: 0.53,
        adjustedStart: "0:03:00",
        adjustedEnd: "0:00:03.55",
        start: "0:03:00",
        end: "0:00:03.55"
        }    
    ]
    },
    {
    id: 23,
    type: "Car",
    thumbnailId: "1c0b9fbb-6e05-42e3-96c1-abe2cd48t34",
    displayName: "car",
    wikiDataId: "Q1420",
    instances: [
        {
        confidence: 0.427,
        adjustedStart: "0:00:00",
        adjustedEnd: "0:00:14.24",
        start: "0:00:00",
        end: "0:00:14.24"
        }    
    ]
    }
]
```

| **Key** | **Definition** |
| --- | --- |
| ID | Incremental number of IDs of the detected objects in the media file |
| Type | Type of objects,  for example, Car 
| ThumbnailID | GUID representing a single detection of the object |
| displayName | Name to be displayed in the VI portal experience |
| WikiDataID | A unique identifier in the WikiData structure |
| Instances | List of all instances that were tracked  
| Confidence | A score between 0-1 indicating the object detection confidence |
| adjustedStart | adjusted start time of the video when using the editor | 
| adjustedEnd | adjusted end time of the video when using the editor |
| start | the time that the object appears in the frame | 
| end | the time that the object no longer appears in the frame |


## Components

No components are defined for object detection.

## Transparency notes

> [!IMPORTANT]
> Read the [transparency note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context) for all VI features. Each insight also has its own transparency note.

- There are up to 20 detections per frame for standard and advanced processing and 35 tracks per class.
- Object size shouldn't be greater than 90 percent of the frame. Large objects that consistently span over a large portion of the frame might not be recognized.
- Small or blurry objects can be hard to detect. They can either be missed or misclassified (wine glass, cup).
- Objects that are transient and appear in few frames might not be recognized.
- Other factors that might affect the accuracy of the object detection include low light conditions, camera motion, and occlusions.
- Azure AI Video Indexer supports only real world objects. There's no support for animation or CGI. Computer generated graphics (such as news-stickers) might produce strange results.
- Binders, brochures, and other written materials tend to be detected as `Book`.

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

