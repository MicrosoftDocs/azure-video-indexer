---
title: Try Azure AI Video Indexer enabled by Arc
description: This article walks you through the steps required to enable Video Indexer as an Arc extension on your current infrastructure.
ms.topic: quickstart
ms.service: azure-video-indexer
ms.date: 06/25/2024
ms.author: inhenkel
author: IngridAtMicrosoft
---

# Try Azure AI Video Indexer enabled by Arc

[Azure AI Video Indexer enabled by Arc](azure-video-indexer-enabled-by-arc-overview.md) is an Azure Arc extension enabled service that runs video and audio analysis on edge devices. The solution is designed to run on [Azure Arc enabled Kubernetes](/azure/azure-arc/kubernetes/) and supports many video formats, including MP4 and other common formats. It supports several languages in all basic audio-related models. It assumes that one Video Indexer resource is mapped to one extension.

This article walks you through the steps required to enable Video Indexer as an Arc extension on your current infrastructure.

## Possible deployment

Here is a block diagram showing Azure AI Video Indexer running on Azure Arc. There are three types: 

1. Store type A uses both vision and audio presets.
1. Store type B uses only vision presets. It also has a custom model. For more information about using a custom model with Azure AI Video Indexer enabled by Arc, see [Bring Your Own AI model](../azure-video-indexer-bring-your-own-model-overview.md). 
1. Store C uses only audio presets. 

The extension is stored on each edge device and each device is associated with a single AI Video Indexer account that interfaces with Azure Arc and the cloud.

:::image type="content" source="../media/common/vi-arc-diagram-v2.svg" lightbox="../media/common/avi-arc-diagram.svg" alt-text="VI Arc block diagram":::

## Prerequisites

