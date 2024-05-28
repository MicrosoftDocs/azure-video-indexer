---
title: Use Video Indexer with storage behind firewall
description: This article gives an overview how to configure Azure AI Video Indexer to use storage behind firewall.
ms.topic: article
ms.date: 05/28/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Configure Video Indexer to work with storage accounts behind firewall

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

When you create a Video Indexer account, you must associate it with an Azure Storage account. Video Indexer can access the storage account using system authentication or Managed Identity authentication. Video Indexer validates that the user adding the association has access to the storage account with Azure Resource Manager Role Based Access Control (RBAC).

If you want to use a firewall to secure your storage account and enable trusted storage, [Managed Identities](/azure/media-services/latest/concept-managed-identities) authentication that allows Video Indexer access through the firewall is the preferred option. It allows Video Indexer to access the storage account that has been configured without needing public access for [trusted storage access.](/azure/storage/common/storage-network-security?tabs=azure-portal#grant-access-to-trusted-azure-services)

> [!IMPORTANT]
> It's important to understand the implications if you lock your storage accounts without public access, especially in relation to the Video Indexer portal. The source IP of the client device is pivotal in this scenario. If the storage account is locked and does not have an exception for the source IP, access to the SAS URL for the video source file will be denied. This applies to both downloading and streaming video content.

> To ensure seamless access, we recommend that you work closely with your network/storage administrator to accommodate these requirements. Utilize your corporate network, a VPN, or Azure Private Link to provide the necessary connectivity while you maintain the security posture of your storage accounts.

> For instance, Azure Private Link provides a secure way to access Azure services privately from your virtual network. It simplifies the network architecture and secures the connection between endpoints in Azure by eliminating data exposure to the public internet.

> Any changes to network configurations should be carefully planned and tested to avoid disrupting access to essential services and resources.

Follow these steps to enable Managed Identity for Storage and then lock your storage account. It's assumed that you already created a Video Indexer account and associated the Storage account.

## Assign the Managed Identity and role

Follow all of the steps for [creating an Azure AI Video Indexer account](/azure/azure-video-indexer/create-account?tabs=portal), but also use the steps below:

1. When you select **Assign Role**, the following roles are assigned: `Azure Media Services : Contributor` and `Azure Storage : Storage Blob Data Owner`. You can verify or manually set assignments by navigating to the **Identity** menu of your Video Indexer account and selecting **Azure Role Assignments**.
1. Navigate to your Storage account. Select **Networking** from the menu and select **Enabled from selected virtual networks and IP addresses** in the **Public network access** section.
1. Under **Exceptions**, make sure that **Allow Azure services on the trusted services list to access this storage account** is selected.

## Upload from locked storage account

When uploading a file to Video Indexer you can provide a link to a video using a SAS locator. If the storage account hosting the video is not publicly accessible, use the Managed Identity and Trusted Service approach. Since there is no way to know if a SAS url is pointing to a locked storage account, explicitly set the query parameter `useManagedIdentityToDownloadVideo` to `true` in the [upload-video API call](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video). 

You also need to set the role `Azure Storage : Storage Blob Data Owner` on this storage account as you did with the storage account.
