---
title: Cost management for Azure AI Video Indexer enabled by Arc
description: Learn about the hybrid billing model for Azure AI Video Indexer enabled by Arc and estimate your total cost of ownership before deploying.
author: cwatson-cat
ms.author: cwatson
ms.date: 07/14/2026
ms.service: azure-video-indexer
ms.topic: concept-article
appliesto:
  - Azure AI Video Indexer enabled by Azure Arc
ai-usage: ai-assisted
#customer intent:  As a solution owner, I want to understand the cost structure of Azure AI Video Indexer enabled by Arc (free extension + paid infrastructure) so that I can estimate my total cost of ownership before deploying.
---

# Cost management for Azure AI Video Indexer enabled by Arc

Azure AI Video Indexer enabled by Arc uses a hybrid billing model: the extension itself is free, but you pay for the infrastructure and Azure services that host and support it. Understanding this cost structure is essential for planning your total cost of ownership before deploying at the edge.

This article breaks down the free and paid components of your deployment so you can estimate costs accurately. Check the [Azure AI Video Indexer pricing page](https://azure.microsoft.com/pricing/details/video-indexer/) for the latest cloud service pricing, which doesn't apply to the edge deployment.

## Understand the billing model

Your total cost has two parts:

- **Azure AI Video Indexer enabled by Arc**: Free to use. You're not charged for the extension or for the videos and audio that you index at the edge.
- **Infrastructure and platform services**: You pay for the hardware and Azure services that host and connect the extension.

The extension runs on your Arc-enabled Kubernetes cluster. All media processing happens at the edge, so you don't pay for cloud indexing. Control plane information (such as billing and monitoring data) is sent to the cloud, but no indexed videos or insights leave the edge.

## Costs to plan for

Plan for the following costs when you run Azure AI Video Indexer enabled by Arc.

| Cost | Description | More information |
|--|--|--|
| Hardware | Physical or virtual machines that meet the [minimum hardware requirements](azure-video-indexer-enabled-by-arc-overview.md#minimum-hardware-requirements) for the cluster. | You provide and manage this hardware. |
| Azure Local | If you run the cluster on Azure Local, you'll pay the Azure Local service fee. | [Azure Local billing and payment](/azure/azure-local/concepts/billing) and [Azure Local pricing](https://azure.microsoft.com/pricing/details/azure-local/) |
| Azure Arc | Some Azure Arc control plane capabilities are free; others are billed. | [Azure Arc pricing](https://azure.microsoft.com/pricing/details/azure-arc/core-control-plane/) |
| Other Azure services | Services your solution uses (such as storage or monitoring) are billed at their own rates. | [Azure Monitor pricing](https://azure.microsoft.com/pricing/details/monitor/) |

The [Azure AI Video Indexer pricing page](https://azure.microsoft.com/pricing/details/video-indexer/) covers the cloud service and doesn't apply to Azure AI Video Indexer enabled by Arc, which is free.

## Estimate costs before you deploy

Use the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/) to estimate costs for Azure services that support your deployment, such as Azure Local, Azure Arc, and Azure Monitor. Since the extension is free, your estimate includes only infrastructure and platform services.

## Monitor costs

Monitor supporting Azure resources the same way you'd monitor any other Azure service. In the Azure portal, use [Cost analysis in Cost Management](/azure/cost-management-billing/costs/quick-acm-cost-analysis) to review spend for the resource group that holds your Arc-enabled cluster and related resources. To avoid surprises, [create budgets and cost alerts](/azure/cost-management-billing/costs/tutorial-acm-create-budgets).

## Related content

- [What is Azure AI Video Indexer enabled by Arc?](azure-video-indexer-enabled-by-arc-overview.md)
- [Azure Local billing and payment](/azure/azure-local/concepts/billing)
- [Azure Arc pricing](https://azure.microsoft.com/pricing/details/azure-arc/core-control-plane/)
