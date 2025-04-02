---
title: Azure AI Video Indexer Bring Your Own AI model overview  
description: This article is an overview of Azure AI Video Indexer enabled by Arc bring your own model.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/09/2024
ms.service: azure-video-indexer
ms.topic: overview
---

# Azure AI Video Indexer Bring Your Own (BYO) AI Model overview

This article is an overview of Azure AI Video Indexer bring your own AI model.

## Introduction

You can combine insights from other sources, including third-party, classification and detection models, to produce a detailed analysis of your media data. You can use one or more of any models offered by Microsoft, an external custom model, or a customized Person, Brand, Speech, or Language model offered by Azure Video Indexer.

The feature is also available for [VI enabled by Arc](./arc/azure-video-indexer-enabled-by-arc-overview.md).

DISCLAIMER: Microsoft’s [Code of conduct for Azure OpenAI Service](/legal/cognitive-services/openai/code-of-conduct?context=%2Fazure%2Fai-services%2Fopenai%2Fcontext%2Fcontext) applies to your use of the Bring Your Own Model feature, which includes Microsoft’s right to discontinue your access and use of this feature for noncompliance.

## Pricing
With the Video Indexer BYO model, users can add custom insights to video insight objects without incurring any additional costs beyond the listed cost of the indexing process. However, any costs related to the external environment and model shouldn't be considered part of Video Indexer's billing price. We strongly recommend reviewing our best practices section to optimize the external logic and reduce costs.

### General workflow

1. Video is uploaded and indexed with Azure AI Video Indexer.  
1. When the indexing process is completed, an event is created.  
1. Your custom code listens to the event and starts the video post-processing process.
    1. Get insights extracted by Video Indexer.
    1. Get keyframe for a video section.
    1. Send the keyframe to the custom AI model. 
    1. Patch the custom insights back to Video Indexer.

:::image type="content" source="media/common/general-byo-workflow.svg" lightbox="media/common/general-byo-workflow.svg" alt-text="diagram of the workflow described above"::: 

## Prerequisites

Before you can start using the BYO model feature with Azure AI Video Indexer, you must: 

1. Train or bring an external AI model that receives video assets and return an insight.   
1. Create custom code that:
    1. Listens for Event Hubss events. 
    1. Extracts the `video id` from the events. 
    1. Retrieves the relevant assets by calling VI APIs. In this scenario, request *Get Video Index* and *Get frames SAS URLs*.
    1. Sends the assets to the external AI model. 
    1. Creates a JSON object based on the insights retrieved from the custom AI model.  
    1. Requests *Patch Update Video Index*.

## Schema

The values for populating the custom data are as follows:

| Name | **Description** | **Required** |
|--|--|--|
| **name** | External AI model name | true |
| **displayName** | Insight group name to be displayed in Video Indexer | true |
| **displayType** | Defines the type of UI representation for this specific insight group. **Default value**: Capsules<br/>**Possible types**:<br/>*Capsule* – One level text only <br/>*CapsuleAndTags* -Two levels text only more will be added in the future.  | false |
| **results** | Array of objects that represent the insights detected by the external AI model | true |
| **results.id** | User provided ID of the result object, should be unique within the results scope | true |
| **results.type** | This field represents the type of insight that was categorized by the external AI model.  It's used to represent a general insight category, which means that there could be multiple insights of this type identified in a specific frame. Examples of insight types include: "basketball", "crowd clapping", "white shirt". | true |
| **results.subType** | This field represents the type of insight that was categorized by the external AI model. It's used to represent a specific insight category, which means that there could be only a single insight of this type identified in a specific frame. Examples of insight types include: "basketball \#23", "John clapping", "Dana’s white shirt". | false |
| **results.metaData** | More data on the insight | false |
| **results.instances** | Array that represents the time windows the insight was detected in. | true |
| **results.instances.confidence** | Set with the confidence score returned from the external model | false |
| **results.instances.start** | Start time of the instance in the video. Format: `hh.mm.ss.ff` | false |
| **results.instances.end** | End time of the instance in the video. Format: `hh.mm.ss.ff`  | false |
| **results.instances.adjustedStart** | Used when displayed in the UI, set with the value from Start | false |
| **results.instances.adjustedEnd** | Used when displayed in the UI, set with the value from End | false |
 
## Framerate

Azure AI Video Indexer supports one FPS for the Basic/Standard video level and four FPS for the advanced level. Higher frame rates aren't supported. You can optimize indexing by:

- Processing only specific segments that are of interest such as frames that include a detected sound, object or person, or 
- sample a lower FPS, for example,  every 5 seconds. 

## Frame selection

You can use the skip frames and page size parameters for time selection. The formula is the skip frames value multiplied by the FPS plus the page size value multiplied by the FPS can be used to determine the time range.

**URL:** `https://api.videoindexer.ai/{location}/Accounts/{accountId}/Videos/{videoId}/FramesFilePaths[?urlsLifetimeSeconds][&pageSize][&skip][&accessToken]`

**Parameters:**

| Name | **Description** | **Required** |
|--|--|--|
| **videoId** | ID of the video | true |
| **urlsLifetimeSeconds** | lifetime of the urls in seconds | true |
| **pageSize** | Max number of frames to return every call | false |
| **skip** | Frames to skip | false |
| **accessToken** | Should be given as parameter in URL query string or in Authorization header as Bearer token. Access token scope should be Account and permission should be Reader. | true |

**Response:** `FrameFilePathsResult`

| Name          | **Description**                       | **Required**  |
|---------------|---------------------------------------|---------------|
| **results**   | List of FrameUriData                  | False         |
| **NextPage**  | Paging data (skip, pageSize, isDone)  | False         |

**FrameFilePathData**

| Name            | **Description**                       |
|-----------------|---------------------------------------|
| **name**        | Name of the frame file                |
| **frameIndex**  | Index of the frame                    |
| **StartTime**   | Start time of the frame in the video  |
| **EndTime**     | End time of the frame in the video    |
| **filePath**    | Sas URI of the frame in the cloud environment or file path in edge environments |

### Sample data sent from custom application in schema format
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

## Bring Your Own model samples
[BYO samples](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/BringYourOwn-Samples)

## Related content
[Use the Azure AI Video Indexer API](/azure/azure-video-indexer/video-indexer-use-apis)
