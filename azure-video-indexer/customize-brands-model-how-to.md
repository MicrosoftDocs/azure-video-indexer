---
title: Customize a brands model in Azure AI Video Indexer
description: This article shows you how to customize a brands model with Azure AI Video Indexer. 
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/09/2024
ms.service: azure-video-indexer
ms.topic: how-to
---

# Customize a brands model in Azure AI Video Indexer

Azure AI Video Indexer supports brand detection from speech and visual text during indexing and reindexing of video and audio content. Brand detection identifies the mention of products, services, and companies suggested by Bing's brands database. For example, if Microsoft is mentioned in a video or audio content or if it shows up in visual text in a video, Azure AI Video Indexer detects it as a brand. 

Brands are disambiguated from other terms using context. 

The custom brands model that you create are only available in the account in which you created the model.

Customizing the brands model allows you to: 

- Select whether or not Azure AI Video Indexer detects brands from the Bing brands database
- Exclude certain brands from being detected (essentially creating a list of unapproved brands)
- Include brands that should be part of your model that might not be in Bing's brands database (approved brands).

> [!NOTE]
> If your video was indexed before adding a brand, you need to reindex it. You can find the **Re-index** item in the drop-down menu associated with the video. Select **Advanced options** -> **Brand categories** and check **All brands**.

## Prerequisites

- An Azure account
- An Azure AI Video Indexer account

## [Web portal](#tab/customizewebportal)

## Edit brands model settings

You can set whether or not you want brands from the Bing brands database to be detected. To set this option, edit the settings of your brands model.

