## Object detection

[!INCLUDE [object detection description](object-detection-description.md)]

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

[!INCLUDE [get insights with the web portal](get-insights-web-portal.md)]

[!INCLUDE [get insights with the API](get-insights-api.md)]

## Example response 

Detected and tracked objects appear under "detected Objects" in the downloaded *insights.json* file. Every time a unique object is detected, the object is given an ID. That object is also tracked, meaning that the model watches for the detected object to return to the frame. If it does, another instance is added to the instances for the object with different start and end times.

In this example, the first car was detected and given an ID of 1 since it was also the first object detected. Then, a different car was detected and that car was given the ID of 23 since it was the 23rd object detected. Later, the first car appeared again and another instance was added to the JSON. Here's the resulting JSON:

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

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

- There are up to 20 detections per frame for standard and advanced processing and 35 tracks per class.
- Object size shouldn't be greater than 90 percent of the frame. Large objects that consistently span over a large portion of the frame might not be recognized.
- Small or blurry objects can be hard to detect. They can either be missed or misclassified (wine glass, cup).
- Objects that are transient and appear in few frames might not be recognized.
- Other factors that might affect the accuracy of the object detection include low light conditions, camera motion, and occlusions.
- Azure AI Video Indexer supports only real world objects. There's no support for animation or CGI. Computer generated graphics (such as news-stickers) might produce strange results.
- Binders, brochures, and other written materials tend to be detected as "book."

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)
