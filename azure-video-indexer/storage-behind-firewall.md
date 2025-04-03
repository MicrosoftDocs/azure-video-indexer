---
title: Use Video Indexer with storage behind firewall
description: This article gives an overview how to configure Azure AI Video Indexer to use storage behind firewall.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 04/03/2025
ms.service: azure-video-indexer
ms.topic: article
---

# Configure Video Indexer to work with storage accounts behind firewall

One of the benefits of using trusted storage is that it disables public access to your storage account. Another benefit of using trusted storage is the ability to grant access to trusted Azure services.

When you create a Video Indexer account, you must associate it with an Azure Storage account. *Storage accounts for VI must be a Standard general-purpose v2 storage account*. Video Indexer accesses the storage account using user assigned or system assigned Managed Identity authentication. Video Indexer validates that the user adding the association has access to the storage account with Azure Resource Manager Role Based Access Control (RBAC).

To secure your storage account, you can use [trusted storage access](/azure/storage/common/storage-network-security?tabs=azure-portal#grant-access-to-trusted-azure-services) through which your firewall configuration. It enables only trusted Azure platform services to access the storage account. With it, [Managed Identities](/previous-versions/azure/media-services/latest/concept-managed-identities) allows Video Indexer to access the storage account.

Use the following information to enable Managed Identity for Storage and then lock your storage account. It assumes that you already created a Video Indexer account and associated the Storage account.

## Assign the Managed Identity and role

Follow all of the steps for [creating an Azure AI Video Indexer account](/azure/azure-video-indexer/create-account?tabs=portal), but also use the following steps:

1. When you select **Assign Role**, the `Azure Storage : Storage Blob Data Owner` role is assigned. You can verify or manually set assignments by navigating to the **Identity** menu of your Video Indexer account and selecting **Azure Role Assignments**.
1. Navigate to your Storage account. Select **Networking** from the menu and select **Enabled from selected virtual networks and IP addresses** in the **Public network access** section.
1. Under **Exceptions**, make sure that **Allow Azure services on the trusted services list to access this storage account** is selected.