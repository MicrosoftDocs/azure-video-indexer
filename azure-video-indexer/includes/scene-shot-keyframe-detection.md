---
title: Text-based emotion detection
ms.service: azure-video-indexer
ms.topic: include
ms.date: 07/25/2024
ms.author: inhenkel
---

## Scene, shot, keyframe detection

[!INCLUDE [Scene, shot, keyframe detection description](scene-shot-keyframe-detection-description.md)]

### Scene, shot and keyframe detection use cases

[!INCLUDE [get insights with the web portal](get-insights-web-portal.md)]

[!INCLUDE [get insights with the API](get-insights-api.md)]

## Example response 

```json
"shots":[  
    {  
      "id":0,
      "keyFrames":[  
          {  
            "id":0,
            "instances":[  
                {  
                  "thumbnailId":"00000000-0000-0000-0000-000000000000",
                  "start":"0:00:00.209",
                  "end":"0:00:00.251",
                  "duration":"0:00:00.042"
                }
            ]
          },
          {  
            "id":1,
            "instances":[  
                {  
                  "thumbnailId":"00000000-0000-0000-0000-000000000000",
                  "start":"0:00:04.755",
                  "end":"0:00:04.797",
                  "duration":"0:00:00.042"
                }
            ]
          }
      ],
      "instances":[  
          {  
            "start":"0:00:00",
            "end":"0:00:06.34",
            "duration":"0:00:06.34"
          }
      ]
    },

]

```

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

[!INCLUDE [transparency-scene-shot-keyframe-detection](transparency-scene-shot-keyframe-detection.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)
