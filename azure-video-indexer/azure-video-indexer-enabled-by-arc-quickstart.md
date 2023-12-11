---
title: Tutorial - Azure AI Video Indexer enabled by Arc
description: This tutorial shows you how to deploy Azure Video Indexer with Arc.
ms.topic: quickstart
ms.service: azure-video-indexer
ms.date: 12/11/2023
ms.author: inhenkel
author: IngridAtMicrosoft
---

# Try Azure Video Indexer enabled by Arc

Azure Video Indexer enabled by Arc ([!INCLUDE [variable-edge-product-name](includes/variable-edge-product-name.md)]) is an Azure Arc Extension Enabled Service that runs video and audio analysis on edge devices. The solution is designed to run on Azure Stack Edge profile, a heavy edge device, and supports many video formats, including MP4 and other common formats. The solution supports several languages in all basic audio-related models. It assumes that one Video Indexer resource is mapped to one extension.

This article walks you through the steps for enabling Video Indexer as an Arc extension on your current infrastructure.

## Prerequisites

> [!IMPORTANT]
> To successfully deploy the Azure Video Indexer extension, it is **mandatory** that your Azure subscription id is approved in advance. You must first sign up using [this form](https://aka.ms/vi-register).

- Review the [!INCLUDE [variable-edge-product-name](includes/variable-edge-product-name.md)][ overview](azure-video-indexer-enabled-by-arc-overview.md).
- Set up the following things before you attempt the rest of this tutorial:
    - Create an Azure subscription with permissions to create Azure resources.
    - Create an Azure Video Indexer Account. Use the [Create Video Indexer account](create-account-portal.md) tutorial.
    - Install the latest version of the [Azure CLI](/cli/azure/install-azure-cli). (You can skip this step if you're using Cloud Shell.)
    - **If not using Cloud Shell**, install the latest version of *connectedk8s* Azure CLI extension. Use the following command.
    
        ```bash
        az extension add --name connectedk8s
        ```

> [!IMPORTANT]
> The AKS cluster contains the Video Indexer extension must be in the East US region.

## Minimum hardware requirements

The following list is the minimum and recommended requirements if the extension contains single language support. If you install multiple speech and translation containers with several languages, increase the hardware requirements accordingly.

| Component | Minimum Requirements | Recommended Requirements
| --- | --- | --- |
| VM Count | 1 | 2
| CPU (Per Cluster)| 16 cores | 32 cores | 
| RAM (Per Cluster)| 32 GB | 64 GB |
| Storage | 30 GB | 50 GB |

> [!Note] 
> At least a 2-node cluster is recommended for high availability and scalability. The recommended settings refer to cluster wide settings, so for example, if you have 2 nodes, each node should have 16 cores and 32 GB of RAM.

> [!TIP] 
> We recommend creating a dedicate node-pool / auto-scaling groups to host the VI Solution

### Minimum software requirements

| Component |  Minimum Requirements |
| --- | --- |
| Operating System | Ubuntu 20.04 LTS or any Linux Compatible OS |
| Kubernetes | 1.24 |
| Azure CLI | 2.4.0 |

## Prepare for deployment

During the deployment, the script asks for environment specific values. Have these values ready so you can copy and paste them when the script asks for them. 

| Question | Value | Details
| --- | --- | --- |
| What is the Video Indexer account ID during deployment? | GUID | Your Video Indexer Account ID |
| What is the Azure subscription ID during deployment? | GUID | Your Azure Subscription ID |
| What is the name of the Video Indexer resource group during deployment? | string | The Resource Group Name of your Video Indexer Account |
| What is the name of the Video Indexer account during deployment? | string | Your Video Indexer Account name |

> [!WARNING]
> This sample environment is **NOT** meant to be used in production and only provided to quickly test functionality. Be certain to restrict access to the IP addresses in the environment to prevent security issues.

## Deploy with the Azure Portal

1. In the Azure portal, navigate to your Azure Arc-connected cluster.
1. From the menu, select **Extensions** > **+ Add** > **Azure Video Indexer Arc Extension**.
1. Select **Create**. The *Create an AI Video Indexer extension* screen will appear.
1. Configure the extension in *Instance details*:
    1. Select the **subscription** and **resource group** for your extension.
    1. Select the **region and connected** k8 cluster.
    1. Enter a **name** for your extension.
    1. Select the **Azure Video Indexer Account** that the extension will be connected to.
    1. Enter the **cluster endpoint**, either an IP or DNS Name to be used as the API endpoint.
    1. Provide the **storage class** you want to use for the extension that's supported by your Kubernetes distribution. For example, if you're using AKS, you could use `azurefile-cli`. For more information on predefined storage classes supported by AKS, see [Storage Classes in AKS](/azure/aks/concepts-storage#storage-classes). If you're using other Kubernetes distributions, see your Kubernetes distribution documentation for predefined storage classes supported or the way you can provide your own.
1. Select **Review + create** and then **Create**.

## Next steps

Once you have tried deploying Azure Video Indexer enabled by Arc in the Azure portal, see the either [AVIenabledbyArc on GitHub](https://github.com/Azure-Samples/media-services-video-indexer/blob/master/AVIenabledbyArc/vi-edge-deployment-script.sh) or the [Arc Jumpstart]().
