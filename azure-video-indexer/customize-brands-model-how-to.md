---
title: Customize a brands model in Azure AI Video Indexer
description: This article shows you how to customize a brands model with Azure AI Video Indexer.
author: cwatson-cat
ms.author: cwatson
ms.date: 07/13/2026
ms.service: azure-video-indexer
ms.topic: how-to
#customer intent: As a Video Indexer user, I want to customize brand detection so that results match my approved and excluded brands.
ai-usage: ai-assisted
appliesto:
  - Cloud-based Azure AI Video Indexer
---

# Customize a brands model in Azure AI Video Indexer

Azure AI Video Indexer supports brand detection from speech and visual text during indexing and reindexing of video and audio content. Brand detection identifies mentions of products, services, and companies suggested by Bing's brands database. For example, if Microsoft is mentioned in video or audio content, or appears in visual text in a video, Azure AI Video Indexer detects it as a brand.

Context disambiguates brands from other terms.

The custom brands model that you create is available only in the account where you created the model.

When you customize the brands model, you can:

- Choose whether Azure AI Video Indexer detects brands from the Bing brands database
- Exclude certain brands from being detected (essentially creating a list of unapproved brands)
- Include brands that should be part of your model that might not be in Bing's brands database (approved brands).

> [!NOTE]
> If you indexed your video before you added a brand, you need to reindex it. You can find **Re-index** in the drop-down menu for the video. Select **Advanced options** -> **Brand categories**, and then select **All brands**.

## Prerequisites

- An Azure account
- An Azure AI Video Indexer account

## [Web portal](#tab/customizewebportal)

## Edit brands model settings

Choose whether Azure AI Video Indexer detects brands from the Bing brands database. To set this option, edit your brands model settings.

1. Go to [Azure AI Video Indexer](https://www.videoindexer.ai/) and sign in.
1. Select **Content model customization** on the left side of the page to customize a model in your account.
1. To edit brands, select the **Brands** tab.
1. Select **Show brands suggested by Bing** if you want Azure AI Video Indexer to detect brands suggested by Bing. Clear the option if you don't.

## Include brands in the model

The **Include brands** section contains custom brands that you want Azure AI Video Indexer to detect, even if Bing doesn't suggest them.

### Add a brand to the include list

1. Select **+ Create new brand**.
1. Enter a name (required), category (optional), description (optional), and reference URL (optional).
  1. Use the category field to tag brands. This value appears as the brand's *tags* when you use the Azure AI Video Indexer APIs. For example, the brand `Azure` can be tagged or categorized as `Cloud`.
  1. The reference URL can be any reference website for the brand, such as a link to its Wikipedia page.
1. Select **Save**. The brand is added to the **Include brands** list.

### Edit a brand on the include list

You can update a brand's category, description, or reference URL. You can't change a brand name because brand names are unique. If you need to change a brand name, delete the brand (see the next section) and create a new one.

1. Select the pencil icon next to the brand that you want to edit. 
1. Select the **Update** button to update the brand with the new information.

### Delete a brand on the include list

1. Select the trash icon next to the brand that you want to delete.
1. Select **Delete**. The brand is no longer in your *Include brands* list.

## Exclude brands from the model

The **Exclude brands** section contains brands that you don't want Azure AI Video Indexer to detect.

### Add a brand to the exclude list

1. Select **+ Create new brand**.
1. Provide a name (required), category (optional).
1. Select **Save**. The brand is added to the **Exclude brands** list.

### Edit a brand on the exclude list

You can update only a brand's category. You can't change a brand name because brand names are unique. If you need to change a brand name, delete the brand (see the next section) and create a new one.

1. Select the pencil icon next to the brand that you want to edit.
1. Select the **Update** button to update the brand with the new information.

### Delete a brand on the exclude list

1. Select the trash icon next to the brand that you want to delete.
1. Select **Delete**. The brand is removed from your *Exclude brands* list.

## [API](#tab/customizeapi)

> [!NOTE]
> For all requests, setting `enabled` to `true` puts the brand in the *Include* list for Azure AI Video Indexer to detect.
> Setting `enabled` to `false` puts the brand in the *Exclude* list, so Azure AI Video Indexer *can't* detect it.

## Create a brand

Use the [Create Brand](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Brand) API request to create a new custom brand and add it to the custom brands model for the specified account.

Set other parameters in the request body:

* The `referenceUrl` value can be any reference website for the brand, such as a link to its Wikipedia page.
* The `tags` value is a list of tags for the brand. These tags appear in the brand's *Category* field in the Azure AI Video Indexer website. For example, the brand `Azure` can be tagged or categorized as `Cloud`.

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

## Delete a brand

Use the [Delete Brand](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Brand) API request to remove a brand from the custom brands model for the specified account. Specify the account in the `accountId` parameter. The brand is removed from both the *Include* and *Exclude* brands lists.

### Example response

No content is returned when the brand is deleted successfully.

## Get a specific brand

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

The [Update Brand](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Brand) request updates the details of a brand in the custom brands model for the specified account by using the brand ID.

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

## Get all brands

Use a [Get Brands](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Brands) API request to return all included and excluded brands in the custom brands model for the account.

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
      }
]
```

## Get brands model settings

Use a [Get Brands](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Brands) API request to return the brands model settings in the specified account. The brands model settings indicate whether detection from the Bing brands database is enabled. If Bing brands aren't enabled, Azure AI Video Indexer detects brands only from the specified account's custom brands model.

### Example response

```json
{
  "state": true,
  "useBuiltIn": true
}
```

## Update brands model settings

The [Update Brands Model Settings](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Brands-Model-Settings) request updates the brands model settings in the specified account. The brands model settings indicate whether detection from the Bing brands database is enabled. If Bing brands aren't enabled, Azure AI Video Indexer detects brands only from the custom brands model.

Setting the `useBuiltIn` flag to `true` enables Bing brands. Setting `useBuiltIn` to `false` disables Bing brands.

### Example response

No content is returned when the brands model setting is updated successfully.
