---
title: Set up Azure AI Video Indexer with firewall-protected storage
description: Learn how to configure Azure AI Video Indexer with firewall-protected storage accounts to secure your data. Get started now.
author: cwatson-cat
ms.author: cwatson
ms.date: 10/06/2025
ms.service: azure-video-indexer
ms.topic: how-to
appliesto:
  - Cloud-based Azure AI Video Indexer
# customer intent: As an Azure user, I want to configure Video Indexer to work with storage accounts behind firewall so that I can secure my data.
---

# Set up Video Indexer with firewall-protected storage

One of the benefits of using trusted storage is that it disables public access to your storage account. Another benefit of using trusted storage is the ability to grant access to trusted Azure services.

When you create a Video Indexer account, you must associate it with an Azure Storage account. *Storage accounts for VI must be a Standard general-purpose v2 storage account*. Video Indexer accesses the storage account using user-assigned or system-assigned managed identity authentication. Video Indexer validates that the user adding the association has access to the storage account with Azure Resource Manager Role Based Access Control (RBAC).

To secure your storage account, you can use [trusted storage access](/azure/storage/common/storage-network-security?tabs=azure-portal#grant-access-to-trusted-azure-services) through your firewall configuration. It enables only trusted Azure platform services to access the storage account. With it, [Managed Identities](/previous-versions/azure/media-services/latest/concept-managed-identities) allow Video Indexer to access the storage account.

Use the following information to enable managed identity for Azure Storage and then lock your storage account. It assumes that you already created a Video Indexer account and associated the storage account.

## Assign the managed identity and role

Follow all of the steps for [creating an Azure AI Video Indexer account](/azure/azure-video-indexer/create-account?tabs=portal), but also use the following steps:

1. When you select **Assign Role**, the `Azure Storage : Storage Blob Data Owner` role is assigned. You can verify or manually set assignments by navigating to the **Identity** menu of your Video Indexer account and selecting **Azure Role Assignments**.
1. Navigate to your Storage account. Select **Networking** from the menu and select **Enabled from selected virtual networks and IP addresses** in the **Public network access** section.
1. Under **Exceptions**, make sure that **Allow Azure services on the trusted services list to access this storage account** is selected.

## Upload videos from a firewall-protected storage account

After you complete the setup steps in [Assign the managed identity and role](#assign-the-managed-identity-and-role), Video Indexer can access your firewall-protected storage account as a trusted Azure service. However, you must also tell Video Indexer to use that trusted access when you upload a video by URL.

To upload a video from a firewall-protected storage account, set `useManagedIdentityToDownloadVideo=true` as a query parameter on your [Upload Video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video) API request:

```http
POST https://api.videoindexer.ai/{location}/Accounts/{accountId}/Videos?name={videoName}&videoUrl={videoUrl}&useManagedIdentityToDownloadVideo=true
```

This parameter tells Video Indexer to authenticate to the source storage account by using its managed identity instead of attempting anonymous access. It applies only when you upload a video by URL from a storage account that is behind a firewall. You don't need to set it when you upload files directly from your local machine.

## Related content

- [Upload Video API reference](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video)
- [Azure AI Video Indexer documentation](index.yml)