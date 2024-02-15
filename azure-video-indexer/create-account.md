---
title: Create an Azure AI Video Indexer account
description: This article explains how to create an account for Azure AI Video Indexer.
ms.topic: how-to
ms.date: 02/15/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---
 
# Create an Azure AI Video Indexer (AVI) account

[!INCLUDE [AMS AVI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

[!INCLUDE [Gate notice](./includes/face-limited-access.md)]

To start using Azure AI Video Indexer, create an Azure AI Video Indexer account. 

This article walks you through the steps of creating the Azure AI Video Indexer account and its accompanying resources. The account that gets created is Azure Resource Manager (ARM) account. For information about different account types, see [Overview of account types](accounts-overview.md).

## Trial account

[!INCLUDE [trial-account](includes/trial-account.md)]

The trial account option isn't available on the Azure Government cloud. For other Azure Government limitations, see [Limitations of Azure AI Video Indexer on Azure Government](connect-to-azure.md#limitations-of-azure-ai-video-indexer-on-azure-government).

## Classic account

You can no longer create a classic account.

Classic accounts will be retired on June 30th, 2024. If you currently have a classic account, see the [migration guide](azure-video-indexer-ams-retirement-guide.md).

## Paid account

### Prerequisites

- An Azure subscription
- At the subscription level, either the **Owner** role, or both **Contributor** and **User Access Administrator** roles

For more information, see [View the access a user has to Azure resources](/azure/role-based-access-control/check-access).

### [Azure portal](#tab/portal)

1.  In the Azure portal, select **+ Create a resource.**
1.  Search for and select *Azure AI Video Indexer.* The Create a Video Indexer resource page appears.
1.  Create a resource group and selecting the region.
1.  Give the account a name in the **Resource name** field.
1.  Connect the account to storage. Either…
    1.  Select an existing storage account from the **Storage account** dropdown or
    1.  Create a new storage account. For more information about creating a storage account, see [Create a storage account](/azure/storage/common/storage-account-create?tabs=azure-portal).
1.  Select or create a **user assigned managed identity**. (If you forget, a prompt in the storage overview page appears later in the process.)
1.  Select **Review + create**. Validation of the configuration starts.
1.  When validation is complete, select **Create**.
1.  When the deployment is complete, select **Go to resource**. The storage resource overview page appears.
1.  If you assigned a system assigned managed identity during the storage creation process, a notification on the page says that you must select a managed identity role assignment. Select the **Assign role** button.

### [API](#tab/api)
[Create accounts with API](/rest/api/videoindexer/stable/accounts)

---

## Government account

Government accounts have special requirements and limitations. 

- Only paid accounts are available on Azure Government.
- No manual content moderation available in Azure Government. In the public cloud, when content is deemed offensive based on a content moderation, the customer can ask for a human to look at that content and potentially revert that decision.
- For Azure Government, we don't present a Bing description of celebrities and named entities identified. It's a UI capability only.

### Prerequisites for connecting to Azure Government

- An Azure subscription in [Azure Government](/azure/azure-government/).
- A Microsoft Entra ID account in Azure Government.
- Prerequisites for permissions and resources as described in the [Paid account](#paid-account) section.

### Create new account via the Azure Government portal

To create a paid account in Azure Government, follow the instructions in [Create-Paid-Account](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Paid-Account). This API end point only includes Government cloud regions.

If you aren't an Owner or Contributor for any Azure AI Video Indexer accounts in Azure Government, you're'given an empty experience from which you can start creating your account.

If you're already a contributor or an administrator of an existing Azure AI Video Indexer account in Azure Government, you're taken to that account and from there you can use the steps described in the [Paid account](#paid-account) section.
