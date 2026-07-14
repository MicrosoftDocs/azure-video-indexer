---
title: Use the Azure AI Video Indexer API
description: This article describes how to get started with Azure AI Video Indexer APIs.
author: cwatson-cat
ms.author: cwatson
ms.date: 07/13/2026
ms.service: azure-video-indexer
ms.topic: how-to
ms.custom: se-defect-target
ai-usage: ai-assisted
#customer intent: As a developer, I want to authenticate and call Azure AI Video Indexer APIs so that I can automate media indexing workflows.
appliesto:
    - Cloud-based Azure AI Video Indexer
---

# Use Azure AI Video Indexer APIs

In this article, you learn how to get API credentials and call Azure AI Video Indexer APIs by using a paid account.  
This article helps you automate indexing workflows instead of relying only on the web experience.
You can't use the API with a trial account.

## Prerequisites

1. Create an Azure AI Video Indexer [standard account](create-account.md).
1. Upload a media file. There are two ways:
    1. **Upload a media file to the URL of your choice (recommended)**. You can use a public network location. After you upload the file, check whether Azure AI Video Indexer can access the file by copying and pasting the URL into your browser's location bar. If you can play the media file, then it's likely that Azure AI Video Indexer can also access it. If you want to secure the storage location by using Azure Storage Blob, upload the file and get a SAS URL. For more information about getting a secure URL for your file, see [Azure Blob Storage SAS URLs](/azure/storage/common/storage-sas-overview). This URL is used to copy your file to Azure AI Video Indexer for indexing. If the storage account is behind a firewall, see [Upload videos from a firewall-protected storage account](storage-behind-firewall.md#upload-videos-from-a-firewall-protected-storage-account) for the required `useManagedIdentityToDownloadVideo` parameter.
    1. **Send the video file as a byte array in the request body**. For more information about uploading a media file as a byte array in a request body, see [Upload a blob with .NET](/azure/storage/blobs/storage-blob-upload).

## Subscribe to the API

1. **Sign in** to the [Azure AI Video Indexer API developer portal](https://api-portal.videoindexer.ai/) with the account you created.
1. **Find, copy, and save the primary and secondary keys**. You can find your subscription in your **[Profile](https://api-portal.videoindexer.ai/profile)**. The primary and secondary keys are in the **Subscriptions** section.
1. Select the **Show** link for both the Primary key and the Secondary key. Copy and paste them to a text editor until you're ready to use them in your environment variables file.

## Get authorization examples and API samples

For authorization examples specific to your development language, see the [Samples](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/API-Samples).

## Try the API in a web browser

You can explore requests [with the API](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Account-Access-Token) by using the Try It button in the API reference.
