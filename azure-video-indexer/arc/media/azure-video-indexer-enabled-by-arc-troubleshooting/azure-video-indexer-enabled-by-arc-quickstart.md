---
title: Try Azure AI Video Indexer enabled by Arc
description: This article walks you through the steps required to enable Video Indexer as an Arc extension on your current infrastructure.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: quickstart
#customer intent: As a video content manager, I want to enable Azure AI Video Indexer as an Arc extension in my infrastructure to analyze and index video content on edge devices, ensuring compliance with data governance policies and reducing latency in on-premises workflows.
---

# Try Azure AI Video Indexer enabled by Arc

[Azure AI Video Indexer enabled by Arc](../azure-video-indexer-enabled-by-arc-overview.md) is an Azure Arc extension enabled service that runs video and audio analysis and [generative AI](../generative_ai_with_vi.md) on edge devices. The solution runs on [Azure Arc enabled Kubernetes](/azure/azure-arc/kubernetes/), supports many video formats, and assumes that one Video Indexer resource maps to one extension. It transcribes spoken content in more than 35 source languages and translates them to English. For a full list of supported languages, see [Supported languages per scenario](../language-support.md#supported-languages-per-scenario).

<!-- Para above is duplicated in azure-video-indexer-enabled-by-arc-overview.md so sync any changes-->

This article walks you through the steps required to enable Video Indexer as an Arc extension in your current infrastructure.

<!--
## Possible deployment

Here is a block diagram showing Azure AI Video Indexer running on Azure Arc. There are three types: 

1. Store type A uses both vision and audio presets.
1. Store type B uses only vision presets. It also has a custom model. For more information about using a custom model with Azure AI Video Indexer enabled by Arc, see [Bring Your Own AI model](../azure-video-indexer-bring-your-own-model-overview.md). 
1. Store C uses only audio presets. 

The extension is stored on each edge device and each device is associated with a single AI Video Indexer account that interfaces with Azure Arc and the cloud.

:::image type="content" source="../media/common/vi-arc-diagram-v2.svg" lightbox="../media/common/avi-arc-diagram.svg" alt-text="VI Arc block diagram":::
-->

## Prerequisites

> [!IMPORTANT]
> To successfully deploy the Azure AI Video Indexer extension, it's **mandatory** that your Azure subscription ID is approved in advance. You must first sign up using the form at [Application for gated services](https://aka.ms/vi-register).

- Create an Azure subscription and assign permissions to a user so they can create Azure resources.
- Create an Azure AI Video Indexer account. For more information about creating an account, see the [Create a Video Indexer account](/azure/azure-video-indexer/create-account-portal) tutorial.
- Create an [Arc enabled Kubernetes cluster](/azure/aks/hybrid/aks-create-clusters-portal).

To use the Video Indexer extension, you need to have an externally facing endpoint, which can be either a DNS name or an IP address. The endpoint should be set as a secure transfer protocol (`https:\\`) and is used as the extension API endpoint. It also gets used by the Video Indexer web portal to communicate with the extension. We recommend that you use an ingress control to manage the endpoint.

> [!NOTE]
> If the endpoint isn't publicly accessible, you can perform actions on the extension from the web portal only from the local network.

## Minimum hardware requirements for this quickstart

This quickstart is designed to allow you to see the extension in action. Smaller resource sizes are suggested for you to work with in a *test* environment. For this quickstart, the minimum hardware requirements are:

- CPU: 16 cores
- Memory: 16 GB

The CPU in the nodes should support [AVX2](https://wikipedia.org/wiki/Advanced_Vector_Extensions). Most newer CPUs support the extension, but it might not be supported in some older virtualization environments.

To view minimum hardware requirements in a *production* environment, see the [Minimum hardware requirements](/azure/azure-video-indexer/azure-video-indexer-enabled-by-arc-overview#minimum-hardware-requirements) in the overview article.

## Minimum software requirements

| Component |  Minimum requirements |
| --- | --- |
| Operating system | Ubuntu 22.04 LTS or any Linux Compatible OS |
| Kubernetes | 1.29 |
| Azure CLI | 2.64.0 |

<!-- section duplicated to azure-video-indexer-enabled-by-arc-overview-->

## Parameter definitions

Here's a table of the parameters used to configure the extension.

| Parameter | Description |
| --- |--- |
| release-namespace | The Kubernetes namespace that the extension is installed into |
| cluster-name | The Kubernetes Azure Arc instance name |
| resource-group | The Kubernetes Azure Arc resource group name |
| version | Video Indexer Extension version, leave empty for latest |
| videoIndexer.accountId | Video Indexer account ID |
| videoIndexer.endpointUri | URL containing a DNS name or IP address to be used as the extension external endpoint |
| ViAi.gpu.enabled | Enable GPU usage for summarization |
| ViAi.gpu.tolerations.key | Maps the nodes where summarization runs with GPU. Convention is to set to `nvidia.com/gpu` |
| ViAi.gpu.nodeSelector.workload | Identifies the node selected for summarization. Set to `summarization`. |


## Prepare for deployment

During the deployment, the script asks for environment specific values. Have these values ready so you can copy and paste them when the script asks for them.

| Question | Value | Details
| --- | --- | --- |
| What is the Video Indexer account ID during deployment? | GUID | Your Video Indexer account ID |
| What is the Azure subscription ID during deployment? | GUID | Your Azure subscription ID |
| What is the name of the Video Indexer resource group during deployment? | string | The resource group name of your Video Indexer account |
| What is the name of the Video Indexer account during deployment? | string | Your Video Indexer account name |

## Deploy with the Azure portal

1. In the Azure portal, navigate to your Azure Arc-connected cluster.
1. From the menu, select **Extensions** > **+ Add** > **Azure AI Video Indexer Arc Extension**.
1. Select **Create**. The *Create an AI Video Indexer extension* screen appears.
1. Configure the extension in *Instance details*:
    1. Select the **subscription** and **resource group** for your extension.
    1. Select the **region and connected** k8 cluster.
    1. Enter a **name** for your extension.
    1. Select the **Azure AI Video Indexer Account** that the extension connects to.
    1. Enter the **cluster endpoint**, either an IP address or DNS name to use as the API endpoint.
    1. Provide the **storage class** you want to use for the extension that's supported by your Kubernetes distribution. For example, if you're using AKS, you could use `azurefile-cli`. For more information about predefined storage classes supported by AKS, see [Storage Classes in AKS](/azure/aks/concepts-storage#storage-classes). If you're using other Kubernetes distributions, see your Kubernetes distribution documentation for predefined storage classes supported or the way you can provide your own.
    1. Select a generative AI model to apply AI capabilities such as textual summarization on VI enabled by Arc. For more information, see [Generative AI with Azure AI Video Indexer (VI)](../generative_ai_with_vi.md).
1. Select **Review + create** and then select **Create**.

## Manual deployment

Use the [sample deployment script](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/VideoIndexerEnabledByArc/aks) to manually deploy the extension. Before you get started, consider Storage class.

**Storage class** - Video Indexer extension requires that a storage volume must be available on the Kubernetes cluster. The storage class needs to support `ReadWriteMany`. It's important to note that the indexing process is IO intensive, so the IOPS (input/output operations per second) of the storage volume has a significant effect on the duration of the process.

> [!IMPORTANT]
> If you're using a language model, you must [label a node or a node pool](/azure/aks/use-labels) with `workload:summarization`. The label is a key-value pair, the key is `workload`, and the value is `summarization`. The machine labeled with this label must have at least 32 CPUs (for production), and we strongly recommend that they're Intel CPUs (as opposed to AMD).

> [!TIP]
> Read the [How to connect your cluster to Azure Arc](/azure/azure-arc/kubernetes/quickstart-connect-cluster?tabs=azure-cli) article for a complete walkthrough of the process.

## Optional configuration

The extension default settings are set to handle the common workloads, for specific cases, the following parameters can be used to configure the resource allocation:

| Parameter | Default | Description |
|-----------|---------|-------------|
| videoIndexer.webapi.resources.requests.cpu | 0.5 | The request number of cores for the web API pod  |
| videoIndexer.webapi.resources.requests.mem | 4Gi | The request memory capacity for the web API pod  |
| videoIndexer.webapi.resources.limits.cpu | 1 | The limits number of cores for the web API pod  |
| videoIndexer.webapi.resources.limits.mem | 6Gi | The limits memory capacity for the web API pod  |
| storage.storageClass | "" | The storage class to be used |
| storage.useExternalPvc | false | Determines whether an external PVC is used. When true, the VideoIndexer PVC isn't installed. |
| scaling.ai.maxReplicaCount | 20 | Sets the AI workload max pod scale (not including summarization)|

## Next steps

Review the [Azure AI Video Indexer enabled by Arc samples](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/VideoIndexerEnabledByArc).