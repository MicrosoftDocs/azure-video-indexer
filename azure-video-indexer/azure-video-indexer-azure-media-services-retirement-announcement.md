---
title: Azure AI Video Indexer (VI) changes related to Azure Media Service (AMS) retirement  
description: This article explains the upcoming changes to Azure AI Video Indexer (VI) related to the retirement of Azure Media Services (AMS).
ms.topic: conceptual
ms.date: 06/10/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Changes related to Azure Media Service (AMS) retirement

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

This article explains the upcoming changes to Azure AI Video Indexer (VI) resulting from the [retirement of Azure Media Services (AMS)](/azure/media-services/latest/azure-media-services-retirement).

Currently, VI requires the creation of an AMS account. Additionally, VI uses AMS for video encoding and streaming operations. The required changes will affect all VI customers. See the official AI VI announcement [here](https://azure.microsoft.com/updates/videoindexer-2/).

To continue using VI beyond June 30, 2024, all customers **must** make changes to their VI accounts to remove the AMS dependency. Detailed guidance for converting VI accounts will be provided in February 2024 when the new account type is released.

## Pricing and billing

Currently, VI uses AMS for encoding and streaming for the VI player. AMS charges you for both encoding and streaming. In the future, VI will encode media and you'll be billed using the updated VI accounts. Pricing details will be shared in February 2024. There will be no charge for the VI video player.

## VI changes

VI will continue to offer the same insights, performance, and functionality. However, a few aspects of the service will change which fall under the following three categories:

- Account changes
- API changes
- Product changes

## Account changes

VI has three account types. All will be impacted by the AMS retirement. The account types are:

- ARM-based accounts
- Classic accounts
- Trial accounts

See [Azure AI Video Indexer account types](/azure/azure-video-indexer/accounts-overview) to understand more about VI account types.

### Azure Resource Manager (ARM)-based accounts

**New accounts:** As of February 15, all newly created VI accounts will be non-AMS dependent accounts. You'll no longer be able to create AMS-dependent accounts.

**Existing accounts**: Existing accounts will continue to work through June 30, 2024. To continue using the account beyond June 30, customers must go through the process to convert their account to a non-AMS dependent account. If you don’t convert your account to a non-AMS dependent account, you won't be able to access the account or use it beyond June 30.

### Classic accounts

- **New accounts:** As of February 15, all newly created VI accounts will be non-AMS dependent accounts. You'll no longer be able to create Classic accounts.
- **Existing accounts:** Existing classic accounts will continue to work through June 30, 2024. VI will release an updated API version for the non-AMS dependent accounts that doesn’t contain any AMS related parameters.

To continue using the account beyond June 30, 2024, classic accounts will have to go through two steps:

1. Connect the account as an ARM-based account. You can connect the accounts already. See [Azure AI Video Indexer accounts](accounts-overview.md) for instructions.
1. Make the required changes to the VI account to remove the AMS dependency. If this isn’t done, you won't be able to access the account or use it beyond June 30, 2024.

### Existing trial accounts

- As of February 15, 2024 Video Indexer trial accounts will continue to work as usual. However, when using them through the APIs, customers must use the updated APIs.
- VI supports [importing content](import-content-from-trial.md) from a trial VI account to a paid VI account. This import option will be supported only until **February 15th, 2024**.

## API changes

**Between February 15 to June 30, 2024**, VI will support both existing data and control plane APIs as well as the updated APIs that exclude all AMS related parameters.

New VI accounts as well as existing VI accounts that have completed the steps to remove all AMS dependencies will only use the updated APIs that will exclude all AMS related parameters.

**On July 1, 2024**, code using APIs with AMS parameters will no longer be supported. This applies to both control plane and data plane operations.

### Breaking API changes

There will be breaking API changes. The following table describes the changes for your awareness, but actionable guidance will be provided when the changes have been released.

| **Type** | **API Name** |  **Change** |
|---|---|---|
| **ARM** | Create<br/>Update<br/>Patch<br/>ListAccount | - The `mediaServices` Account property will be replaced with a `storageServices` Account property.<br/><br/> - The `Identity` property will change from an `Owner` managed identity to `Storage Blob Data Contributor` permissions on the storage resource. |
| **ARM** | Get<br/>MoveAccount | The `mediaServices` Account property will be replaced with a `storageServices` Account property. |
| **ARM** | GetClassicAccount<br/>ListClassicAccounts |  API will no longer be supported. |
| **Classic** | CreatePaidAccountManually | API will no longer be supported. |
| **Classic** | UpdateAccountMediaServicesAsync |  API will no longer be supported. |
| **Data plane** | Upload | Upload will no longer accept the `assetId` parameter. |
| **Data plane** | Upload<br/>ReIndex<br/>Redact | `AdaptiveBitrate` will no longer be supported for new uploads. |
| **Data plane** | GetVideoIndex | `PublishedUrl` property will always be null. |
| **Data plane** | GetVideoStreamingURL | The streaming URL will return references to VI account endpoints rather than AMS account endpoints. |

Full details of the API changes and alternatives will be provided when the updated APIs are released.

## Product changes

As of July 1, 2024, VI won’t use AMS for encoding or streaming. As a result, it will no longer support the following:

- Encoding with adaptive bitrate will no longer be supported. Only single bitrate will be supported for new indexing jobs. Videos already encoded with adaptive bitrate will be playable in the VI player.
- Video Indexer [dynamic encryption](/azure/media-services/latest/drm-content-protection-concept) of media files will no longer be supported.
- Media files created by non-AMS dependent accounts won’t be playable by the [Azure Media Player](https://azure.microsoft.com/products/media-services/media-player).
- Using a Cognitive Insights widget and playing the content with the Azure Media Player outlined [here](video-indexer-embed-widgets.md) will no longer be supported.
