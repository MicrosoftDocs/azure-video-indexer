---
title:  Azure AI Video Indexer accounts
description: Learn about the different types of Azure AI Video Indexer accounts, including trial accounts, paid ARM-based accounts, and deprecated classic accounts.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/09/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: concept-article
#customer intent: As a user of Azure AI Video Indexer, I want to understand the different types of accounts available, including trial and paid accounts, so that I can choose the right one for my needs.
---

# Azure AI Video Indexer account types overview

Azure AI Video Indexer provides different types of accounts to suit various user needs, including trial accounts for testing and paid accounts for production use.

## Trial account

Try a free trial Azure AI Video Indexer account with your content. You don't need an Azure subscription. The account provides up to 2,400 minutes of free indexing using the [Azure AI Video Indexer](https://www.videoindexer.ai/) website or the Azure AI Video Indexer API (see the [developer portal](https://api-portal.videoindexer.ai/)).

> [!NOTE]
> If you don't use your trial account for 12 months, it can be deleted. To keep your account, sign in at least once every 12 months.

## Azure AI Video Indexer account

Azure AI Video Indexer paid accounts are Azure Resource Manager (ARM) based and unlike trial accounts, are created with your Azure subscription. ARM-based accounts give you access to security and management capabilities, such as [Role Based Access Control (RBAC) user management](/azure/role-based-access-control/overview), [Azure Monitor integration](/azure/azure-monitor/overview), deployment through ARM templates, and more.

A paid account that doesn't have minute, support, or service level agreement (SLA) limitations. Accounts can be created with the Azure portal. <!--(see [Create an account with the Azure portal](create-account-portal.md)) or API (see [Create accounts with API](/rest/api/videoindexer/stable/accounts)).-->

For more information about pricing, see [Azure AI Video Indexer pricing](https://azure.microsoft.com/pricing/details/video-indexer/).

## Classic accounts are deprecated

You can't create a classic account. Classic accounts retired on June 30, 2024.

## Limited access features

This section covers limited access features in Azure AI Video Indexer.

|When did I create the account?|Trial account (free)|	Paid account <br/>(classic or ARM-based)|
|---|---|---|
|Existing VI accounts <br/><br/>created before June 21, 2022|You could use face identification, customization, and celebrity recognition until June 2023. <br/><br/>**Recommended**: Move to a paid account then complete the [intake form](https://aka.ms/facerecognition). If you meet the eligibility criteria, Azure AI Video Indexer enables the features also after the grace period. |You could access face identification, customization, and celebrity recognition until June 2023 ¹.<br/><br/>**Recommended**: Complete the [intake form](https://aka.ms/facerecognition). If you meet eligibility criteria, Azure AI Video Indexer enables the features also after the grace period.|
|New VI accounts <br/><br/>created after June 21, 2022	| You can't use face identification, customization, and celebrity recognition right now. <br/><br/>**Recommended**: Move to a paid account then complete the [intake form](https://aka.ms/facerecognition). If you meet the eligibility criteria, Azure AI Video Indexer enables the features (within 10 days).|Azure AI Video Indexer disables the access to face identification, customization, and celebrity recognition today by default, but gives the option to enable it. <br/><br/>**Recommended**: Complete the [intake form](https://aka.ms/facerecognition). If you meet the eligibility criteria, Azure AI Video Indexer enables the features (within 10 days).|

¹ In Brazil South, face detection isn't available.

For more information, see [Azure AI Video Indexer limited access features](limited-access-features.md).

## Create an account

To create an account, see [Create an Azure AI Video Indexer account](create-account.md).

## Related content

- [Create an Azure AI Video Indexer account](create-account.md)