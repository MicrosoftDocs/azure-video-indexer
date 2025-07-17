---
title: Get face detection insights
description: This article shows you how to get the Azure AI Video Indexer face detection insights.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/04/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
---

# Get face detection insights

This article shows you how to get Azure AI Video Indexer face detection insights. Face detection finds faces in a media file and groups similar faces. The system generates face detection insights as a categorized list in a JSON file. Each entry includes a thumbnail and either a name or an ID for each face. In the web portal, when you select a face’s thumbnail, you see details like the person’s name (if recognized), the percentage of the video where the person appears, and the person's biography if they're a celebrity. You can scroll through instances in the video where the person appears.

## Celebrities recognition model

The celebrities recognition model covers approximately 1 million faces and is based on commonly requested data sources. Faces that Video Indexer doesn't recognize as celebrities are detected but left unnamed. You can build your own custom [person model](/azure/azure-video-indexer/customize-person-model-overview) to train Video Indexer to recognize faces that aren't recognized by default.

> [!IMPORTANT]
> To support Microsoft Responsible AI principles, access to face identification, customization, and celebrity recognition features are limited and based on eligibility and usage criteria. Face identification, customization, and celebrity recognition features are available to Microsoft managed customers and partners. To apply for access, use the [facial recognition intake form](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUQjA5SkYzNDM4TkcwQzNEOE1NVEdKUUlRRCQlQCN0PWcu).

## Face detection use cases

The following list describes examples of common use cases for face detection:

- Summarize where an actor appears in a movie or reuse footage by deep searching specific faces in organizational archives for insight about a specific celebrity.
- Get improved efficiency when you create feature stories at a news agency or sports agency. Examples include deep searching a celebrity or a football player in organizational archives.
- You can use faces that appear in a video to create promos, trailers, or highlights. Video Indexer can assist by adding keyframes, scene markers, time stamps, and labeling so that content editors invest less time reviewing numerous files.

## Key terms  

| Term | Definition |
|---|---|
| **Face recognition**  | Analyzing images to identify the faces that appear in the images. This process is implemented via the Azure AI Face API. |
| **Enrollment** | The process of enrolling images of individuals for template creation so that they can be recognized. When a person is enrolled to a verification system that's used for authentication, their template is also associated with a primary identifier. The identifier is used to determine which template to compare against the probe template. High-quality images and images that represent natural variations in how a person looks (for instance, wearing glasses and not wearing glasses) generate high-quality enrollment templates. |
| **Template** | Enrolled images of people are converted to templates, which are then used for facial recognition. Machine-interpretable features are extracted from one or more images of an individual to create that individual’s template. The Face API doesn't store the enrollment or probe images. The original images can't be reconstructed based on a template. Template quality is a key determinant for accuracy in your results. |

## View the insight JSON with the web portal

After you upload and index a video, download insights in JSON format from the web portal.

1. Select the **Library** tab.
1. Select the media you want.
1. Select **Download**, and then select **Insights (JSON)**. The JSON file opens in a new browser tab.
1. Find the key pair described in the example response.

## Use the API

1. Use a [Get Video Index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Index) request. Pass `&includeSummarizedInsights=false`.
2. Find the key pairs described in the example response.

> [!IMPORTANT]
> When you review face detections in the UI, you might not see all faces that appear in the video. We expose only face groups that have a confidence of more than 0.5, and the face must appear for a minimum of 4 seconds or 10 percent of the value of `video_duration`. Only when these conditions are met do we show the face in the UI and in the *Insights.json* file. You can always retrieve all face instances from the face artifact file by using the API: `https://api.videoindexer.ai/{location}/Accounts/{accountId}/Videos/{videoId}/ArtifactUrl[?Faces][&accessToken]`.

## Example response

```json
    "faces": [
        {
        "id": 1785,
        "name": "Emily Tran",
        "confidence": 0.7855,
        "description": null,
        "thumbnailId": "fd2720f7-b029-4e01-af44-3baf4720c531",
        "knownPersonId": "92b25b4c-944f-4063-8ad4-f73492e42e6f",
        "title": null,
        "imageUrl": null,
        "thumbnails": [
            {
            "id": "4d182b8c-2adf-48a2-a352-785e9fcd1fcf",
            "fileName": "FaceInstanceThumbnail_4d182b8c-2adf-48a2-a352-785e9fcd1fcf.jpg",
            "instances": [
                {
                "adjustedStart": "0:00:00",
                "adjustedEnd": "0:00:00.033",
                "start": "0:00:00",
                "end": "0:00:00.033"
                }
            ]
            },
            {
            "id": "feff177b-dabf-4f03-acaf-3e5052c8be57",
            "fileName": "FaceInstanceThumbnail_feff177b-dabf-4f03-acaf-3e5052c8be57.jpg",
            "instances": [
                {
                "adjustedStart": "0:00:05",
                "adjustedEnd": "0:00:05.033",
                "start": "0:00:05",
                "end": "0:00:05.033"
                }
            ]
            },
        ]
        }
    ]
```

> [!IMPORTANT]
> Read the [transparency note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context) for all VI features. Each insight also has its own transparency note.

[!INCLUDE [transparency-named-entities](./includes/transparency-face-detection.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

