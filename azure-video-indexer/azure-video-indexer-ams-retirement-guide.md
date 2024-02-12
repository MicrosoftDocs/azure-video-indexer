---
title: Preparing for AMS retirement - AVI update and migration guide  
description: Azure Video Indexer (AVI) used Azure Media Services (AMS) for encoding, packaging, and streaming of media assets. AMS announced that it's retiring on June 30, 2024. Therefore, AVI is removing the dependency on AMS. To continue using AVI, between February 15 and June 30 2024, you must take steps to transition away from their current AVI account AMS dependency. Follow this guide.
ms.topic: conceptual
ms.service: azure-video-indexer
ms.date: 01/29/2024
ms.author: inhenkel
author: IngridAtMicrosoft
---


# Preparing for AMS retirement: AVI update and migration guide

Azure Video Indexer (AVI) used Azure Media Services (AMS) for encoding, packaging, and streaming of media assets. AMS announced that it's retiring on June 30, 2024. Therefore, AVI is removing the dependency on AMS.

To continue using AVI, between February 15th and June 30th 2024, you must take the following steps to transition away from your current AVI account AMS dependency:

1.  Update your AVI account so that it links to an Azure Storage account instead of an AMS account.
1.  Migrate the existing AVI AMS assets from the AMS managed storage account to the storage account you linked to the AVI account. While this step is optional, if not done, once AMS is retired you won’t be able to access your previously indexed videos or their insights.

These changes impact many areas of AVI and the preparatory actions you must take depends on how you're using it. Therefore, before performing an AVI account update, you should review how you're using AVI and make the needed changes to keep your applications and platforms using AVI from being adversely affected.

This document discusses each of these changes, their impact, and what needs to be done to smoothly navigate them.

## Changes

The following is a description of the changes to the AVI product that apply once you have updated your account. Consider these changes and how they'll affect your workflow and your code. They only apply once you have updated your account.

### Video upload

The AMS asset ID will no longer be used for uploading a video. A video URL or local file will be used instead.

### Account creation and management

