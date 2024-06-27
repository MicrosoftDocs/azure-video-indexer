---
title: Upload and index media with Azure AI Video Indexer (VI)
description: This article shows you how to upload and index media files (audio or video) with the Azure AI Video Indexer website using advanced settings.
ms.topic: article
ms.date: 06/26/2024
author: IngridAtMicrosoft
ms.author: inhenkel
ms.service: azure-video-indexer
---

# Upload and index media with Azure Video Indexer (VI)

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

This article shows you how to upload and index media files (audio or video) with the [Azure AI Video Indexer website](https://aka.ms/vi-portal-link) using advanced settings. If you would like to try a basic upload, see the [quickstart](try-vi-web-portal-quickstart.md).

## Prerequisites

- An Azure AI Video Indexer account. You can [sign up](https://aka.ms/vi-portal-link) for a free trial account, or create a [paid account](accounts-overview.md#paid-account).
- At least one media file. See [supported file formats](avi-support-matrix.md?branch=pr-en-us-272#supported-file-formats).
- To upload media files from a URL, you need a publicly accessible URL for the file that can be opened via a URL in a web browser.
- If the file is hosted in an Azure storage account, you need to [generate a SAS token URL](/azure/ai-services/document-intelligence/create-sas-tokens?view=form-recog-3.0.0&preserve-view=true) and paste it in the input box. 

You **can't** use URLs from streaming services such as YouTube.

## Upload the file

Use these steps to upload and index a video file. 

1. Sign in to the [Video Indexer website](https://aka.ms/vi-portal-link).
1. Select **Upload**.
1. Select the file source. You can upload up to 10 files at a time.
    - To upload from your file system, select **Browse files** and choose the files you want to upload. 
    - To add more files, select **Add file**. 
    - To remove a file, select **Remove** on the file name.
    - To upload from a URL, select **Enter URL**, paste the source file URL, and select **Add**.
1. Configure the basic settings for indexing or use the default configuration. You need to specify the following settings for each file:
    - **Privacy**: Choose whether the video URL will be publicly available or private after indexing.
    - **Streaming quality**: Choose the streaming quality for the video. You can select **Single bitrate**, or **No streaming** For more information, see [the streaming options](indexing-configuration-guide.md#streaming-quality-options)
    - **Video source language**: Choose the spoken language of the video to ensure high quality transcript and insights extraction. If you don't know the language or there's more than one spoken language, select **Auto-detect single language** or **Auto-detect multi-language**. For more information, see  [Language detection](multi-language-identification-transcription.md).
1. If it's the first time you're uploading a media file, check the consent checkbox to agree to the terms and conditions.
1. Configure the *general settings* for indexing. You can rename the files.
1. Configure the *advanced settings* for indexing. These settings are for all files in the batch:
    - **Indexing preset**: [Choose the preset](indexing-configuration-guide.md#indexing-options) that fits your needs. You can also exclude sensitive AI by selecting the checkbox.
    - **People model**: If you're using a [customized people](customize-person-model-overview.md) model, choose it from the dropdown list.
    - **Brand categories**: If you're using a [customized brand](customize-brands-model-overview.md) model, choose it from the dropdown list.
    - **File information**: If you want to add metadata, enter the text in the input box. Metadata is shared between all files in the same upload batch. When uploading a single file, you can add a description.
1. Select **Review + upload**.
1. Review the summary page that shows the indexing settings and the upload progress.
1. Select **Upload + index**.
1. When the file indexing is complete, select the Library tab, then select the media file to view insights. 

## Troubleshoot uploading issues

If you encounter any issues while uploading media files, try the following solutions:

- If the **Upload** button is disabled, hover over the button and check for the indication of the problem. 
- Try to refresh the page.
- If you're using a trial account, check the account quota for daily count, daily duration, or total duration. To view your quota and usage, select **Account settings**.
- If the upload from URL failed, check that:
    - the URL is valid and public. You should be able to view or hear the file from placing the URL in the browser location field. 
    - the media file isn't encrypted, protected by DRM, corrupted, or damaged. 
    - it's a [supported media file](/azure/media-services/latest/encode-media-encoder-standard-formats-reference).
    - the file size isn't larger than 2 GB. 
    - you have a stable internet connection.
