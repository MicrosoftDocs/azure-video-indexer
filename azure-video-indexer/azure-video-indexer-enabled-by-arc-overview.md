---
title: What is Azure Video Indexer enabled by Arc? (Preview)  
description: Azure AI Video Indexer enabled by Arc an Azure Arc extension enabled service that runs video and audio analysis on edge devices. It's a hybrid video indexing solution that enables customers to index their video content anywhere it resides, on the cloud, the edge or multicloud.
ms.topic: overview
ms.service: azure-video-indexer
ms.date: 2/13/2024
ms.author: inhenkel
author: IngridAtMicrosoft
---

# What is Azure AI Video Indexer enabled by Arc? (Preview)

Azure Video Indexer enabled by Arc is an Azure Arc Extension enabled service that runs video and audio analysis on edge devices. The solution is designed to run on Azure Stack Edge Profile, a heavy edge device, and supports many video formats, including MP4 and other common formats. It supports several languages in all basic audio-related models. It assumes that one Video Indexer resource is mapped to one extension.

If you aren't already familiar with [Azure AI Video Indexer](/azure/azure-video-indexer/), it's recommended that you familiarize yourself with the cloud service first.

Additionally, before you start working with [!INCLUDE [variable-edge-product-name](includes/variable-edge-product-name.md)], review the [transparency note](/legal/azure-video-indexer/transparency-note) to understand usage restrictions.

