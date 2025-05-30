---
title:  Azure AI Video Indexer accounts  
description: This article provides an overview of Azure AI Video Indexer accounts, including trial, paid, and deprecated classic accounts.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 05/28/2025
ms.service: azure-video-indexer
ms.topic: conceptual
---

# Azure AI Video Indexer account types

This article gives an overview of Azure AI Video Indexer accounts types.

## Trial account

[!INCLUDE [trial-account](includes/trial-account.md)]

## Azure AI Video Indexer account

Azure AI Video Indexer paid accounts are Azure Resource Manager (ARM) based and unlike trial accounts, are created with your Azure subscription. ARM-based accounts give you access to security and management capabilities, such as [Role Based Access Control (RBAC) user management](/azure/role-based-access-control/overview), [Azure Monitor integration](/azure/azure-monitor/overview), deployment through ARM templates, and more.

A paid account that doesn't have minute, support, or SLA limitations. Accounts can be created with the Azure portal. <!--(see [Create an account with the Azure portal](create-account-portal.md)) or API (see [Create accounts with API](/rest/api/videoindexer/stable/accounts)).-->

For more information about pricing, see [Azure AI Video Indexer pricing](https://azure.microsoft.com/pricing/details/video-indexer/).  
   
## Classic accounts are deprecated

You can't create a classic account. Classic accounts retired on June 30, 2024. 
 
## Limited access features

[!INCLUDE [limited access](./includes/limited-access-account-types.md)]

For more information, see [Azure AI Video Indexer limited access features](limited-access-features.md).

## Create an account

To create an account, see [Create an Azure AI Video Indexer account](create-account.md).
