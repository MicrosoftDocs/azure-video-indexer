---
title: Configure failover for disaster recovery for Azure AI Video Indexer
description: Learn how to configure failover for Azure AI Video Indexer and maintain app availability during outages. Get started today.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/09/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
#customer intent: As an Azure user, I want to know how to configure failover and disaster recovery for Azure AI Video Indexer so that I can ensure optimal availability for my applications.
---

# Configure failover for disaster recovery

Azure AI Video Indexer doesn't provide instant failover of the service if there's a regional datacenter outage or failure. This article explains how to configure your environment for a failover to ensure optimal availability for apps and minimized recovery time if a disaster occurs.

We recommend that you configure business continuity disaster recovery (BCDR) across regional pairs to benefit from Azure's isolation and availability policies. For more information, see [Azure paired regions](/azure/availability-zones/cross-region-replication-azure).

## Fail over to a secondary account

To implement BCDR, you need to have two Azure AI Video Indexer accounts to handle redundancy.

1. Create two Azure AI Video Indexer accounts connected to Azure (see [Create an Azure AI Video Indexer account](connect-to-azure.md)). Create one account for your primary region and the other to the paired Azure region.
1. If there's a failure in your primary region, switch to indexing using the secondary account.

> [!TIP]
> You can automate BCDR by setting up activity log alerts for service health notifications as per [Create activity log alerts on service notifications](/azure/service-health/alerts-activity-log-service-notifications-portal).

For information about using multiple tenants, see [Manage multiple tenants](manage-multiple-tenants.md). To implement BCDR, choose one of these two options: [Azure AI Video Indexer account per tenant](./manage-multiple-tenants.md#azure-ai-video-indexer-account-per-tenant) or [Azure subscription per tenant](./manage-multiple-tenants.md#azure-subscription-per-tenant).

## Related content

- [Azure AI Video Indexer documentation](index.yml)