> [!IMPORTANT]
> To successfully deploy the Azure Video Indexer extension, it is **mandatory** that your Azure subscription id is approved in advance. You must first sign up using [this form](https://aka.ms/vi-register).

# What is Azure Arc and Azure Arc-enabled Kubernetes?

Azure Arc simplifies governance and management of complex environments that extend across data centers, multiple clouds, and edge by delivering a consistent multi-cloud and on-premises management platform.

Azure Arc-enabled Kubernetes allows you to attach Kubernetes clusters running anywhere so that you can manage and configure them in Azure. By managing all of your Kubernetes resources in a single control plane, you can enable a more consistent development and operation experience to run cloud-native apps anywhere and on any Kubernetes platform.

When the Azure Arc agents are deployed to the cluster, an outbound connection to Azure is initiated, using industry-standard SSL to secure data in transit.

Once clusters are connected to Azure, they're represented as their own resources in Azure Resource Manager (ARM), and they can be organized using resource groups and tagging.

See these articles to understand more about [Azure Arc](/azure/azure-arc/overview) and [Azure Arc-enabled Kubernetes](/azure/azure-arc/kubernetes/overview).

## What is an Azure Arc extension?

Virtual machine (VM) extensions are small applications that provide post-deployment configuration and automation tasks on Azure VMs. For example, if a virtual machine requires software installation, anti-virus protection, or to run a script in it, a VM extension can be used. To understand more about extensions, see [Virtual machine extension management with Azure Arc-enabled servers](/azure/azure-arc/servers/manage-vm-extensions).

The Azure Video Indexer extension is what allows you to install and deploy Azure AI Video indexer to the Kubernetes cluster.

## Use cases

All VI enabled by Arc accounts are Azure Resource Manager (ARM) accounts. ARM operations are decoupled from video insight operations. This design allows you to perform analysis on your edge devices without the need to upload your media assets to Azure.

- **Data governance** – You can bring the AI to the content instead of vice versa. Use [!INCLUDE [variable-edge-product-acronym](includes/variable-edge-product-acronym.md)] when you can’t move indexed content from on-premises to the cloud due to:
    - regulation.
    - architecture decisions.
    - data store being too large, making lift and shift a significant effort.

- **On-premises workflow** – Your indexing process is part of an on-premises workflow, and you want to lower the indexing duration latency affecting the flow.
- **Pre-indexing** – You want to index before uploading the content to the cloud. To create clarity, you can presort your on-premises video and/or audio archive, and then only upload it for Standard and/or Advanced indexing in the Cloud.

> [!NOTE]
> To successfully deploy the VI Extension it is mandatory that we approve your Azure subscription id in advance. Therefore you must first sign up using [this form](https://aka.ms/vi-register).

## Example deployment 

The below is a block diagram showing Azure Video Indexer running on Azure Arc. There are three types: 

1. Store type A uses both vision and audio presets.
1. Store type B uses only vision presets. It also has a custom model. For more information about using a custom model with Azure Video Indexer enabled by Arc, see [Bring Your Own AI model](../azure-video-indexer-enabled-by-arc-bring-your-own-model-overview.md). 
1. Store C uses only audio presets. 

The extension is stored on each edge device and each device is associated with a single AI Video Indexer account that interfaces with Azure Arc and the cloud.

:::image type="content" source="../media/common/vi-arc-diagram-v2.svg" lightbox="../media/common/avi-arc-diagram.svg" alt-text="AVI Arc block diagram":::

## Supported AI presets

[!INCLUDE [variable-edge-product-acronym](includes/variable-edge-product-acronym.md)] supports the following indexing presets:

| Model | Basic Video | Basic Audio | Basic Video & Audio |
|--|--|--|--|
| [Transcription](transcription-translation-lid.md) |  | :heavy_check_mark: | :heavy_check_mark: |
| [Translation](transcription-translation-lid.md) |  | :heavy_check_mark: | :heavy_check_mark: |
| [Captioning](view-closed-captions.md) |  | :heavy_check_mark: | :heavy_check_mark: |
| [Key frame detection](scenes-shots-keyframes.md) | :heavy_check_mark: |  | :heavy_check_mark: |
| [OCR](ocr.md) | :heavy_check_mark: |  | :heavy_check_mark: |
| [Scene detection](scenes-shots-keyframes.md) | :heavy_check_mark: |  | :heavy_check_mark: |
| [Shot detection](scenes-shots-keyframes.md) | :heavy_check_mark: |  | :heavy_check_mark: |

:::image type="content" source="media/common/avi-flow-edge.svg" lightbox="media/common/avi-flow-edge.svg" alt-text="Graphic Azure Video Indexer enabled by Arc available presets already listed":::

## Supported input formats and codecs

### Video formats

- AVI  (.avi)
- FLV (with H.264 and AAC codecs) (.flv)
- ISMV (.isma, .ismv)
- Matroska/WebM (.mkv)
- MP4 (.mp4, .m4a, .m4v)
- MXF (.mxf)
- MPEG2-TS
- QuickTime (.mov)
- WAVE/WAV (.wav)
- Webm
- Windows Media Video (WMV)/ASF (.wmv, .asf)

### Video codecs

Here is your alphabetized list:

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

## Supported languages

- Arabic (Saudi Arabia)
- Arabic Egypt
- Chinese (Simplified)
- English (US)
- French
- German
- Italian
- Spanish

## Bring your own model

Azure Video Indexer enabled by Arc also supports bringing your own model. See the [Bring Your Own Model (BYO)](azure-video-indexer-enabled-by-arc-bring-your-own-model-overview.md) article for details.

## Limitations

- The supported file size for indexing is up to 2 GB.
- Upgrading the extension:
    - Extension support applies for the latest version only.
    - We recommend setting that `auto-upgrade` property to `true`. This setting keeps the extension up to date.
    - If the auto upgrade setting is set to false, the version upgrade should be done incrementally. Jumping between versions can cause indexing processes to fail.
- After the extension installation or upgrade, expect the *first* index\translation process duration to be longer. The longer duration is due to AI model image download. The duration varies depending on network speed.
- Only one Video Indexer extension can be deployed per Arc enabled Kubernetes cluster.
- The cluster's volume performance (based on storage class) has significant influence on the turnover duration of the indexing job especially since the frame extraction is writing all frames into the volume).
- You can use only cloud account access tokens obtained via the Azure portal. Cloud video access tokens aren't supported, but with the API, extension access tokens are available and we support all types.
-   Video error messages aren't stored due to memory limitations.

## Next steps
- Try deploying in the Azure portal using the [Azure Video Indexer enabled by Arc quickstart](azure-video-indexer-enabled-by-arc-quickstart.md) 
- Try the [Azure Video Indexer enabled by Arc sample on GitHub ](https://github.com/Azure-Samples/azure-video-indexer-samples/blob/master/VideoIndexerEnabledByArc/aks/readme.md)
- Try the [Azure Video Indexer enable by Arc Jumpstart](https://arcjumpstart.com/azure_arc_jumpstart/azure_edge_iot_ops/aks_edge_essentials_single_vi)