1. Go to the [Azure AI Video Indexer](https://www.videoindexer.ai/) website and sign in.
1. To customize a model in your account, select the **Content model customization** button on the left of the page.
1. To edit brands, select the **Brands** tab.
1. Check the **Show brands suggested by Bing** option if you want Azure AI Video Indexer to detect brands suggested by Bing—leave the option unchecked if you don't.

## Include brands in the model

The **Include brands** section represents custom brands that you want Azure AI Video Indexer to detect, even if they aren't suggested by Bing.  

### Add a brand to include list

1. Select **+ Create new brand**.
1. Provide a name (required), category (optional), description (optional), and reference URL (optional). 
  1. The category field is meant to help you tag your brands. This field shows up as the brand's *tags* when using the Azure AI Video Indexer APIs. For example, the brand `Azure` can be tagged or categorized as `Cloud`. 
  1. The reference URL field can be any reference website for the brand (like a link to its Wikipedia page).
1. Select **Save**. The brand is added to the **Include brands** list.

### Edit a brand on the include list

You can update the category, description, or reference URL of a brand. You can't change the name of a brand because names of brands are unique. If you need to change the brand name, delete the entire brand (see next section) and create a new brand with the new name.

1. Select the pencil icon next to the brand that you want to edit. 
1. Select the **Update** button to update the brand with the new information.

### Delete a brand on the include list

1. Select the trash icon next to the brand that you want to delete.
1. Select **Delete**. The brand is no longer in your *Include brands* list.

## Exclude brands from the model

The **Exclude brands** section represents the brands that you don't want Azure AI Video Indexer to detect.

### Add a brand to exclude list

1. Select **+ Create new brand.**
1. Provide a name (required), category (optional).
1. Select **Save**. The brand is added to the **Exclude brands** list.

### Edit a brand on the exclude list

You can only update the category of a brand. You can't change the name of a brand because names of brands are unique. If you need to change the brand name, delete the entire brand (see next section) and create a new brand with the new name.

1. Select the pencil icon next to the brand that you want to edit.
1. Select the **Update** button to update the brand with the new information.

### Delete a brand on the exclude list

1. Select the trash icon next to the brand that you want to delete.
1. Select **Delete**. The longer appears in your *Exclude brands* list.

## [API](#tab/customizeapi)

> [!NOTE]
> For all requests, setting `enabled` to `true` puts the brand in the *Include* list for Azure AI Video Indexer to detect.
> Setting `enabled` to `false` puts the brand in the *Exclude* list, so Azure AI Video Indexer *can't* detect it.

## Create a brand

You can use a [Create Brand](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Brand) API request to create a new custom brand and adds it to the custom brands model for the specified account.

Some other parameters that you can set in the body:

* The `referenceUrl` value can be any reference websites for the brand, such as a link to its Wikipedia page.
* The `tags` value is a list of tags for the brand. This tag shows up in the brand's *Category* field in the Azure AI Video Indexer website. For example, the brand `Azure` can be tagged or categorized as `Cloud`.

### Example response

```json
{
  "referenceUrl": "https://en.wikipedia.org/wiki/Example",
  "id": 97974,
  "name": "Example",
  "accountId": "SampleAccountId",
  "lastModifierUserName": "SampleUserName",
  "created": "2018-04-25T14:59:52.7433333",
  "lastModified": "2018-04-25T14:59:52.7433333",
  "enabled": true,
  "description": "This is an example",
  "tags": [
    "Tag1",
    "Tag2"
  ]
}
```

## Delete a Brand

You can use a [Delete Brand](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Brand) API request to remove a brand from the custom Brands model for the specified account. The account is specified in the `accountId` parameter. The brand is no longer in the *Include* or *Exclude* brands lists.

### Example response

There's no returned content when the brand is deleted successfully.

## Get a specific Brand

Use a [Get Brand](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Brand) API request to search for the details of a brand in the custom brands model for the specified account using the brand ID.

### Example response

```json
{
  "referenceUrl": "https://en.wikipedia.org/wiki/Example",
  "id": 128846,
  "name": "Example",
  "accountId": "SampleAccountId",
  "lastModifierUserName": "SampleUserName",
  "created": "2018-01-06T13:51:38.3666667",
  "lastModified": "2018-01-11T13:51:38.3666667",
  "enabled": true,
  "description": "This is an example",
  "tags": [
    "Tag1",
    "Tag2"
  ]
}
```

## Update a specific brand

The [Update Brand](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Brand) request lets you search for the details of a brand in the custom Brands model for the specified account using the brand ID.

### Example response

```json
{
  "referenceUrl": null,
  "id": 97974,
  "name": "Example",
  "accountId": "SampleAccountId",
  "lastModifierUserName": "SampleUserName",
  "Created": "2018-04-25T14:59:52.7433333",
  "lastModified": "2018-04-25T15:37:50.67",
  "enabled": false,
  "description": "This is an update example",
  "tags": [
    "Tag1",
    "NewTag2"
  ]
}
```

## Get all of the Brands

You can use a [Get Brands](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Brands) API request to return all of the brands in the custom brands, included and excluded, for the account.

### Example response

```json
[
    {
        "ReferenceUrl": null,
        "id": 97974,
        "name": "Example",
        "accountId": "AccountId",
        "lastModifierUserName": "UserName",
        "Created": "2018-04-25T14:59:52.7433333",
        "LastModified": "2018-04-25T14:59:52.7433333",
        "enabled": true,
        "description": "This is an example",
        "tags": ["Tag1", "Tag2"]
    },
    {
        "ReferenceUrl": null,
        "id": 97975,
        "name": "Example2",
        "accountId": "AccountId",
        "lastModifierUserName": "UserName",
        "Created": "2018-04-26T14:59:52.7433333",
        "LastModified": "2018-04-26T14:59:52.7433333",
        "enabled": false,
        "description": "This is another example",
        "tags": ["Tag1", "Tag2"]
    },
]
```

## Get Brands model settings

You can use a [Get Brands](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Brands) API request to return the Brands model settings in the specified account. The Brands model settings represent whether detection from the Bing brands database is enabled or not. If Bing brands aren't enabled, Azure AI Video Indexer only detects brands from the custom Brands model of the specified account.

### Example response

```json
{
  "state": true,
  "useBuiltIn": true
}
```

## Update Brands model settings

The [Update Brands Model Settings](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Brands-Model-Settings) request updates the Brands model settings in the specified account. The Brands model settings represent whether detection from the Bing brands database is enabled or not. If Bing brands aren't enabled, Azure AI Video Indexer only detects brands from the custom Brands model.

The `useBuiltIn` flag set to true means that Bing brands are enabled. If `useBuiltin` is false, Bing brands are disabled.

### Example response

There's no returned content when the Brands model setting is updated successfully.
