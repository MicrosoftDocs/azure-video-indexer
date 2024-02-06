---
title: Create an Azure AI Video Indexer account
description: This article explains how to create an account for Azure AI Video Indexer.
ms.topic: how-to
ms.date: 02/05/2025
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---
 
# Create an Azure AI Video Indexer (AVI) account

[!INCLUDE [AMS AVI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

[!INCLUDE [Gate notice](./includes/face-limited-access.md)]

To start using Azure AI Video Indexer, create an Azure AI Video Indexer account. 

This article walks you through the steps of creating the Azure AI Video Indexer account and its accompanying resources. The account that gets created is ARM (Azure Resource Manager) account. For information about different account types, see [Overview of account types](accounts-overview.md).

## Trial account

[!INCLUDE [trial-account](includes/trial-account.md)]

The trial account option isn't available on the Azure Government cloud. For other Azure Government limitations, see [Limitations of Azure AI Video Indexer on Azure Government](connect-to-azure.md#limitations-of-azure-ai-video-indexer-on-azure-government).

## Classic account

Classic accounts are being deprecated. It isn't recommended to create a new classic account.

If you currently have a classic account, see the [migration guide](azure-video-indexer-ams-retirement-guide.md).

## Paid account

### Prerequisites

- An Azure subscription.
* An **Owner** role, or both **Contributor** and **User Access Administrator** roles. For more information, see [View the access a user has to Azure resources](/azure/role-based-access-control/check-access).

### [Azure portal](#tab/portal)


### [API](#tab/api)
[Create accounts with API](/rest/api/videoindexer/stable/accounts)

## Government account

Government accounts have special requirements and limitations. 

- Only paid accounts are available on Azure Government.
- No manual content moderation available in Azure Government. In the public cloud, when content is deemed offensive based on a content moderation, the customer can ask for a human to look at that content and potentially revert that decision.
- In Azure Government we won't present a Bing description of celebrities and named entities identified. This is a UI capability only.

### Prerequisites for connecting to Azure Government

- An Azure subscription in [Azure Government](/azure/azure-government/).
- An Entra ID account in Azure Government.
- Prerequisites for permissions and resources as described above in the [Paid account](#paid-account) section.

### Create new account via the Azure Government portal

To create a paid account in Azure Government, follow the instructions in [Create-Paid-Account](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Paid-Account). This API end point only includes Government cloud regions.

If you don't have any Azure AI Video Indexer accounts in Azure Government where you're an owner or a contributor, you'll get an empty experience from which you can start creating your account.

If you are already a contributor or an administrator of a existing Azure AI Video Indexer accounts in Azure Government, you're taken to that account and from there you can use the steps described in the [Paid account](#paid-account) section.