-   **API**
    -   You must update account creation and requests to use the AVI API version 2023-01-01.
    -   Requests must be submitted with the [Azure Storage Account property](https://github.com/Azure/azure-rest-api-specs/blob/main/specification/vi/resource-manager/Microsoft.VideoIndexer/stable/2024-01-01/vi.json) rather than the AMS account.
-   **Portal** – During the AVI account creation process, the AVI account will be associated with the Azure Storage account.

### Storage account

Linking an Azure Storage account to an AVI account is permanent and can’t be undone. Therefore, it's recommended that you create a storage account that is solely for use with the AVI account. (This is especially important if you expect to use network restrictions.) It’s recommended that the storage account is in the same region as the AVI account.

You won’t be able to link your AVI account to the storage account that was previously associated with the AMS account. 

### Streaming player

Azure Media Player is also being retired as of June 30, 2024. If you have been using the AVI streaming endpoint to stream videos, you must choose a different player that supports Dash or HLS packaging and the use of a token in the request. 

### Streaming and Streaming endpoints

**Adaptive bitrate streaming** – Encoding and streaming with adaptive bitrate is no longer supported and indexing requests will fail if streaming is set to adaptive bitrate. Instead, submit a request to encode with either single bitrate or no streaming.

**Newly indexed video** - All API requests for a streaming URL will get a URL to an AVI endpoint rather than an AMS endpoint. The AVI endpoint will be prefixed with “vi-apim.”

**Previously indexed videos** – Your updated AVI account will still be able to stream your AMS assets until they're migrated. In this case, responses to requests for a streaming URL, `Get Streaming Video URL` and `Get Video Index`, will differ depending on whether the assets have been migrated. Therefore, your application must be able to play from both the AMS endpoint and the AVI endpoints. For example, Shaka player will only be able to play AVI endpoints while AMP will be able to play AMS endpoints.

**Unmigrated videos -** Requests for videos that aren’t migrated will return an AMS streaming URL until June 30, 2024. After that date, you won’t be able to make requests to AMS at all.

### Projects

AVI has a Projects feature that can be used to edit and stitch together videos. Once your AVI account has been updated, the feature will be limited until your videos are migrated.

Existing projects will be playable, but you won’t be able to edit or render them. If needed, render and download the project files before you update your account.

If AVI is migrating your AVI AMS assets for you, projects will be disabled during the days/hours your assets are being migrated. Once the migration is complete, they'll be playable.

You'll receive an email notification that the migration is complete, and you can check the migration status on the AVI website as well.

### Billing

AVI won’t charge for streaming. AVI will charge a flat rate for encoding, which will cost less than it previously cost to encode with AMS. The charge for encoding will appear as “Video Modification." Remember to check if you need to change any billing alerts.

## Migration

### Recommended: Ask for AVI assistance with migration

AVI is offering to perform both file processing and asset migration. You can opt in through the Azure portal or through an API request when you update your account up until the AMS retirement on June 30, 2024. 

Migration won’t happen immediately, but AVI commits to migrating your assets before the AMS retirement date.

Only your *AVI* associated AMS assets will be migrated. If other AMS assets exist on the same storage account, they won’t be migrated.

AVI won’t delete the original copies of your AMS files. After migration, you can delete them yourself if needed.

> [!IMPORTANT] 
> Even after you have updated your account, AVI will still access your AMS account and its associated storage account until all your videos have been migrated. Until the migration is complete, it's important that you DO NOT delete or change the accounts, roles, or permissions of the AMS, Azure Storage or AVI accounts. You will receive an email notification that the migration is complete, and you can check the migration status on the AVI website as well.

Due to the AMS retirement, all AVI customers that persist AVI created videos and insights must process the assets to a new format and migrate them to the Azure Storage account linked to their AVI account. 

This requires the following two operations:

1. It reprocesses the media assets, converting the AMS assets to CMAF format with HLS and DASH manifests. This is needed for the assets to be streamed by Video Indexer and other players.
1. Storing of these reprocessed assets in the Azure Storage account that you have linked to your AVI account.

As AMS asset migration would be challenging to do on your own, AVI is providing a migration experience for both the file reprocessing and asset move. There's no cost for using the migration solution except storage of the migrated assets in a storage account and the networking costs associated with moving the data which should be low if both storage accounts are in the same region.

If an asset fails to migrate, despite AVI’s multiple attempts and retries to migrate it, the migration will be treated as completed with errors and you'll be sent a list of the files that failed to migrate. They can also be downloaded from the Migration page in the AVI website.

You can view the status and progress of your migration in the AVI website and will also receive a notification email once the migration is complete. 

As the migration solution will migrate all AVI AMS assets, it’s a good time to review and delete any files that are no longer needed and don’t need to be migrated. 

Once you have opted in to the migration, it's recommended that VI AMS assets are not deleted until you are notified that the migration is complete as they might not have been migrated yet.

Microsoft disclaims any liability for any damages in relation to the migration.

## Detailed updating and migrating instructions

For a complete step-by-step guide, see [Update your Azure Video Indexer account and migrate assets](update-your-azure-video-indexer-account-and-migrate-assets.md).

## FAQ

### Can we request that AVI only migrates some of our accounts AVI AMS assets?

No, it's all or nothing. Before starting the migration, you should review and delete any assets you don’t want migrated.

### I opted in to the AVI migrate solution but then changed my mind. Can I opt out? 

You aren't able to change the request through the portal or API and AVI might have already started migrating your assets. If needed, you can open a support ticket and if the migrate process hasn’t started yet, AVI might be able to cancel the request.

### Does AVI charge me for the migration? 

No, it’s a free experience. The only cost is the storage of the migrated assets in a storage account and the networking costs associated with moving the data which should be low if both storage accounts are in the same region.

### If I don’t use AVI for streaming or encoding, do I still have to migrate AVI AMS assets to continue accessing AVI insights?

No, unless you want to migrate the source video that you initially sent to AVI for indexing.

### If we don’t persist any video data, do we have to migrate AVI AMS assets? 

No, unless you want to migrate the source video that you initially sent to AVI for indexing.

### I see that my asset migration is in process – does it matter if a particular video has been migrated yet? 

In most cases no. The only scenario that is impacted is if you're using an AVI Streaming URL to play videos. Videos not yet migrated need to be played by a player that supports AMS assets, the Azure Media Player. Videos that were already indexed need to be played by a player that supports Dash or HLS packaging and the sending of a token in the request (such as Shaka, DashJS, or VideoJS).  

### How can I tell if a video has been migrated yet? 

By the reply of the Get Streaming URL request – if not yet migrated, it will contain mention of media service at the beginning.
