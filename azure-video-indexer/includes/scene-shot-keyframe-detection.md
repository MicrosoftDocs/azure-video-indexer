---
title: Text-based emotion detection
ms.service: azure-video-indexer
ms.topic: include
ms.date: 08/22/2024
ms.author: inhenkel
---

## Scene, shot, keyframe detection

[!INCLUDE [Scene, shot, keyframe detection description](scene-shot-keyframe-detection-description.md)]

### Scene, shot and keyframe detection use cases

- Easily browse, manage, and edit your video content based on varying granularities.
- Use editorial shot type detection for editing videos into clips, trailers, or when searching for a specific style of keyframe.

## Scene detection

Azure AI Video Indexer determines when a scene changes in video based on visual cues. A scene depicts a single event and it is composed of a series of consecutive shots, which are semantically related. 

A scene thumbnail is the first keyframe of its underlying shot. 

Azure AI Video Indexer segments a video into scenes based on color coherence across consecutive shots and retrieves the beginning and end time of each scene.

Videos must contain at least three scenes.

## Shot detection

Azure AI Video Indexer determines when a shot changes in the video based on visual cues, by detecting both abrupt and gradual transitions in the color scheme of adjacent frames. The shot's metadata includes a start and end time, as well as the list of keyframes included in that shot. The shots are consecutive frames taken from the same camera at the same time.

## Keyframe editorial shot type detection

The shot type is determined based on analysis of the first keyframe of each shot. Shots are identified by the scale, size, and location of the faces appearing in their first keyframe.

The shot size and scale are determined based on the distance between the camera and the faces appearing in the frame. Using these properties, Azure AI Video Indexer detects the following shot types:

- Wide: shows an entire person’s body.
- Medium: shows a person's upper-body and face.
- Close up: mainly shows a person’s face.
- Extreme close-up: shows a person’s face filling the screen.

Shot types can also be determined by location of the subject characters with respect to the center of the frame. This property defines the following shot types in Azure AI Video Indexer:

- Left face: a person appears in the left side of the frame.
- Center face: a person appears in the central region of the frame.
- Right face: a person appears in the right side of the frame.
- Outdoor: a person appears in an outdoor setting.
- Indoor: a person appears in an indoor setting.

Additional characteristics:

- Two shots: shows two persons’ faces of medium size.
- Multiple faces: more than two persons.

[!INCLUDE [get insights with the web portal](get-insights-web-portal.md)]

[!INCLUDE [get insights with the API](get-insights-api.md)]

## Example response

```json
"scenes": [
                    {
                        "id": 1,
                        "instances": [
                            {
                                "adjustedStart": "0:00:00",
                                "adjustedEnd": "0:00:09.1333333",
                                "start": "0:00:00",
                                "end": "0:00:09.1333333"
                            }
                        ]
                    },
                    {
                        "id": 2,
                        "instances": [
                            {
                                "adjustedStart": "0:00:09.1333333",
                                "adjustedEnd": "0:00:10.8",
                                "start": "0:00:09.1333333",
                                "end": "0:00:10.8"
                            }
                        ]
                    },
                    {
                        "id": 3,
                        "instances": [
                            {
                                "adjustedStart": "0:00:10.8",
                                "adjustedEnd": "0:00:26.9333333",
                                "start": "0:00:10.8",
                                "end": "0:00:26.9333333"
                            }
                        ]
                    }...
                    {
                        "id": 31,
                        "instances": [
                            {
                                "adjustedStart": "0:18:45",
                                "adjustedEnd": "0:18:50.2",
                                "start": "0:18:45",
                                "end": "0:18:50.2"
                            }
                        ]
                    }
                ],
                "shots": [
                    {
                        "id": 1,
                        "tags": [
                            "Wide",
                            "Medium"
                        ],
                        "keyFrames": [
                            {
                                "id": 1,
                                "instances": [
                                    {
                                        "thumbnailId": "60152925-0e6d-48cf-be33-aa6c00dfb334",
                                        "adjustedStart": "0:00:00.1666667",
                                        "adjustedEnd": "0:00:00.2",
                                        "start": "0:00:00.1666667",
                                        "end": "0:00:00.2"
                                    }
                                ]
                            },
                            {
                                "id": 2,
                                "instances": [
                                    {
                                        "thumbnailId": "f1a09cdf-b42b-45f5-bc69-5292d1216e50",
                                        "adjustedStart": "0:00:00.2333333",
                                        "adjustedEnd": "0:00:00.2666667",
                                        "start": "0:00:00.2333333",
                                        "end": "0:00:00.2666667"
                                    }
                                ]
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:00:00",
                                "adjustedEnd": "0:00:01.9333333",
                                "start": "0:00:00",
                                "end": "0:00:01.9333333"
                            }
                        ]
                    },
                    {
                        "id": 2,
                        "tags": [
                            "Medium"
                        ],
                        "keyFrames": [
                            {
                                "id": 3,
                                "instances": [
                                    {
                                        "thumbnailId": "b17774d0-41cf-4174-9c41-6bc2f17c86e2",
                                        "adjustedStart": "0:00:02",
                                        "adjustedEnd": "0:00:02.0333333",
                                        "start": "0:00:02",
                                        "end": "0:00:02.0333333"
                                    }
                                ]
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:00:01.9333333",
                                "adjustedEnd": "0:00:02.9666667",
                                "start": "0:00:01.9333333",
                                "end": "0:00:02.9666667"
                            }
                        ]
                    }...
```

## Download the keyframes with the API

To download each keyframe, use the keyframe IDs with the [Get Thumbnails](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Thumbnail) request.

[!INCLUDE [artifacts](artifacts.md)]

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

[!INCLUDE [transparency-scene-shot-keyframe-detection](transparency-scene-shot-keyframe-detection.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)
