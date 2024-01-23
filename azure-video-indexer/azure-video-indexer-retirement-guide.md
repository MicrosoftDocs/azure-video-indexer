---
title: Preparing for AMS retirement - AVI update and migration guide  
description: Azure Video Indexer (AVI) used Azure Media Services (AMS) for encoding, packaging and streaming of media assets. AMS announced that it is retiring on June 30th, 2024. Therefore, AVI is removing the dependency on AMS. To continue using AVI, between February 15th and June 30th 2024, you must take steps to transition away from their current AVI account AMS dependency. Follow this guide.
ms.topic: conceptual
ms.service: azure-video-indexer
ms.date: 01/22/2024
ms.author: inhenkel
author: IngridAtMicrosoft
---


# Preparing for AMS retirement: AVI update and migration guide

Azure Video Indexer (AVI) used Azure Media Services (AMS) for encoding, packaging and streaming of media assets. AMS announced that it is retiring on June 30th, 2024. Therefore, AVI is removing the dependency on AMS.

To continue using AVI, between February 15th and June 30th 2024, you must take steps to transition away from their current AVI account AMS dependency and do the following:

1.  Update your AVI account so that it links to an Azure Storage account instead of an AMS account.
1.  Migrate the existing AVI AMS assets from the AMS managed storage account to the storage account you linked to the AVI account. While this is optional, if not done, once AMS is retired you won’t be able to access your previously indexed videos or their insights.

These changes impact many areas of AVI and the preparatory actions you must take will depend on how you are using AVI. Therefore, before performing an AVI account update, you should review how you are using AVI and make the needed changes to avoid your applications and platforms that use AVI from being adversely affected.

This document will discuss each of these changes, their impact, and what needs to be done to smoothly navigate them.

## Changes

The following is a description of the changes to the AVI product that apply once you have updated your account. Consider these changes and how they will affect your workflow and your code. They only apply once you have updated your account.

### Video upload

Uploading a video for indexing will no longer support the use of an AMS asset ID. A video URL or local file will be used instead.

### Account creation and management

-   **API**
    -   You must update your account creation and update requests to use the AVI API version 2023-01-01.
    -   Requests must be submitted with the [Azure Storage Account property](https://github.com/Azure/azure-rest-api-specs/blob/main/specification/vi/resource-manager/Microsoft.VideoIndexer/stable/2024-01-01/vi.json) rather than the AMS account.
-   **Portal** – During the AVI account creation process, the AVI account will be associated with the Azure Storage account.

### Storage account

Linking an Azure Storage account to an AVI account is permanent and can’t be undone. Therefore, it is recommended that you create a storage account that is solely for use with the AVI account. (This is especially important if you expect to use network restrictions.) It’s recommended that the storage account is in the same region as the AVI account.

You won’t be able to link your AVI account to the storage account that was previously associated with the AMS account. Keep in mind that when you create a new AVI account, it will be associated with a new storage account and not the one that you used with the AMS account.

### Streaming player

Azure Media Player is also being retired as of June 30th, 2024. If you have been using the AVI streaming endpoint to stream videos, you must choose a different player that supports Dash or HLS packaging as well as the use of a token in the request. AVI will be using the [Shaka player](https://developers.google.com/widevine/open-source/shaka-player).

### Streaming and Streaming endpoints

**Adaptive bitrate streaming** – Encoding and streaming with adaptive bitrate is no longer supported and indexing requests will fail if streaming is set to adaptive bitrate. Instead, submit a request to encode with either single bitrate or no streaming.

**Newly indexed video** - All API requests for a streaming URL will get a URL to an AVI endpoint rather than an AMS endpoint. The AVI endpoint will be prefixed with “vi-apim”.

**Previously indexed videos** – Your updated AVI account will still be able to stream your AMS assets until they have been migrated. In this case, responses to requests for a streaming URL, Get Streaming Video URL and Get Video Index, will differ depending on whether the assets have been migrated. Therefore, your application must be able to play from both the AMS endpoint and the AVI endpoints. The Shaka player will only be able to play AVI endpoints while AMP will be able to play AMS endpoints. .

**Unmigrated videos -** Requests for videos that aren’t migrated will return an AMS streaming URL until June 30th, 2024. After that date, you won’t be able to make requests to AMS at all.

### Projects

AVI has a Projects feature that can be used to edit and stitch together videos. Once your AVI account has been updated, the Project feature will be limited until your videos are migrated.

Existing projects will be playable, but you won’t be able to edit or render them. If needed, render and download the project files before you update your account.

If AVI is migrating your AVI AMS assets for you, projects will be disabled during the days/hours your assets are being migrated. Once the migration is complete, they will be playable.

You will receive an email notification that the migration is complete, and you can check the migration status on the AVI website as well.

### Billing

AVI won’t charge for streaming. AVI will charge a flat rate for encoding which will usually cost less than it previously cost to encode with AMS. The charge for encoding will appear as “Video Modification”. Remember to check if you need to change any billing alerts.

## Migration

> [!IMPORTANT] 
> Even after you have updated your account, AVI will still access your AMS account and its associated storage account until all your videos have been migrated. Until the migration is complete, it is important that you do not delete or change the accounts, roles, or permissions of the AMS, Azure Storage or AVI accounts. You will receive an email notification that the migration is complete, and you can check the migration status on the AVI website as well.

You have two options for migrating your videos:

1.  Asking for AVI assistance with migration, which is recommended.
1.  Not migrating.

### Recommended: Ask for AVI assistance with migration

AVI is offering to perform both file processing and asset migration. You can opt-in through the Azure portal or through an API request when you update your account up until the AMS retirement on June 30th, 2024. For more information, see [Azure AI Video Indexer Account types.](/azure/azure-video-indexer/accounts-overview)

Migration won’t happen immediately, but AVI commits to migrating your assets before the AMS retirement date.

Only your *AVI* associated AMS assets will be migrated. If other AMS assets exist on the same storage account, they won’t be migrated.

AVI won’t delete the original copies of your AMS files. After migration, you can delete them yourself if needed.

## Detailed updating and migrating instructions

For a complete step-by-step guide, see [Update your Azure Video Indexer account and migrate assets](update-your-azure-video-indexer-account-and-migrate-assets.md).
