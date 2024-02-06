---
title: Import your content from the trial account
description: Learn how to import your content from the trial account.
ms.topic: tutorial
ms.date: 02/05/2024
ms.custom: ignite-fall-2021
ms.author: itnorman
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Import content from your trial account to a regular account

[!INCLUDE [AMS AVI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

There's no cost to move your content from an Azure AI Video Indexer trial account to a paid account.

When might you want to switch from a trial to a regular account?

* You used up the free trial minutes and want to continue indexing.
* You're ready to start using Video Indexer for production workloads.
* You want an experience that doesn't have minute, support, or SLA limitations. 

## Create a new Azure Resource Manager (ARM) based account for the import

- Create an ARM-based account. The account must be created and available before performing the import. Account creation can be performed through the Azure portal (see [Create an account](create-account.md)) or API (see [Create accounts with API](/rest/api/videoindexer/stable/accounts)).  
- The ARM-based account must be an empty account that hasn't been used to index any media files.

> [!NOTE]
> Importing from the trial account can be performed only once per trial account.

## Import your data

To import your data, follow the steps:

 1. Go to the [Azure AI Video Indexer website](https://aka.ms/vi-portal-link)
 1. Select your trial account and go to the **Account settings** page.
 1. Select the **Import content to an ARM-based account**.
 1. From the dropdown menu, choose the ARM-based account.
 1. Select **Import content**

All media and your customized content model are copied from the trial account into the new ARM-based account.
