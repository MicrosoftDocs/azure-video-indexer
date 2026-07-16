---
title: Azure AI Video Indexer Bring Your Own AI model overview
description: This article is an overview of Azure AI Video Indexer enabled by Arc bring your own model.
author: cwatson-cat
ms.author: cwatson
ms.date: 07/14/2026
ms.service: azure-video-indexer
ms.topic: overview
appliesto:
  - Cloud-based Azure AI Video Indexer
ai-usage: ai-assisted
#customer intent: As a developer, I want to understand how to extend Azure AI Video Indexer with custom AI models so that I can add specialized insights to my video analysis.
---

# Azure AI Video Indexer Bring Your Own (BYO) AI Model overview

Combine insights from other sources, including third-party, classification, and detection models, to produce a detailed analysis of your media data. You can use one or more of any models offered by Microsoft, an external custom model, or a customized Person, Brand, Speech, or Language model offered by Azure Video Indexer.

The feature is also available with [Azure AI Video Indexer enabled by Arc](./arc/azure-video-indexer-enabled-by-arc-overview.md).

> [!NOTE]
> DISCLAIMER: Microsoft's [Code of conduct for Azure OpenAI Service](/legal/cognitive-services/openai/code-of-conduct?context=%2Fazure%2Fai-services%2Fopenai%2Fcontext%2Fcontext) applies to your use of the Bring Your Own Model feature, which includes Microsoft's right to discontinue your access and use of this feature for noncompliance.

## Pricing

With the Video Indexer BYO model, you can add custom insights to video insight objects without incurring any extra costs beyond the listed cost of the indexing process. However, any costs related to the external environment and model shouldn't be considered part of Video Indexer's billing price. We strongly recommend reviewing our best practices section to optimize the external logic and reduce costs.

### General workflow

1. Video is uploaded and indexed with Azure AI Video Indexer.  
1. When the indexing process is completed, an event is created.  
1. Your custom code listens to the event and starts the video post-processing process.
    1. Retrieve insights extracted by Azure AI Video Indexer.
    1. Get keyframes for a video section.
    1. Send the keyframe to the custom AI model. 
    1. Patch the custom insights back to Video Indexer.

:::image type="complex" source="./media/common/general-byo-workflow.svg" border="true" alt-text="Diagram showing the general bring your own model workflow process." lightbox="./media/common/general-byo-workflow.svg":::
Diagram of the bring your own model workflow showing the following process: A video is uploaded and indexed with Azure AI Video Indexer. When indexing completes, an event is created. Custom code listens to this event and starts post-processing. The custom code retrieves Video Indexer insights and keyframes by calling APIs. The keyframes are sent to the custom AI model for processing. The custom model returns insights, which the custom code patches back into Video Indexer by using the Patch Update Video Index API.
:::image-end:::

## Prerequisites

Before you can start using the BYO model feature with Azure AI Video Indexer, you must: 

1. Train or bring an external AI model that receives video assets and returns insights.   
1. Create custom code that:
    1. Listens for Event Hubs events. 
    1. Extracts the `video id` from the events. 
    1. Retrieves the relevant assets by calling Azure AI Video Indexer APIs. In this scenario, request *Get Video Index* and *Get frames SAS URLs*.
    1. Sends the assets to the external AI model. 
    1. Creates a JSON object based on the insights retrieved from the custom AI model.  
    1. Requests *Patch Update Video Index*.

## Schema

The values for populating the custom data are as follows:

| Name | **Description** | **Required** |
|--|--|--|
| **name** | External AI model name | true |
| **displayName** | Insight group name to be displayed in Video Indexer | true |
| **displayType** | Defines the type of UI representation for this specific insight group. **Default value**: Capsules<br/>**Possible types**:<br/>*Capsule* – One level text only <br/>*CapsuleAndTags* -Two levels text only more will be added in the future. | false |
| **results** | Array of objects that represent the insights detected by the external AI model | true |
| **results.id** | User provided ID of the result object, should be unique within the results scope | true |
| **results.type** | Type of insight that the external AI model categorized. Use this field to represent a general insight category, which means there can be multiple insights of this type identified in a specific frame. Examples of insight types include: `basketball`, `crowd clapping`, `white shirt`. | true |
| **results.subType** | Specific insight type that the external AI model categorized. Use this field to represent a specific insight category, which means there can be only a single insight of this type identified in a specific frame. Examples of insight types include: `basketball #23`, `John clapping`, `Dana's white shirt`. | false |
| **results.metaData** | More data on the insight | false |
| **results.instances** | An array that represents the time windows where the insight appears. | true |
| **results.instances.confidence** | Set with the confidence score returned from the external model | false |
| **results.instances.start** | Start time of the instance in the video. Format: `hh.mm.ss.ff` | false |
| **results.instances.end** | End time of the instance in the video. Format: `hh.mm.ss.ff`  | false |
| **results.instances.adjustedStart** | Displayed in the UI, set with the value from Start. | false |
| **results.instances.adjustedEnd** | Displayed in the UI, set with the value from End. | false |
 
## Framerate

Azure AI Video Indexer supports one FPS for the Basic/Standard video level and four FPS for the advanced level. Higher frame rates aren't supported. You can optimize indexing by:

- Process only specific segments that interest you, such as frames that include a detected sound, object, or person.
- Sample a lower FPS, for example, every 5 seconds.

## Frame selection

Use the skip frames and page size parameters for time selection. Multiply the skip frames value by the FPS, then add the page size value multiplied by the FPS to determine the time range.

**URL:** `https://api.videoindexer.ai/{location}/Accounts/{accountId}/Videos/{videoId}/FramesFilePaths[?urlsLifetimeSeconds][&pageSize][&skip][&accessToken]`

**Parameters:**

| Name | **Description** | **Required** |
|--|--|--|
| **videoId** | ID of the video | true |
| **urlsLifetimeSeconds** | Lifetime of the URLs, in seconds | true |
| **pageSize** | Maximum number of frames to return for each call | false |
| **skip** | Number of frames to skip | false |
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
              ‾         "start": "0:00:32.72",
              ‾         "end": "0:00:42.72",
              ‾     }
            ‾   ]
          ‾ }
        ]
    }... 
```

## Bring Your Own model samples

- [Bring your own model samples](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/BringYourOwn-Samples)

## Related content

- [Use the Azure AI Video Indexer API](/azure/azure-video-indexer/video-indexer-use-apis)
