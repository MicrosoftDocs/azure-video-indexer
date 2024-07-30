---
title: Use the Azure AI Video Indexer API
description: This article describes how to get started with Azure AI Video Indexer API and a trial account.
ms.date: 07/25/2024
ms.topic: quickstart
author: IngridAtMicrosoft
ms.author: inhenkel
ms.service: azure-video-indexer
---

# Quickstart: Use the API

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-abbreviated.md)]

Azure AI Video Indexer consolidates various audio and video artificial intelligence (AI) technologies offered by Microsoft into one integrated service, making development simpler. Azure AI Video Indexer is designed to enable developers to focus on using media AI technologies without worrying about scale, global reach, availability, and reliability of cloud platforms. You can use the API to upload your files, get detailed video insights, get URLs of embeddable insights, player widgets, and more.

[!INCLUDE [accounts](./includes/create-accounts-intro.md)]

This article shows you how to use the [Azure AI Video Indexer API](https://api-portal.videoindexer.ai/).

## Prerequisites

Upload a media file. There are two ways:
    
1. **Upload a media file to the URL of your choice (recommended)**. You can use a public network location. After you upload the file, you can check whether the file is accessible to AVI by copying and pasting it into your browser's location bar. If you can play the media file, then it's likely that VI can also access it. If you would like to secure the storage location using Azure Storage Blob, upload the file and obtain a SAS URL. For more information about getting a secure URL for your file, see [Azure Blob Storage SAS URLs](/azure/storage/common/storage-sas-overview). This URL is used to copy your file to Azure AI Video Indexer for indexing.
    
1. **Send the video file a byte array in the request body**. For more information about uploading a media file as a byte array in a request body, see [Upload a blob with .NET](/azure/storage/blobs/storage-blob-upload).

> [!NOTE]
> There is an API request limit of 10 requests per second and up to 120 requests per minute.

## Subscribe to the API

> [!Important]
> - You must use the same email you used when you signed up for Azure AI Video Indexer.
> - Personal Google and Microsoft (Outlook/Live) accounts can only be used for trial accounts. Accounts connected to Azure require Entra ID.
> - There can be only one active account per email. If a user tries to sign in with *user@gmail.com* for LinkedIn and later with *user@gmail.com* for Google, the latter will display an error page, saying the user already exists.
> - Keys should be protected. The keys should only be used by your server code. They shouldn't be available on the client side (.js, .html, and so on).

1. **Sign in** to the [Azure AI Video Indexer API developer portal](https://api-portal.videoindexer.ai/).
1. **Subscribe** by selecting the [Products](https://api-portal.videoindexer.ai/products) tab. Then, select **Authorization** and subscribe. New users are automatically subscribed to Authorization.
1. **Find, copy and save the primary and secondary keys**. You can find your subscription in your **[Profile](https://api-portal.videoindexer.ai/profile)**. The primary and secondary keys are in the **Subscriptions** section.
1. Select the **Show** link for both the Primary key and the Secondary key. Copy and paste them to a text editor until you're ready to use them in your environment variables file.

## Obtain an access token using the Authorization API

You don't want to give full access to every user for your application. There are several levels of access for VI.

| Level | View videos | Process videos | View projects | Process projects | View accounts | Manage accounts | 
| ----------------------- | --- | --- | --- | --- | --- | --- | 
| **Video Reader**        | :heavy_check_mark: | | | | | |
| **Video Contributor**   | :heavy_check_mark: | :heavy_check_mark: | | | | |
| **Project Reader**      | :heavy_check_mark: | | :heavy_check_mark: | | | |
| **Project Contributor** | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | | |
| **Account Reader**      | :heavy_check_mark: | | :heavy_check_mark: | | :heavy_check_mark: | |
| **Account Contributor** | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |

### Create and send the access token request

Set the `subscription-id`, the `resource-group-name`, the VI `account-name` in the request and set the `scope` and `permissionType` parameter in the request body to the access level you need. 

For example, if you want to provide access to a user so that they can work with projects but can't work with accounts, set the `permissionType` to "Contributor" and the `scope` to "Project." IF setting permissions for a project, provide the `projectId`. 

```HTTP

POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.VideoIndexer/accounts/{account-name}/generateAccessToken?api-version=2024-01-01

{
  "permissionType": "Reader",
  "scope": "Project",
  "projectId": "07ec9e38d4"
}

```

### Sample response

```json
{
  "accessToken": "<jwt token of 1260 characters length>"
}
```

For more examples of setting the scope and permission types, see the [VI REST API](/rest/api/videoindexer/generate/access-token?view=rest-videoindexer-2024-01-01&preserve-view=true).

## Start using the API

You're ready to start using the API. Find [the detailed description of each Azure AI Video Indexer REST API](https://api-portal.videoindexer.ai/).

For a detailed example of using the keys in your environment variable file, and using access tokens see the Azure AI Video Indexer [sample](https://github.com/Azure-Samples/azure-video-indexer-samples/blob/master/API-Samples/C%23/ArmBased/Program.cs). 

## Recommendations

- When you call the API that gets video insights for the specified video, you get a detailed JSON output as the response content.
- The JSON output produced by the API contains `Insights` and `SummarizedInsights` elements. We highly recommend using `Insights` and not using `SummarizedInsights` (which is present for backward compatibility).
- We don't recommend that you use data directly from the artifacts folder for production purposes. Artifacts are intermediate outputs of the indexing process and are raw outputs of the various AI engines that analyze the videos. The artifacts schema can change over time. 
- Use the [Get Video Index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Index) API and **not** [Get-Video-Artifact-Download-Url](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Artifact-Download-Url).
