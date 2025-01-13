---
title: Private endpoints with Azure AI Video Indexer
description: This article is an overview of using private endpoints with Azure AI Video Indexer.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.collection: ce-skilling-ai-copilot
ms.date: 11/07/2024
ms.service: azure-video-indexer
ms.topic: article
---

# Private endpoints with Azure AI Video Indexer (preview)

This article is an overview of using private endpoints with Azure AI Video Indexer.

> [!IMPORTANT]
> This feature is currently in preview. Sign up to request access to try this feature by filling out [this form](https://aka.ms/vi-enable-private-endpoint).

> [!NOTE]
> This article is an abbreviated vesion of the concepts in [Use private endpoints with Azure Storage](/azure/storage/common/storage-private-endpoints), but is adjusted for use with Azure AI Video Indexer. For a complete understanding of private endpoints and private links, see [What is a private endpoint?](/azure/private-link/private-endpoint-overview).

## Use cases

You can use private endpoints for your Azure AI Video Indexer accounts to allow clients on a virtual network to securely access data over a Private Link. The private endpoint uses a separate IP address from the virtual network address space for each Azure AI Video Indexer account. Network traffic between the clients on the virtual network and the Azure AI Video Indexer account traverses over the virtual network and a private link on the Microsoft backbone network, eliminating exposure from the public internet.

Using private endpoints for your Azure AI Video Indexer account enables you to:

- Secure your Azure AI Video Indexer account by configuring the video indexer firewall to block all connections on the public endpoint for the storage service.
- Increase security for the virtual network, by enabling you to block exfiltration of data from the virtual network.
- Securely connect to Azure AI Video Indexer accounts from on-premises networks that connect to the virtual network using [VPN](/azure/vpn-gateway/vpn-gateway-about-vpngateways) or [ExpressRoutes](/azure/expressroute/expressroute-locations) with private-peering.

## Conceptual overview

A private endpoint is a special network interface for an Azure service in your virtual network. When you create a private endpoint for your Video Indexer account, it provides secure connectivity between clients on your virtual network and your Video Indexer instance. The private endpoint is assigned an IP address from the IP address range of your virtual network. The connection between the private endpoint and the Azure AI Video Indexer service uses a secure private link.

Applications in the virtual network can connect to the Azure AI Video Indexer service over the private endpoint seamlessly, using the FQDN of their Azure AI Video Indexer instance. 

Private endpoints can be created in subnets that use [Service Endpoints](/azure/virtual-network/virtual-network-service-endpoints-overview). Clients in a subnet can thus connect to one Azure AI Video Indexer account using private endpoint, while using service endpoints to access others.

When you create a private endpoint for an Azure AI Video Indexer account in your virtual network, a consent request is sent for approval to the Azure AI Video Indexer account owner. If the user requesting the creation of the private endpoint is also an owner of the Azure AI Video Indexer account, this consent request is automatically approved.

:::image type="content" source="media/common/private-link-with-azure-video-indexer-diagram.png" alt-text="private endpoint diagram":::

Azure AI Video Indexer account owners can manage consent requests and the private endpoints through the 'Private endpoints' tab for the Video Indexer account in the Azure portal.

## Creating a private endpoint

To understand more about creating a private endpoint in general, see [Create a private endpoint in the Azure portal](/azure/private-link/create-private-endpoint-portal?tabs=dynamic-ip).

## Try private endpoints with Azure AI Video Indexer

To try private endpoints with your Azure AI Video Indexer account, see [How to use Private Endpoints with Azure AI Video Indexer](private-endpoint-how-to.md). However, you must fill out [this form](https://aka.ms/vi-enable-private-endpoint) before attempting to use private endpoints.
