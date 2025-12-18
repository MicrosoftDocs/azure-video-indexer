---
title: Detect textual logo with Azure AI Video Indexer
description: This article gives an overview of Azure AI Video Indexer textual logo detection.
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
appliesto:
  - Cloud-based Azure AI Video Indexer
---

# How to detect textual logo

> [!NOTE]
> Textual logo detection creation process is currently available through API. The result can be viewed through the Azure AI Video Indexer [website](https://www.videoindexer.ai/). 

**Textual logo detection** insights are based on the Optical Character Recognition (OCR) textual detection, which matches a specific predefined text.

For example, if you created the textual logo `Microsoft`, appearances of the word `Microsoft` are detected as the Microsoft logo. A logo can have different variations. These variations can be associated with the main logo name. For example, you might have under the `Microsoft` logo the following variations: `MS`, `MSFT`, and so on.

```json
{
    "name": "Microsoft",
    "wikipediaSearchTerm": "Microsoft",
    "textVariations": [{
    "text": "Microsoft",
    "caseSensitive": false
    }, {
    "text": "MSFT",
    "caseSensitive": true
    }]
}
```

:::image type="content" source="./media/textual-logo-detection/microsoft-example.png" border="true" alt-text="Screenshot Azure AI Video Indexer textual logo detection." lightbox="./media/textual-logo-detection/microsoft-example.png" :::

## Prerequisite

The Azure Video Index account must have at least the `contributor` role assigned to the resource.

## How to use

In order to use textual logo detection, follow these steps, described in this article: 

1. Create a logo instance using with a [Create logo](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Logo) API request (with variations).  

    * Save the logo ID. 
1. Create a logo group using a [Create Logo Group](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Logo-Group) API request. 

    * Associate the logo instance with the group when creating the new group (by pasting the ID in the logos array). 
1. Upload a video using: **Advanced video** or **Advance video + audio** preset, use the `logoGroupId` parameter to specify the logo group you would like to index the video with. 

## Create a logo instance

Use a [Create logo](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Logo) API request to create your logo. You can use the **try it** button.

:::image type="content" source="./media/textual-logo-detection/logo-api.png" border="true" alt-text="Screenshot showing an example of a Create logo API request." lightbox="./media/textual-logo-detection/logo-api.png" :::

In this example, we use the example supplied as default: 

Insert the following parameters:

* `Location`: The location of the Azure AI Video Indexer account.
* `Account ID`: The ID of the Azure AI Video Indexer account.
* `Access token`: The token, at least at a contributor level permission. 

The default body is: 
  
```json
{
    "name": "Microsoft",
    "wikipediaSearchTerm": "Microsoft",
    "textVariations": [{
    "text": "Microsoft",
    "caseSensitive": false
    }, {
    "text": "MSFT",
    "caseSensitive": true
    }]
}
```

|Key|Value|
|---|---|
|Name|Name of the logo used in the Azure AI Video Indexer website.|
|wikipediaSearchTerm|Term used to create a description in the Video Indexer website.|
|text|The text the model uses for comparison. Make sure to add the obvious name as part of the variations. For example, Microsoft.|
|caseSensitive| Determines whether the text is case sensitive. Set to true/false according to the variation.|

The response should return **201 Created**.

```json
HTTP/1.1 201 Created

content-type: application/json; charset=utf-8

{
    "id": "id"
    "creationTime": "2023-01-15T13:08:14.9518235Z",
    "lastUpdateTime": "2023-01-15T13:08:14.9518235Z",
    "lastUpdatedBy": "Jhon Doe",
    "createdBy": "Jhon Doe",
    "name": "Microsoft",
    "wikipediaSearchTerm": "Microsoft",
    "textVariations": [{
        "text": "Microsoft",
        "caseSensitive": false,
        "creationTime": "2023-01-15T13:08:14.9518235Z",
        "createdBy": "Jhon Doe"
    }, {
        "text": "MSFT",
        "caseSensitive": true,
        "creationTime": "2023-01-15T13:08:14.9518235Z",
        "createdBy": "Jhon Doe"
    }]
}
```
## Create a new textual logo group 
 
Use a [Create Logo Group](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Logo-Group) API request to create a logo group. Use the **try it** button. 
 
Insert the following parameters: 

* `Location`: The location of the Azure AI Video Indexer account.
* `Account ID`: The ID of the Azure AI Video Indexer account.
* `Access token`: The token, at least at a contributor level permission. 

:::image type="content" source="./media/textual-logo-detection/logo-group-api.png" border="true" alt-text="Screenshot showing an example of the Create Logo Group API request." lightbox="./media/textual-logo-detection/logo-group-api.png" :::

In the **Body** paste the logo ID from the previous step.

```json
{
    "logos": [{
        "logoId": "id"
    }],
    "name": "Technology",
    "description": "A group of logos of technology companies."
}
```

* The default example has two logo IDs. The first group was created with only one logo ID.

    The response should return **201 Created**. 

    ```
    HTTP/1.1 201 Created
    
    content-type: application/json; charset=utf-8
    
    {
        "id": "id",
        "creationTime": "2023-01-15T14:41:11.4860104Z",
        "lastUpdateTime": "2023-01-15T14:41:11.4860104Z",
        "lastUpdatedBy": "Jhon Doe",
        "createdBy": "Jhon Doe",
        "logos": [{
            "logoId": " e9d609b4-d6a6-4943-86ff-557e724bd7c6"
        }],
        "name": "Technology",
        "description": "A group of logos of technology companies."
    }    
    ```

## Upload from URL 
 
Use the upload API call: 

Specify the following parameters:

- `Location`: The location of the Azure AI Video Indexer account
- `Account`: The ID of the Azure AI Video Indexer account
- `Name`: The name of the media file you're indexing
- `Language`: `en-US`. For more information, see [Language support](language-support.md).
- `IndexingPreset`: Select **Advanced Video/Audio+video**  
- `Videourl`: The url
- `LogoGroupID`: GUID representing the logo group (you got it in the response when creating it)
- `Access token`: The token, at least at a contributor level permission
 
## Inspect the output 

Assuming the textual logo model finds a match, you're able to view the result in the [Azure AI Video Indexer website](https://www.videoindexer.ai/).
 
### Insights  

A new section would appear in the insights panel showing the number of custom logos that were detected. One representative thumbnail is displayed representing the new logo. 

:::image type="content" source="./media/textual-logo-detection/logo-insight.png" border="true" alt-text="Screenshot showing a detected custom logo using Insights." lightbox="./media/textual-logo-detection/logo-insight.png" :::

### Timeline 

When switching to the Timeline view, under the **View**, mark the **Logos** checkbox. All detected thumbnails are displayed according to their time stamp.

:::image type="content" source="./media/textual-logo-detection/logo-timeline.png" border="true" alt-text="Screenshot showing the logo timeline." lightbox="./media/textual-logo-detection/logo-timeline.png" :::

All logo instances that were recognized with a certainty above 80% present are displayed. The extended list of detections, including low certainty detection, are available in the [Artifacts](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Artifact-Download-Url) file.

## Add a logo to an existing logo group

In the first part of this article, there was one instance of a logo and associated to the right logo group upon the creation of the logo group. If all logo instances are created before the logo group is created, they can be associated with logo group on the creation phase. However, if the group was already created, the new instance should be associated to the group following these steps:

1. Create the logo.

    1. Copy the logo ID.
1. [Get logo groups](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Logo-Groups). 

    1. Copy the logo group ID of the right group. 
1. [Get logo group](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Logo-Group).

    1. Copy the response the list of logos IDs:

    Logo list sample:

    ```json
    "logos": [{
        "logoId": "id"
    }],
    ```
1. [Update logo group](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Logo-Group).

    1. Logo group ID is the output received at step 2.
    1. At the *Body* of the request, paste the existing list of logos from step 3.
    1. Then add to the list the logo ID from step 1.
1. Validate the response of the [Update logo group](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Logo-Groups) making sure the list contains the previous IDs and the new.

## Additional information and limitations 
 
* A logo group can contain up to 50 logos.
* One logo can be linked to more than one group.
* Use the [Update logo group](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Logo-Groups) to add the new logo to an existing group.
