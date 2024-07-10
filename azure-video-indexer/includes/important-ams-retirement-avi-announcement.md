---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/10/2024
ms.author: inhenkel
title: AMS VI retirement announcement
---

> [!WARNING]
> Over the past year, Azure AI Video Indexer (VI) announced the removal of its dependency on Azure Media Services (AMS) due to its [retirement](https://aka.ms/ams-retirement). [Features adjustments](https://azure.microsoft.com/updates/videoindexer-2/) and [changes](/azure/azure-video-indexer/azure-video-indexer-azure-media-services-retirement-announcement) were announced and a [migration guide](../azure-video-indexer-ams-retirement-guide.md) was provided.<br/><br/>
> The deadline to complete migration was June 30, 2024. VI has extended the update/migrate deadline so you can update your VI account and opt in to the AMS VI asset migration through July 15th, 2024. To use the AMS VI asset migration, you also must extend your AMS account through July. This can be done by going to your AMS account in the Azure portal and selecting **Click here to extend.**<br/><br/>
> However, after June 30, if you have **not** updated your VI account, you **won't be able to index new videos nor will you be able to play any videos** that have not been migrated. If you update your account after June 30, you can resume indexing immediately but you **won't be able to play videos indexed before the account update until they are migrated through the AMS VI migration**.