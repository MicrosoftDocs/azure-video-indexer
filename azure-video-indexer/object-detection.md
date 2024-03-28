---
title: Azure AI Video Indexer object detection overview
description: An introduction to Azure AI Video Indexer object detection overview.
ms.date: 03/27/2024
ms.topic: article
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Azure AI Video Indexer object detection

Azure AI Video Indexer can detect objects in videos. The insight is part of standard and advanced video presets.

## Prerequisites

Review [transparency note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context)

## JSON keys and definitions

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

## JSON response

Object detection is included in the insights that are the result of an [Upload](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video) request. 

### Detected and tracked objects

Detected and tracked objects appear under “detected Objects” in the downloaded *insights.json* file. Every time a unique object is detected, it's given an ID. That object is also tracked, meaning that the model watches for the detected object to return to the frame.  If it does, another instance is added to the instances for the object with different start and end times.

In this example, the first car was detected and given an ID of 1 since it was also the first object detected. Then, a different car was detected and that car was given the ID of 23 since it was the 23rd object detected. Later, the first car appeared again and another instance was added to the JSON. Here is the resulting JSON:

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

## Try object detection

You can try out object detection with the web portal or with the API.

## [Web Portal](#tab/webportal)

Once you have uploaded a video, you can view the insights. On the insights tab, you can view the list of objects detected and their main instances.

### Insights
Select the **Insights** tab. The objects are in descending order of the number of appearances in the video.

:::image type="content" source="media/object-detection/insights-tab.png" alt-text="screenshot of the interface of the insights tab":::

### Timeline
Select the **Timeline** tab.

:::image type="content" source="media/object-detection/timeline-tab.png" alt-text="screenshot of the interface of the timeline tab":::

Under the timeline tab, all object detection is displayed according to the time of appearance. When you hover over a specific detection, it shows the detection percentage of certainty. 

### Player

The player automatically marks the detected object with a bounding box. The selected object from the insights pane is highlighted in blue with the objects type and serial number also displayed.
 
Filter the bounding boxes around objects by selecting bounding box icon on the player.

:::image type="content" source="media/object-detection/object-filtering-icon.png" alt-text="screenshot of object filtering icon player interface":::

Then, select or deselect the detected objects checkboxes.

:::image type="content" source="media/object-detection/object-filtering.png" alt-text="screenshot of object filtering detected objects in the player interface":::

Download the insights by selecting **Download** and then **Insights (JSON)**.

## [API](#tab/api)

When you use the [Upload](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video) request with the standard or advanced video presets, object detection is included in the indexing.

To examine object detection more thoroughly, use [Get Video Index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Index).

---

## Supported objects

:::row:::
    :::column:::
        - airplane
        - apple
        - backpack
        - banana
        - baseball bat
        - baseball glove
        - bed
        - bicycle
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
        - kite
        - knife
        - laptop
        - microwave
        - motorcycle
        - mouse (a computer mouse not the animal)
        - necktie
        - orange
        - oven
        - parking meter
        - pizza
        - potted plant
    :::column-end:::
    :::column:::
        - refrigerator
        - remote
        - sandwich
        - scissors
        - skateboard
        - skis
        - snowboard
        - spoon
        - sports ball
        - suitcase
        - surfboard
        - teddy bear
        - television
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
        - weapon, see [Specific class notes for the weapon class](#specific-class-notes)
        - wine glass
    :::column-end:::
:::row-end:::

## Limitations

- There are up to 20 detections per frame for standard and advanced processing and 35 tracks per class.
- Object size shouldn't be greater than 90 percent of the frame. Very large objects that consistently span over a large portion of the frame might not be recognized.
- Small or blurry objects can be hard to detect. The can either be missed or misclassified (wine glass, cup).
- Objects that are transient and appear in very few frames may ot be recognized.
- Other factors that may affect the accuracy of the object detection include low light conditions, camera motion, and occlusion.
- Video AI Indexer supports only real world objects. There is no support for animation or CGI. Computer generated graphics (such as news-stickers) may produce strange results.
- See [specific class notes](#specific-class-notes).

## Specific class notes

### Bound written materials

Binders, brochures, and other written materials tend to be detected as "book".

### Weapon

- The weapon class includes appearances of hand gun and rifles.
- Hands holding dark objects (mostly, but not limited to blurry objects) may be confused with weapons.
- Weapons over a very dark background can be missed.
- Low quality videos (resolution, compression, etc) may affect the ability of the model to identify the weapon.
- Mechanical objects (including robots) and complicated machinery may sometimes be detected as weapons.
