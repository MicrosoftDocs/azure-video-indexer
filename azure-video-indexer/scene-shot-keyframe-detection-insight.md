---
title: Get scene, shot, and keyframe detection insights in Azure AI Video Indexer
description: Get scene, shot, and keyframe detection insights with Azure AI Video Indexer. Improve your video editing and management with automated visual analysis.
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
appliesto:
  - Azure AI Video Indexer enabled by Azure Arc
  - Cloud-based Azure AI Video Indexer
#customer intent: As a video content creator, I want to understand how Azure AI Video Indexer detects scenes, shots, and keyframes so that I can better manage and edit my videos.
---

# Get scene, shot, and keyframe detection insights

Scene detection finds when a scene changes in a video based on visual cues. A **scene** shows a single event and has a series of related shots. **Shots** are a series of frames that differ by visual cues, like abrupt or gradual changes in the color scheme of adjacent frames. Shot metadata includes the start time, end time, and a list of keyframes in the shot. A **keyframe** is a frame from a shot that best represents the shot.

## Scene, shot, and keyframe detection use cases

- Easily browse, manage, and edit your video content based on varying granularities.
- Use editorial shot type detection for editing videos into clips, trailers, or when searching for a specific style of keyframe.

## Scene detection

Azure AI Video Indexer determines when a scene changes in video based on visual cues. A scene depicts a single event composed of a series of consecutive shots, which are semantically related. 

A scene thumbnail is the first keyframe of its underlying shot. 

Azure AI Video Indexer segments a video into scenes based on color coherence across consecutive shots and retrieves the beginning and end time of each scene.

Videos must contain at least three scenes.

## Shot detection

Azure AI Video Indexer determines when a shot changes in the video based on visual cues. It does so by detecting both abrupt and gradual transitions in the color scheme and other visual feature of adjacent frames. The shot's metadata includes a start and end time, and the list of keyframes included in that shot. The shots are consecutive frames taken from the same camera at the same time.

> [!NOTE]
> There might be a gap between shots which includes frames that are part of the transition. Therefore, these frames aren't considered part of the shot.

## Keyframe editorial shot type detection

The shot type is determined based on analysis of the first keyframe of each shot. Shots get identified by the scale, size, and location of the faces appearing in their first keyframe.

The shot size and scale are determined based on the distance between the camera and the faces appearing in the frame. Azure AI Video Indexer detects the following shot types using these properties:

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

Other characteristics:

- Two shots: shows two persons’ faces of medium size.
- Multiple faces: more than two persons.

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

To download each keyframe, use the keyframe IDs with a [Get Thumbnails](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Thumbnail) API request.

> [!WARNING]
> Don't use data directly from the artifacts folder for production purposes. Artifacts are intermediate outputs of the indexing process and are raw outputs of different AI engines that analyze videos. The artifacts schema might change over time.

<!-- The warning text is duplicated in faq.yml. Sync any changes  -->

> [!IMPORTANT]
> Read the [transparency note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context) for VI features.

<!-- 8/8/24 Removed from transparency note because not released due to a bug. -->

## Scene, shot, and keyframe detection notes

- The detector works best on media files that have shots and scenes within them.  
- If the video is filmed with one camera that never moves, the shot segmentation works poorly, and the keyframes might not be representative. 
- Keyframes are selected by taking into account the blurriness level of the frames. If most of the shot is blurry, for example with motion, the keyframe might also be blurry. 
- Videos with poor visual quality produce poor results. 
- The time of each shot/scene/keyframe might shift (less than a second).

## Scene, shot, and keyframe components

No components defined.

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

## Related content

- [Azure AI Video Indexer documentation](index.yml)