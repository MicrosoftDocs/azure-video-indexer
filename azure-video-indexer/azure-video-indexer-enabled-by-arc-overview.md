---
title: Azure AI Video Indexer enabled by Arc overview  
description: Azure AI Video Indexer enabled by Arc an Azure Arc extension enabled service that runs video and audio analysis on edge devices. It's a hybrid video indexing solution that enables customers to index their video content anywhere it resides, on the cloud, the edge or multicloud.
ms.topic: overview
ms.service: azure-video-indexer
ms.date: 12/11/2023
ms.author: inhenkel
author: IngridAtMicrosoft
---

# Azure Video Indexer enabled by Arc overview (preview)

[!INCLUDE [variable-edge-product-name](includes/variable-edge-product-name.md)] ([!INCLUDE [variable-edge-product-acronym](includes/variable-edge-product-acronym.md)]) is an Azure Arc extension enabled service that runs video and audio analysis on edge devices. It's a hybrid video indexing solution that enables customers to index their video content anywhere it resides, on the cloud, the edge or multicloud.

Before you start working with [!INCLUDE [variable-edge-product-name](includes/variable-edge-product-name.md)], review the [transparency note](/legal/azure-video-indexer/transparency-note) to understand usage restrictions.

## Azure Arc

[Azure Arc](/azure/azure-arc/overview) allows you to manage the resource types hosted outside of Azure, such as:

- Windows and Linux physical servers
- Kubernetes clusters
- Azure data services
- SQL server
- Azure Stack HCI
- virtual machines based on VMware vSphere

### What is an Azure Arc extension?
An Azure Arc extension is a way to of deliver agents, scripts, and configurations to your on-premises machines orchestrated using the Azure portal or API. For more information about Azure Arc extensions, see [Manage VM extensions](/azure/azure-arc/servers/manage-vm-extensions).

[!INCLUDE [variable-edge-product-acronym](includes/variable-edge-product-acronym.md)] works on both heavy edge and light edge devices, giving you design flexibility. An example of a heavy edge device is Azure Stack HCI. Examples of light edge devices include cell phones, vehicles, and sensors.

You can use [!INCLUDE [variable-edge-product-acronym](includes/variable-edge-product-acronym.md)] on any of the compute resources offered by Azure Arc.

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

## Capacity planning

It is important to plan the resources needed for your environment. The table below outlines the recommended and minimal resources needed to index videos in a range of lengths and sizes. Use the table to determine the capacity needed for your deployment. Things to consider include:

- Video length
- Video size
- Minimal turnover duration - Need definition. What is turnover?
- Average turnover duration - Need definition. What is turnover?
- Turnover duration P50, P75, P85 - What does P50 stand for?
- Node count - the number of virtual machines needed to process the video
- Recommended CPU - the number of recommended (not minimal) cores for each node
- Recommended memory - the size of recommended (not minimal) memory for each node
- Total resources - total recommended (not minimal) cores and memory
- Minimum resources per machine - the minimum resources needed for analyzing each video

> [!TIP]
> For videos over 9 minutes, the recommended total capacity is 256 cores with 1024 GB of memory, and the minimum resources per machine is 32 cores and 10 GB of memory.

| **Video Duration** | **Video Size** | **Minimal Turnover Duration** | **Average Turnover Duration** | **Turnover Duration P50** | **Turnover Duration P75** | **Turnover Duration P85** | **Node Count** | **Recommended CPU** | **Recommended Memory** | **Total Resources** | **Minimal Resources per Machine** |
|--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20 seconds | 3.114 Mb | 03:57 minutes | 04:24 minutes | 04:24 minutes | 04:39 minutes | 04:44 minutes | 2 | 16 cores | 64 GB | 32 cores/128 GB | 16 cores/6GB |
| 90 seconds | 5.044 Mb | 05:12 minutes | 05:27 minutes | 05:26 minutes | 05:34 minutes | 05:37 minutes | 2 | 32 cores | 128 GB | 64 cores/256 GB | 16 cores/6 GB |
| 9 minutes | 31.37 Mb | 08:06 minutes | 08:23 minutes | 08:15 minutes | 08:32 minutes | 08:42 minutes | 3 | 64 cores | 256 GB | 64 cores/256 GB | 32 cores/6 GB |
| 24 minutes | 334 Mb | 22:56 minutes | 23:29 minutes | 23:14 minutes | 23:34 minutes | 24:49 minutes | 4 | 64 cores | 256 GB | 64 cores/256 GB | 32 cores/6 GB |
| 33 minutes | 810 Mb | 21:34 minutes | 22:35 minutes | 22:43 minutes | 22:48 minutes | 23:29 minutes | 4 | 64 cores | 256 GB | 64 cores/256 GB | 32 cores/6 GB |
| 1:07 hours | 1.6 Gb | 48:11 minutes | 49:56 minutes | 49:46 minutes | 50:44 minutes | 51:58 minutes | 4 | 64 cores | 256 GB | 64 cores/256 GB | 32 cores/6 GB |

## Next steps
- Try deploying in the Azure portal using the [Azure Video Indexer enabled by Arc quickstart](azure-video-indexer-enabled-by-arc-quickstart.md) 
- Try the [Azure Video Indexer enabled by Arc sample on GitHub ](https://github.com/Azure-Samples/media-services-video-indexer/blob/master/AVIenabledbyArc/readme.md)
- Try the [Azure Video Indexer enable by Arc Jumpstart](https://arcjumpstart.com/azure_arc_jumpstart/azure_edge_iot_ops/aks_edge_essentials_single_vi)