> [!IMPORTANT]
> To successfully deploy the Azure AI Video Indexer extension, it is **mandatory** that your Azure subscription id is approved in advance. You must first sign up using [this form](https://aka.ms/vi-register).

- Create an Azure subscription with permissions for creating Azure resources.
- Create an Azure AI Video Indexer Account. Use the [Create Video Indexer account](/azure/azure-video-indexer/create-account-portal) tutorial.
- Create an [Arc enabled Kubernetes cluster](/azure/aks/hybrid/aks-create-clusters-portal).
- Download the [example video](../media/common/video.mp4).

To use the Video Indexer extension, you need to have an externally facing endpoint, which can be either a DNS name or IP. The endpoint should be set as a secure transfer protocol (`https:\\`) and is used as the extension API endpoint. It's also used by the Video Indexer web portal to communicate with the extension. It's recommended that you use an ingress control to manage the endpoint. 

> [!NOTE]
> If the endpoint isn't publicly accessible, you will be able to perform actions on the extension from the web portal only from the local network.

## Minimum hardware requirements for this quickstart

This quickstart is designed to allow you to see the extension in action, so smaller resource sizes have been chosen for you to work with in a *test* environment. For this quickstart, the minimum hardware requirements are:

- CPU: 16 cores
- Memory: 16 GB

For the minimum hardware requirements in a *production* environment, see the [Minimum hardware requirements](/azure/azure-video-indexer/azure-video-indexer-enabled-by-arc-overview#minimum-hardware-requirements) in the overview article.

[!INCLUDE [minimum-software-requirements](../includes/vi-arc-minimum-software-requirements.md)]

## Parameter definitions

| Parameter | Default | Description |
| --------- | ------- | ----------- |
| release-namespace | yes | The Kubernetes namespace that the extension is installed into |
| cluster-name |  | The Kubernetes Azure Arc instance name
| resource-group |  | The Kubernetes Azure Arc resource group name
| version | yes | Video Indexer Extension version, leave empty for latest |
| speech.endpointUri |  | Speech Service Url Endpoint (link)
| speech.secret |  | Speech Instance secret (link) |
| translate.endpointUri |  | Translation Service Url Endpoint (link)
| translate.secret |  | Translation Service secret (link)
| ocr.endpointUri |  | OCR Service Url Endpoint (link)
| ocr.secret |  |OCR Service secret (link) |
| videoIndexer.accountId |  | Video Indexer Account ID |
| videoIndexer.endpointUri |  | Dns Name or IP to be used as the extension external endpoint.|

## Prepare for deployment

During the deployment, the script asks for environment specific values. Have these values ready so you can copy and paste them when the script asks for them. 

| Question | Value | Details
| --- | --- | --- |
| What is the Video Indexer account ID during deployment? | GUID | Your Video Indexer Account ID |
| What is the Azure subscription ID during deployment? | GUID | Your Azure Subscription ID |
| What is the name of the Video Indexer resource group during deployment? | string | The Resource Group Name of your Video Indexer Account |
| What is the name of the Video Indexer account during deployment? | string | Your Video Indexer Account name | 

## Deploy with the Azure portal

1. In the Azure portal, navigate to your Azure Arc-connected cluster.
1. From the menu, select **Extensions** > **+ Add** > **Azure AI Video Indexer Arc Extension**.
1. Select **Create**. The *Create an AI Video Indexer extension* screen will appear.
1. Configure the extension in *Instance details*:
    1. Select the **subscription** and **resource group** for your extension.
    1. Select the **region and connected** k8 cluster.
    1. Enter a **name** for your extension.
    1. Select the **Azure AI Video Indexer Account** that the extension will be connected to.
    1. Enter the **cluster endpoint**, either an IP or DNS Name to be used as the API endpoint.
    1. Provide the **storage class** you want to use for the extension that's supported by your Kubernetes distribution. For example, if you're using AKS, you could use `azurefile-cli`. For more information on predefined storage classes supported by AKS, see [Storage Classes in AKS](/azure/aks/concepts-storage#storage-classes). If you're using other Kubernetes distributions, see your Kubernetes distribution documentation for predefined storage classes supported or the way you can provide your own.
1. Select **Review + create** and then **Create**.

## Phi 3 language model

The Phi 3 language model is automatically included and connected with your VI extension. You can start using it immediately. For more information about using language models with VI see:

[Use textual summarization](text-summarization-task.md)
[Use Azure AI Video Indexer to create prompt content](prompt-task.md)
[Azure AI Video Indexer Bring Your Own (BYO) AI Model (Preview) overview](azure-video-indexer-bring-your-own-model-overview.md)

## Manual deployment

Use the [sample deployment script](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/VideoIndexerEnabledByArc/aks) to manually deploy the extension. Before you get started here are some things to keep in mind:

- **Storage class** - Video Indexer extension requires that a storage volume must be available on the Kubernetes cluster. The storage class needs to support `ReadWriteMany`. It's important to note that the indexing process is IO intensive, so the IOPS (input/output operations per second) of the storage volume will have a significant impact on the duration of the process.
- **Managed AI resources** - Some Azure AI resources (Translator, Transcription, and OCR) will be created on the Microsoft tenant. These resources are for your subscription only and are under a pay-as-you-go model. If you already have an AI Video Indexer Arc-enabled resource in your subscription, it will be associated with existing Azure AI resources.

> [!TIP] 
> Follow the article [how to connect your cluster to Azure Arc](/azure/azure-arc/kubernetes/quickstart-connect-cluster?tabs=azure-cli) on Azure Docs for a complete walkthrough of this process.

## Optional configuration

The extension default settings are set to handle the common workloads, for specific cases, the following parameters can be used to configure the resource allocation:

| Parameter | Default | Description |
|-----------|---------|-------------|
| AI.nodeSelector | - | The node Selector label on which the AI Pods (speech and translate) are assigned to | 
| speech.resource.requests.cpu | 1 | The requested number of cores for the speech pod |
| speech.resource.requests.mem | 2Gi | The requested memory capacity for the speech pod |
| speech.resource.limits.cpu | 2 | The limits number of cores for the speech pod. must be > speech.resource.requests.cpu  |
| speech.resource.limits.mem | 3Gi | The limits memory capacity for the speech pod. must be > speech.resource.requests.mem  |
| translate.resource.requests.cpu | 1 | The requested number of cores for the translate pod |
| translate.resource.requests.mem | 16Gi | The requested memory capacity for the translate pod |
| translate.resource.limits.cpu | -- | The limits number of cores for the translate pod. must be > translate.resource.requests.cpu  |
| translate.resource.limits.mem | -- | The limits memory capacity for the translate pod. must be > translate.resource.requests.mem  |
| videoIndexer.webapi.resources.requests.cpu | 0.5 | The request number of cores for the web API pod  |
| videoIndexer.webapi.resources.requests.mem | 4Gi | The request memory capacity for the web API pod  |
| videoIndexer.webapi.resources.limits.cpu | 1 | The limits number of cores for the web API pod  |
| videoIndexer.webapi.resources.limits.mem | 6Gi | The limits memory capacity for the web API pod  |
| videoIndexer.webapi.resources.limits.mem | 6Gi | The limits memory capacity for the web API pod  |
| storage.storageClass | "" | The storage class to be used |
| storage.useExternalPvc | false | determines whether an external PVC is used. if true, the VideoIndexer PVC isn't installed |

## [Deploy with ARM or Bicep](#tab/arm)

You can deploy Azure AI Video Indexer enabled by Arc with an ARM template and Bicep. See the [Samples repo README](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/VideoIndexerEnabledByArc/aks) for detailed instructions.
