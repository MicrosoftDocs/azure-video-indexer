---
title: Azure AI Video Indexer Bring Your Own AI model overview  
description: This article is an overview of Azure AI Video Indexer enabled by Arc bring your own model.
ms.topic: quickstart
ms.service: azure-video-indexer
ms.date: 11/10/2023
ms.author: inhenkel
author: IngridAtMicrosoft
---

# Azure Video Indexer Bring Your Own (BYO) AI model overview

This article is an overview of Azure Video Indexer bring your own AI model.

## Introduction

Azure Video Indexer offers a set of AIs optimized for video and audio content that can be applied to many content types. You can combine more insights from Microsoft sources, custom sources, or third party sources with the built-in Azure Video Indexer insights all in a seamless experience.

This feature is flexible enough to accommodate all forms and types of insights, including detection-oriented and classification-oriented AIs. You have the freedom to select the data that your external model operates upon, such as the video's key frames, the entire video, or just the audio track. You can also use other insights already produced for the video, such as detected objects, faces, and labels. This allows you to run the external analysis on only the related section of the video, improving performance and reducing costs.

The feature is available for both the cloud and edge use cases.

## Pricing
There's no extra cost to use this feature with Azure Video Indexer.

## Workflow

**Workflow diagram from Shemer's PPT goes here**

### General workflow
1. Use the Azure Video Indexer workflow as usual, but add a callback URL to your own custom programming expecting the request.
1. The request returns a JSON file with custom insights.
1. The custom programming calls the Patch method in the Azure Video Indexer API.
1. The Patch method adds the JSON data under the `customInsights` section of the Azure Video Indexer insights JSON.  

## Prerequisites

Before you can start using the BYO model feature with Azure Video Indexer, you must:

1. Create the programming that returns information in the required JSON format, and calls the Patch method.
1. Provide the callback URL for requesting the JSON.
1. Plan to pass a media ID so that the GUIDs map appropriately.

### Test a workflow using Azure services
1. Set up monitoring on your Azure Video Indexer account using Azure Event Hub and a diagnostic setting.
1. Set up the Azure Event so that it triggers an Azure Function that:
    1. Receives the indexing information including the media ID.
    1. Sends a GET request to the Update Video Index with test information formatted with the schema.
1. See the results in the Azure Video Indexer portal.

## Schema

The values for populating the custom data are as follows:

| Name | **Description** | **Required** |
|--|--|--|
| **name** | External AI model name | true |
| **displayName** | Insight group name to be displayed in Video Indexer | true |
| **displayType** | Defines the type of UI representation for this specific insight group. Possible types:  Capsule – One level text only CapsuleAndTags -Two levels text only more will be added in the future. Default value: Capsules | false |
| **results** | Array of objects that represent the insights detected by the external AI model | true |
| **results.id** | User provided ID of the result object, should be unique within the results scope | false |
| **results.wikiDataId** | Should be given as parameter in URL query string or in Authorization header as Bearer token. Access token scope should be Account and permission should be Reader. | false |
| **results.type** | This field represents the type of insight that was categorized by the external AI model.  It is used to represent a general insight category, which means that there could be multiple insights of this type identified in a specific frame. Examples of insight types include: "basketball", "crowd clapping", "white shirt". | true |
| **results.subType** | This field represents the type of insight that was categorized by the external AI model. It is used to represent a specific insight category, which means that there could be only a single insight of this type identified in a specific frame. Examples of insight types include: "basketball \#23", "John clapping", "Dana’s white shirt". | false |
| **results.metaData** | More data on the insight | false |
| **results.thumbnailId** | User provided GUID that refers to the name of the thumbnail image file the image file provided by the user using the upload thumbprints API (P1) | false |
| **results.instances** | Array that represents the time windows the insight was detected in. | true |
|  |  |  |
| **results.instances.confidence** | Confidence of the | false |
| **results.instances.adjustedStart** | Frames to skip | false |
| **results.instances.adjustedEnd** | Frames to skip | false |
| **results.instances.start** | Frames to skip | false |
| **results.instances.end** | Frames to skip | false |

## GUIDs
You're responsible for making certain that the GUIDs for the media segments map to the Azure Video Indexer insights for the same media.
 
## Framerate

Azure Video Indexer supports 1 FPS for the Basic/Standard video level and 4 FPS for the advanced level. Higher frame rates aren't supported. You can optimize indexing by:

- Processing only specific segments that are of interest such as frames that include a detected sound, object or person, or 
- sample a lower FPS, for example,  every 5 seconds. 

## Frame selection

You can use the skip frames and page size parameters for time selection. The formula is the skip frames value multiplied by the FPS plus the page size value multiplied by the FPS can be used to determine the time range.

**URL:** `api/v2/Accounts/{accountId}/Videos/{videoId}/FramesSasUrls[?urlsLifetimeSeconds][&pageSize][&skip][&accessToken]`

**Parameters:**

| Name | **Description** | **Required** |
|--|--|--|
| **videoId** | ID of the video | true |
| **urlsLifetimeSeconds** | lifetime of the urls in seconds | true |
| **pageSize** | Max number of frames to return every call | false |
| **skip** | Frames to skip | false |
| **accessToken** | Should be given as parameter in URL query string or in Authorization header as Bearer token. Access token scope should be Account and permission should be Reader. | true |

**Response:** `FrameUrisResult`

| Name          | **Description**                       | **Required**  |
|---------------|---------------------------------------|---------------|
| **results**   | List of FrameUriData                  | False         |
| **NextPage**  | Paging data (skip, pageSize, isDone)  | False         |

FrameUriData

| Name            | **Description**                       |
|-----------------|---------------------------------------|
| **name**        | Name of the frame file                |
| **frameIndex**  | Index of the frame                    |
| **StartTime**   | Start time of the frame in the video  |
| **EndTime**     | End time of the frame in the video    |
| **SasUri**      | Sas uri of the frame                  |

### Sample schema
```json
"customInsights": [
    {
        "Name": "tattoo",  
        "displayName": "Tattoo’s model",
        "displayType": "CapsuleAndTag",
        "Results": [   
            {   
                "id": 1,   
                "Type": "Dragon",   
                "WikiDataId": "57F",   
                "SubType": "Leg tattoo",   
                "Metadata": "",   
                "Instances": [
                    {
                        "Confidence": 0.49,
                        "AdjustedStart": "0:00:32.72", 
                        "AdjustedEnd": "0:00:42.72",
                        "start": "0:00:32.72",
                        "end": "0:00:42.72",
                    }
                ]
            }
        ]
    }... 
```

**----------Is this section needed for Ignite?---------**
## Thumbnail cropping
I can't tell from the spec doc what is supposed to go in here.
**---------end this section----------**

**----------Is this section needed for Ignite?---------**
## Search
I can't tell from the spec doc what is supposed to go in here.
**---------end this section----------**
