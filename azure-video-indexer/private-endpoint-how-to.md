---
title: How to use private endpoints with Azure AI Video Indexer
description: Learn how to configure private endpoints for Azure AI Video Indexer to ensure secure and private connectivity within your virtual network.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 05/30/2025
ms.service: azure-video-indexer
ms.topic: how-to
#customer intent: As a network administrator, I want to configure private endpoints for Azure AI Video Indexer to ensure secure and private connectivity within my virtual network.
---

# How to use private endpoints with Azure AI Video Indexer

This article shows you how to use private endpoints with Azure AI Video Indexer using the Azure portal. For an overview, see the [use cases for private endpoints with Azure AI Video Indexer](private-endpoint-overview.md).

Private endpoints are supported in all public regions supported by Azure AI Video Indexer. They aren't supported in sovereign cloud regions, such as Microsoft Azure operated by 21Vianet (Azure in China) and Azure for US Government.

## Prerequisites

- A [virtual network and a subnet](/azure/virtual-network/quick-create-portal).

[!INCLUDE [important-private-endpoint-storage-portal](includes/important-private-endpoint-storage-portal.md)]

## Enable the private endpoint on the Azure AI Video Indexer account

When you [create the Azure AI Video Indexer account](create-account.md), networking might not be configured. This situation is normal. You can configure networking after the account is created:

1. Sign in to the [Azure portal](https://portal.azure.com).
1. Navigate to the Azure AI Video Indexer account you want to work with and select **Settings**, then **Networking**. The Public access screen appears.
1. Once you have access, select the **Disable** radio button.
1. Select **+ Create a private endpoint**. The Create private endpoint screen appears.
1. Select the subscription you want to work with.
1. Select the resource group you want to work with or create a new one.
1. Enter a name for the endpoint in the **Name** field.
1. Select the virtual network and the subnet from the dropdowns.
1. Select the private DNS integration checkbox. The fields autopopulate by the selections you chose earlier.
1. Select **Add**.
1. Select **Review + create**.
1. Wait for the validation.
1. Select **Create**.
    1. If you're creating the private endpoint at the same time you're creating an Azure AI Video Indexer account, wait for another validation.
    1. Select **Create** again.
1. Wait for the deployment.
