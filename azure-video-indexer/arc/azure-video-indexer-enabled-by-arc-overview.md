---
title: What is Azure AI Video Indexer enabled by Arc?
description: Azure AI Video Indexer enabled by Arc performs video and audio analysis on edge devices, providing a hybrid solution for indexing content.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: overview
#customer intent: As a video content manager, I want to use Azure AI Video Indexer analyze and index video content on edge devices, ensuring compliance with data governance policies and reducing latency in on-premises workflows.
---

# Azure AI Video Indexer enabled by Arc

[Azure AI Video Indexer enabled by Arc](../azure-video-indexer-enabled-by-arc-overview.md) is an Azure Arc extension enabled service that runs video and audio analysis and [generative AI](../generative_ai_with_vi.md) on edge devices. The solution runs on [Azure Arc enabled Kubernetes](/azure/azure-arc/kubernetes/), supports many video formats, and assumes that one Video Indexer resource maps to one extension. It transcribes spoken content in more than 35 source languages and translates them to English. For a full list of supported languages, see [Supported languages per scenario](../language-support.md#supported-languages-per-scenario).

<!-- Para above is duplicated in azure-video-indexer-enabled-by-arc-quickstart.md so sync any changes-->

If you aren't already familiar with [Azure AI Video Indexer](/azure/azure-video-indexer/), we recommend that you familiarize yourself with the cloud service first.

Additionally, before you start working with Azure AI Video Indexer enabled by Arc, review the [transparency note](/legal/azure-video-indexer/transparency-note) to understand usage restrictions.

> [!IMPORTANT]
> To successfully deploy the Azure AI Video Indexer extension, it's **mandatory** that your Azure subscription ID is approved in advance. You must first sign up using the form at [Application for gated services](https://aka.ms/vi-register).

## What is Azure Arc and Azure Arc-enabled Kubernetes?

Azure Arc simplifies governance and management of complex environments that extend across data centers, multiple clouds, and edge by delivering a consistent multicloud and on-premises management platform.

Azure Arc-enabled Kubernetes allows you to attach Kubernetes clusters running anywhere so that you can manage and configure them in Azure. By managing all of your Kubernetes resources in a single control plane, you can enable a more consistent development and operations experience to run cloud-native apps anywhere and on any Kubernetes platform.

When the Azure Arc agents get deployed to the cluster, an outbound connection to Azure is initiated, using industry-standard SSL to secure data in transit.

Once clusters are connected to Azure, they're represented as their own resources in Azure Resource Manager (ARM), and they can be organized using resource groups and tagging.

For more information about Azure Arc and Arc-enabled Kubernetes, see [Azure Arc overview](/azure/azure-arc/overview) and [What is Azure Arc-enabled Kubernetes?](/azure/azure-arc/kubernetes/overview)

## What is an Azure Arc extension?

Virtual machine (VM) extensions are small applications that provide post-deployment configuration and automation tasks on Azure VMs. For example, if a virtual machine requires software installation, anti-virus protection, or to run a script in it, a VM extension can be used. For more information about extensions, see [Virtual machine extension management with Azure Arc-enabled servers](/azure/azure-arc/servers/manage-vm-extensions).

The Azure AI Video Indexer extension installs and deploys Azure AI Video indexer to the Kubernetes cluster.

Azure AI Video Indexer enabled by Arc only supports Azure Resource Manager accounts. Resource Manager operations are decoupled from video insight operations. This design allows you to perform analysis on your edge devices without the need to upload your media assets to Azure.

The extension is supported in [direct connection mode](/azure/azure-arc/data/connectivity) scenarios only. While all processing is performed in the edge environment, control plane information is sent to the cloud for billing and monitoring purposes. New extension versions are downloaded from the cloud. No customer data, such as what videos were indexed or indexed insights, are sent from the edge location to the cloud.

## Language models

The Phi language model is included and automatically connected with your VI extension. You can start using it immediately. For more information about using language models with VI, see:

- [Use textual summarization](../text-summarization-task.md)
- [Use Azure AI Video Indexer to create prompt content](../prompt-overview.md)
- [Azure AI Video Indexer Bring Your Own (BYO) AI model overview](../bring-your-own-model-overview.md)

See also the [transparency note for textual summarization with VI enabled by Arc](/legal/azure-video-indexer/transparency-note?context=%2Fazure%2Fazure-video-indexer%2Fcontext%2Fcontext#textual-summarization-on-an-edge-device) for hardware requirements, limitations, and known issues.

## Use cases

- **Data governance** – You can bring the AI to the content instead of vice versa. Use Azure AI Video Indexer enabled by Arc when you can’t move indexed content from on-premises to the cloud due to:
    - Regulations.
    - Architecture decisions.
    - Data store being too large, making lift and shift a significant effort.
- **On-premises workflow** – Your indexing process is part of an on-premises workflow, and you want to lower the indexing duration latency affecting the flow.
- **Pre-indexing** – You want to index before uploading the content to the cloud. To create clarity, you can presort your on-premises video or audio archive, and then only upload it for standard or advanced indexing in the cloud.

## Example deployment

The following diagram shows the Azure AI Video Indexer extension running on Azure Arc. There are three types:

1. Store type A uses both vision and audio presets.
1. Store type B uses only vision presets. It also has a custom model. For more information about using a custom model with Azure AI Video Indexer enabled by Arc, see [Bring Your Own AI model](/azure/azure-video-indexer/azure-video-indexer-enabled-by-arc-bring-your-own-model-overview).
1. Store C uses only audio presets.

The extension is stored on each edge device and each device is associated with a single Azure AI Video Indexer account that interfaces with Azure Arc and the cloud.

:::image type="content" source="../media/common/vi-arc-diagram-v2.svg" lightbox="../media/common/vi-arc-diagram-v2.svg" alt-text="Diagram showing the VI Arc extension running on Azure arc." border="false":::

## Supported AI presets

Azure AI Video Indexer enabled by Arc supports the following indexing presets:

| Model | Basic video | Basic audio | Basic video and audio |
|--|--|--|--|
| [Transcription](/azure/azure-video-indexer/transcription-translation-lid) |  | ✔ | ✔ |
| [Translation](/azure/azure-video-indexer/transcription-translation-lid) |  | ✔ | ✔ |
| [Captioning](/azure/azure-video-indexer/view-closed-captions) |  | ✔ | ✔ |
| [Key frame detection](/azure/azure-video-indexer/scenes-shots-keyframes) | ✔ |  | ✔ |
| [Object detection](/azure/azure-video-indexer/object-detection) | ✔ |  | ✔ |
| [Scene detection](/azure/azure-video-indexer/scenes-shots-keyframes) | ✔ |  | ✔ |
| [Shot detection](/azure/azure-video-indexer/scenes-shots-keyframes) | ✔ |  | ✔ |
| [Summarization](/azure/azure-video-indexer/text-summarization-overview) | ✔ | ✔ | ✔ |

<!--
:::image type="content" source="../media/common/avi-flow-edge.svg" lightbox="../media/common/avi-flow-edge.svg" alt-text="Graphic Azure AI Video Indexer enabled by Arc available presets already listed":::
-->

## Minimum hardware requirements

Video Indexer enabled by Arc is designed to run on any Arc enabled Kubernetes environment.

>[!NOTE]
> The following table covers minimum requirements for a *production* environment. We recommend at least a two-node cluster for high availability and scalability. The recommended settings refer to cluster-wide settings. So for example, if you have two nodes, each node should have 16 cores and 32 GB of RAM. We recommend creating a dedicated node-pool or autoscaling groups to host the VI solution.

| Configuration | Virtual machine count | Node CPU cores count  | Node RAM | Node storage | Remarks
| --- | --- | --- | --- | --- | --- |
| Minimum | One | 32 Cores | 64 GB | 50 GB | Storage needs to support `ReadWriteMany` Storage Class |
| Recommended | Two | 48-64 Cores | 256 GB | 100 GB | Storage needs to support `ReadWriteMany` Storage Class |

## Minimum software requirements

| Component |  Minimum requirements |
| --- | --- |
| Operating system | Ubuntu 22.04 LTS or any Linux Compatible OS |
| Kubernetes | 1.29 |
| Azure CLI | 2.64.0 |

<!-- section duplicated to azure-video-indexer-enabled-by-arc-quickstart-->

## Network requirements

Use the following information to configure firewall settings.

### Firewall requirements

Follow the instructions at [Azure Arc-enabled Kubernetes network requirements](/azure/azure-arc/kubernetes/network-requirements).

In addition, add *.azureedge.net and *.data.microsoft.com.

For the Video Indexer enabled by Arc extension, add these endpoints:

| Endpoint (DNS) | Description |
|---|---|
| linuxgeneva-microsoft.azurecr.io, *.blob.core.windows.net | Used for container registry for telemetry containers |
| *.monitoring.core.windows.net, *.microsoftmetrics.com, *.table.core.windows.net | Used for telemetry |
| api.videoindexer.ai | Used for access token validation |

### Summary of required endpoints and ports

Enable the following endpoints and ports.

#### Azure Arc Services (HTTPS)

- management.azure.com:443
- *.dp.kubernetesconfiguration.azure.com:443
- login.microsoftonline.com:443
- *.login.microsoft.com:443
- login.windows.net:443
- mcr.microsoft.com:443
- *.data.mcr.microsoft.com:443
- dl.k8s.io:443
- gbl.his.arc.azure.com:443
- *.his.arc.azure.com:443
- guestnotificationservice.azure.com:443
- *.guestnotificationservice.azure.com:443
- sts.windows.net:443
- *.servicebus.windows.net:443
- graph.microsoft.com:443
- *.arc.azure.net:443
- linuxgeneva-microsoft.azurecr.io:443

#### Azure Arc OBO Services (custom HTTPS port)

- *.obo.arc.azure.com:8084

#### Azure File Storage (SMB)

- STORAGE_ACCOUNT_NAME.file.core.windows.net:139,445

> [!NOTE]
> When you use AKS with the Azure Files CSI driver to mount shares as persistent volumes, open ports 139 and 445 for the specific file share.

#### Telemetry (HTTPS)

- linuxgeneva-microsoft.azurecr.io:443
- *.blob.core.windows.net:443
- gcs.prod.monitoring.core.windows.net:443
- *.microsoftmetrics.com:443
- *.table.core.windows.net:443
- *.azureedge.net:443
- *.data.microsoft.com:443

#### VideoIndexer (HTTPS)

- api.videoindexer.ai:443

## Supported input formats and codecs

The following section lists the supported input formats and codecs for Azure AI Video Indexer enabled by Arc.

### Video formats

- AVI (.avi)
- FLV (with H.264 and AAC codecs) (.flv)
- ISMV (.isma, .ismv)
- Matroska (.mkv)
- MP4 (.mp4, .m4a, .m4v)
- MXF (.mxf)
- MPEG2-TS
- QuickTime (.mov)
- WAVE/WAV (.wav)
- Windows Media Video (WMV)/ASF (.wmv, .asf)

### Video codecs

- AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra
- Digital video (DV) (in AVI files)
- DVCPro/DVCProHD (in MXF container)
- HEVC/H.265
- MPEG-1
- MPEG-2 (up to 422 Profile and High Level; including variants such as Sony XDCAM, Sony XDCAM HD, Sony XDCAM IMX, CableLabs®, and D10)
- MPEG-4 Part 2
- VC-1/WMV9

### Audio codecs up to two tracks

- AAC (AAC-LC, AAC-HE, and AAC-HEv2)
- FLAC
- MPEG Layer 2
- MP3 (MPEG-1 Audio Layer 3)
- VORBIS
- WAV/PCM
- Windows Media Audio

## Bring your own model

Azure AI Video Indexer enabled by Arc also supports bringing your own model. For more information, see the [Bring Your Own Model (BYO)](/azure/azure-video-indexer/azure-video-indexer-enabled-by-arc-bring-your-own-model-overview) article.

## Limitations

- The supported file size for indexing is up to 2 GB.
- Azure AI Video Indexer enabled by Arc doesn't support uploading and indexing videos with a resolution of 1920x1080 or greater.
- Upgrading the extension:
    - Extension support applies to the latest version only.
    - We recommend setting the `auto-upgrade` property to `true`. The setting keeps the extension up to date.
    - If the auto upgrade setting is set to false, you should upgrade the version incrementally. Jumping between versions can cause indexing processes to fail.
- After extension installation or upgrade, expect the *first* index\translation process duration to be longer than normal. The longer duration is due to AI model image download. The duration varies depending on network speed.
- Only one Video Indexer extension can be deployed per Arc enabled Kubernetes cluster.
- The cluster's volume performance (based on storage class) has significant influence on the turnover duration of the indexing job especially since the frame extraction is writing all frames into the volume.
- Only extension access tokens are supported. You can obtain extension access tokens from API/CLI. For samples to get-access-token, see [How to access the extension](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/VideoIndexerEnabledByArc/aks#how-to-acccess-the-extension-).
-   Video error messages aren't stored due to memory limitations.

## Azure Container Storage enabled by Arc

We recommend that you use Azure Container Storage enabled by Azure Arc for storage. For more information, see the following articles:

- [What is Azure Container Storage enabled by Azure Arc?](/azure/azure-arc/container-storage/overview)
- [Prepare Linux for Edge Volumes](/azure/azure-arc/container-storage/howto-prepare-linux-edge-volumes)

## Related content

- Try the [Azure AI Video Indexer enabled by Arc sample on GitHub ](https://github.com/Azure-Samples/azure-video-indexer-samples/blob/master/VideoIndexerEnabledByArc/aks/readme.md)
- Try the [Azure AI Video Indexer enable by Arc Jumpstart](https://arcjumpstart.com/azure_arc_jumpstart/azure_edge_iot_ops/aks_edge_essentials_single_vi)
- Try deploying in the Azure portal using the [Azure AI Video Indexer enabled by Arc quickstart](/azure/azure-video-indexer/azure-video-indexer-enabled-by-arc-quickstart)
