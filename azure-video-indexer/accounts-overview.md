---
title:  Azure AI Video Indexer accounts  
description: This article gives an overview of Azure AI Video Indexer accounts.
ms.topic: conceptual
ms.date: 07/25/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Azure AI Video Indexer account types

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-abbreviated.md)]

This article gives an overview of Azure AI Video Indexer accounts types.

## Trial account

[!INCLUDE [trial-account](includes/trial-account.md)]

## Paid account

Azure AI Video Indexer paid accounts are Azure Resource Manager (ARM) based and unlike trial accounts, are created with your Azure subscription. ARM-based accounts give you access to security and management capabilities, such as [Role Based Access Control (RBAC) user management](/azure/role-based-access-control/overview), [Azure Monitor integration](/azure/azure-monitor/overview), deployment through ARM templates, and more.

A paid account that doesn't have minute, support, or SLA limitations. Accounts can be created with the Azure portal <!--(see [Create an account with the Azure portal](create-account-portal.md)) or API (see [Create accounts with API](/rest/api/videoindexer/stable/accounts)).-->

For more information about pricing, see [Azure AI Video Indexer pricing](https://azure.microsoft.com/pricing/details/video-indexer/).  
   
 ## Classic accounts
 
Before ARM based accounts were added to Azure AI Video Indexer, there was a "classic" account type. The classic account type is still used by some users. Azure AI Video Indexer requires all new accounts to be ARM-based accounts.  If you currently have a classic account, see the [migration guide](./retirement/azure-video-indexer-azure-media-services-retirement-announcement.md).
 
<!--s
For more information on the difference between paid accounts and classic accounts, see [Azure AI Video Indexer as an Azure resource](https://techcommunity.microsoft.com/t5/ai-applied-ai-blog/azure-video-indexer-is-now-available-as-an-azure-resource/ba-p/2912422). -->

## Limited access features

[!INCLUDE [limited access](./includes/limited-access-account-types.md)]

For more information, see [Azure AI Video Indexer limited access features](limited-access-features.md).

## Create an account

To create an account, see [Create an Azure AI Video Indexer account](create-account.md)
