---
title: Private endpoints with Azure AI Video Indexer
description: This article provides an overview of using private endpoints with Azure AI Video Indexer to ensure secure and private connectivity in your virtual network.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/03/2025
ms.service: azure-video-indexer
ms.topic: concept-article
#customer intent: As a network administrator, I want to understand and implement private endpoints for Azure AI Video Indexer to ensure secure and private connectivity within my virtual network.
---

# Private endpoints with Azure AI Video Indexer

This article provides an overview of using private endpoints with Azure AI Video Indexer to ensure secure and private connectivity in your virtual network.

> [!NOTE]
> For a complete understanding of private endpoints and private links, see [What is a private endpoint?](/azure/private-link/private-endpoint-overview).

## Use cases

You can use private endpoints for your Azure AI Video Indexer accounts to allow clients on a virtual network to securely access data over a Private Link. The private endpoint uses an IP address from the virtual network address space to access the client's Azure AI Video Indexer account. Network traffic between the clients on the virtual network and the Azure AI Video Indexer account traverses over the virtual network and a private link on the Microsoft backbone network, eliminating exposure from the public internet.

Using private endpoints for your Azure AI Video Indexer account enables you to:

- Secure your Azure AI Video Indexer account by using a private link. You can manually configure the video indexer firewall to block all connections to the Video Indexer account coming from the public Video Indexer endpoint.
- Securely connect to Azure AI Video Indexer accounts from on-premises networks that connect to the virtual network using [VPN](/azure/vpn-gateway/vpn-gateway-about-vpngateways) or [ExpressRoutes](/azure/expressroute/expressroute-locations) with private peering.

> [!IMPORTANT]
> - Private endpoints support operations that use the Video Indexer API. If you disable public access for your Video Indexer account, you can't use the account through the [Video Indexer web app](https://www.videoindexer.ai/).
> - Video Indexer accounts connect to an Azure Storage account. To learn how to set up your Video Indexer account to connect to a storage account behind a firewall using trusted storage, see [Configure Video Indexer to work with storage accounts behind firewall](../storage-behind-firewall.md).

## Conceptual overview

A private endpoint is a special network interface for an Azure service in your virtual network. When you create a private endpoint for your Video Indexer account, it provides secure connectivity between clients on your virtual network and your Video Indexer instance. The private endpoint is assigned an IP address from the IP address range of your virtual network. The connection between the private endpoint and the Azure AI Video Indexer service uses a secure private link.

Applications in the virtual network can connect to the Azure AI Video Indexer service over the private endpoint seamlessly. They can make requests with the Video Indexer REST API, using the fully qualified domain name (FQDN) of their Azure AI Video Indexer instance. The connection uses the same authorization.

When you create a private endpoint for an Azure AI Video Indexer account in your virtual network, a consent request is sent for approval to the Azure AI Video Indexer account owner. If the user requesting the creation of the private endpoint is also an owner of the Azure AI Video Indexer account, this consent request is automatically approved.

Azure AI Video Indexer account owners can manage consent requests and the private endpoints through the **Private endpoints** tab for the Video Indexer account in the Azure portal.

## DNS changes for private endpoints

>[!NOTE]
> For details about how to configure your DNS settings for private endpoints, see [Azure Private Endpoint DNS integration](/azure/private-link/private-endpoint-dns-integration).

When you create a private endpoint, two DNS CNAME records for the Video Indexer account are created, `<account name>.api.videoindexer.ai` and `<account name>.privatelink.api.videoindexer.ai`.

By default, we also create a [private DNS zone](/azure/dns/private-dns-overview) that corresponds to the private link subdomain `privatelink.api.videoindexer.ai`. The DNS record `<account name>.privatelink.api.videoindexer.ai` maps to the private endpoint IP address.

When you make a REST request to the FQDN endpoint URL from outside the virtual network with the private endpoint, the FQDN is resolved to the public endpoint of Video Indexer (`api.videoindexer.ai`). 

When the virtual network hosting the private endpoint resolves it, it resolves to the private endpoint's IP address.

For example, the DNS resource record for the Video Indexer account `VIAccountA`, when resolved from *outside* the virtual network hosting the private endpoint, would be:

| Name | Type | Value |
| ---- | ---- | ----- |
| `VIAccountA.api.videoindexer.ai` | CNAME | `VIAccountA.privatelink.api.videoindexer.ai`|
| `VIAccountA.privatelink.api.videoindexer.ai` | CNAME | <`Video Indexer public endpoint`> |
 
As previously mentioned, you can deny or control access for clients outside the virtual network through the public endpoint using the Video Indexer firewall.

The DNS resource records for `VIAccountA`, when resolved by a client in the virtual network hosting, the private endpoint, would be:

| Name | Type | Value |
| ---- | ---- | ----- |
| `VIAccountA.api.videoindexer.ai`| CNAME |	`VIAccountA.privatelink.api.videoindexer.ai` |
| `VIAccountA.privatelink.api.videoindexer.ai`	| A | 10.1.1.5 |
 
This approach enables access to the Video Indexer account using the same access token for clients on the virtual network hosting the private endpoints, and clients outside the virtual network.

If you're using a custom DNS server on your network, clients must be able to resolve the FQDN for the Video Indexer account endpoint to the private endpoint IP address. You should configure your DNS server to delegate your private link subdomain to the private DNS zone for the virtual network, or configure the A records for `VIAccountA.privatelink.api.videoindexer.ai` with the private endpoint IP address.

## Create a private endpoint

To understand more about creating a private endpoint in general, see [Create a private endpoint in the Azure portal](/azure/private-link/create-private-endpoint-portal?tabs=dynamic-ip).

## Try private endpoints with Azure AI Video Indexer

To try private endpoints with your Azure AI Video Indexer account, see [How to use Private Endpoints with Azure AI Video Indexer](private-endpoint-how-to.md).