---
title: Use the Azure AI Video Indexer API
description: This article describes how to get started with Azure AI Video Indexer API and a trial account.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.collection: ce-skilling-ai-copilot
ms.date: 11/07/2024
ms.service: azure-video-indexer
ms.topic: quickstart
ms.custom: se-defect-target
---

# Quickstart: Use the API

This article shows you how to use the [Azure AI Video Indexer API](https://api-portal.videoindexer.ai/). You can't use the API with the trial account.

## Prerequisites

1. Create an Azure AI Video Indexer [standard account](create-account.md).
1. Upload a media file. There are two ways:
    1. **Upload a media file to the URL of your choice (recommended)**. You can use a public network location. After you upload the file, you can check whether the file is accessible to AVI by copying and pasting it into your browser's location bar. If you can play the media file, then it's likely that VI can also access it. If you would like to secure the storage location using Azure Storage Blob, upload the file and obtain a SAS URL. For more information about getting a secure URL for your file, see [Azure Blob Storage SAS URLs](/azure/storage/common/storage-sas-overview). This URL is used to copy your file to Azure AI Video Indexer for indexing.
    1. **Send the video file a byte array in the request body**. For more information about uploading a media file as a byte array in a request body, see [Upload a blob with .NET](/azure/storage/blobs/storage-blob-upload).

## Subscribe to the API

1. **Sign in** to the [Azure AI Video Indexer API developer portal](https://api-portal.videoindexer.ai/) with the account you created.
1. **Find, copy and save the primary and secondary keys**. You can find your subscription in your **[Profile](https://api-portal.videoindexer.ai/profile)**. The primary and secondary keys are in the **Subscriptions** section.
1. Select the **Show** link for both the Primary key and the Secondary key. Copy and paste them to a text editor until you're ready to use them in your environment variables file.

## Authorization and samples

For authorization examples specific to your development language, see the [Samples](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/API-Samples).

## Try the API in a web browser

You can explore requests [with the API](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Account-Access-Token) using the Try It button in the reference.
