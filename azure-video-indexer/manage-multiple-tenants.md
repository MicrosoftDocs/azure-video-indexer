---
title: Manage multiple tenants with Azure AI Video Indexer
description: Learn about integration options for managing multiple tenants with Azure AI Video Indexer, including account and subscription strategies.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.custom: ikbarmen
ms.date: 08/18/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: concept-article
## customer intent: As a developer or administrator, I want to understand the different options for managing multiple tenants with Azure AI Video Indexer, so that I can choose the best integration strategy for my application.
---

# Manage multiple tenants

This article discusses different options for managing multiple tenants with Azure AI Video Indexer. Choose a method that is most suitable for your scenario:

* Azure AI Video Indexer account per tenant
* Single Azure AI Video Indexer account for all tenants
* Azure subscription per tenant

## Azure AI Video Indexer account per tenant

An Azure AI Video Indexer account is created for each tenant. The tenants have full isolation in the persistent and compute layer.  

:::image type="content" source="./media/manage-multiple-tenants/video-indexer-account-per-tenant.png" border="false" alt-text="Diagram showing the relationship between an Azure AI Video Indexer account, resources, and a shared Azure subscription." lightbox="./media/manage-multiple-tenants/video-indexer-account-per-tenant.png" :::

### Considerations

* Customers don't share storage accounts (unless manually configured by the customer).
* Customers don't share compute (reserved units) and don't affect processing jobs times of one another.
* You can easily remove a tenant from the system by deleting the Azure AI Video Indexer account.
* There's no ability to share custom models between tenants.
    * Check that there's no business requirement to share custom models.
* Harder to manage due to multiple Azure AI Video Indexer accounts per tenant.

> [!TIP]
> Create an admin user for your system in [the Azure AI Video Indexer developer portal](https://api-portal.videoindexer.ai/) and use the Authorization API to provide your tenants the relevant [account access token](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Account-Access-Token).

## Single Azure AI Video Indexer account for all users

The customer is responsible for tenants isolation when using a single VI account for all users. All tenants have to use a single Azure AI Video Indexer account. The customer needs to filter the proper results for that tenant when uploading, searching, or deleting content.

:::image type="content" source="./media/manage-multiple-tenants/single-video-indexer-account-for-all-users.png" border="true" alt-text="Diagram showing the relationship between all users in tenants, an Azure Video Indexer account, and a single resource group in one subscription." lightbox="./media/manage-multiple-tenants/single-video-indexer-account-for-all-users.png" :::

With this option, customization models (Person, Language, and Brands) can be shared or isolated between tenants by filtering the models by tenant.

When [uploading videos](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video), you can specify a different partition attribute per tenant which allows isolation in the [search API](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Search-Videos). By specifying the partition attribute in the search API, you only get results of the specified partition. 

### Considerations

* Ability to share content and customization models between tenants.
* One tenant impacts the performance of other tenants.
* Customer needs to build a complex management layer on top of Azure AI Video Indexer.

> [!TIP]
> You can use the priority attribute to prioritize tenants jobs.

## Azure subscription per tenant 

Each tenant has their own Azure subscription when using an Azure subscription per tenant. For each user, you create a new Azure AI Video Indexer account in the tenant subscription.

:::image type="content" source="./media/manage-multiple-tenants/azure-subscription-per-tenant.png" border="true" alt-text="Diagram showing the relationship between tenants where each user has their own Azure Video Indexer account and their own Azure subscription." lightbox="./media/manage-multiple-tenants/azure-subscription-per-tenant.png" :::

### Considerations

* This configuration is the only option that enables billing separation.
* This integration has more management overhead than Azure AI Video Indexer account per tenant. If billing isn't a requirement, we recommended that you use one of the other options described in this article.

## Related content

* [Create an Azure AI Video Indexer account](create-account.md)
* [Azure AI Video Indexer documentation](index.yml)