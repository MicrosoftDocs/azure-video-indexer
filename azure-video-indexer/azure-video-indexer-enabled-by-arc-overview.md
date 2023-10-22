---
title: Azure AI Video Indexer enabled by Arc overview  
description: Azure AI Video Indexer enabled by Arc (AVIEA) an Azure Arc extension enabled service that runs video and audio analysis on edge devices. It's a hybrid video indexing solution that enables customers to index their video content anywhere it resides, on the cloud, the edge or multicloud.
ms.topic: tutorial
ms.date: 10/04/2023
ms.author: inhenkel
author: IngridAtMicrosoft
---

# Azure Video Indexer enabled by Arc overview

Azure AI Video Indexer enabled by Arc (AVIeA) an Azure Arc extension enabled service that runs video and audio analysis on edge devices. It's a hybrid video indexing solution that enables customers to index their video content anywhere it resides, on the cloud, the edge or multicloud.

Before you start working with Azure Video Indexer enabled by Arc, review the [transparency note](/legal/azure-video-indexer/transparency-note) to understand usage restrictions.

## Azure Arc

Azure Arc allows you to manage the resource types hosted outside of Azure, such as:

- Windows and Linux physical servers
- Kubernetes clusters
- Azure data services
- SQL server
- Azure Stack HCI
- virtual machines based on VMware VSphere

AVIeA works on both heavy edge and light edge devices, giving you design flexibility. An example of a heavy edge device is Azure Stack HCI. Examples of light edge devices include cell phones, vehicles, and sensors.

## Use cases

All AVIeA accounts are Azure Resource Manager (ARM) accounts. ARM operations are decoupled from video insight operations. This design allows you to perform analysis on your edge devices without the need to upload your media assets to Azure.

- **Data governance** – You can bring the AI to the content instead of vice versa. Use AVIEA when you can’t move indexed content from on-premises to the cloud due to:
    - regulation.
    - architecture decisions.
    - data store being too large, making lift and shift a significant effort.

- **On-premises workflow** – Your indexing process is part of an on-premises workflow, and you want to lower the indexing duration latency affecting the flow.
- **Pre-indexing** – You want to index before uploading the content to the cloud. To create clarity, you can presort your on-premises video\audio archive, and then only upload it for Standard\Advanced indexing in the Cloud.

## Sample architecture

You can use AVIeA on any of the compute resources offered by Azure Arc. The following example architecture diagram shows how AVIeA is used with a few Kubernetes clusters.

**TO-DO: DIAGRAM**
<!--
DIAGRAM ::image type="content" source="media/file-name/image-name.png" lightbox=” media/file-name/image-name.png” alt-text="screenshot of the interface of the timeline tab":::--> 
DIAGRAM
DIAGRAM EXPLANATION

## Supported AI presets

AVIeA supports the following indexing presets:

| Model | Basic Video | Basic Audio | Basic Video & Audio |
|--|--|--|--|
| Transcription |  | :heavy_check_mark: | :heavy_check_mark: |
| Translation |  | :heavy_check_mark: | :heavy_check_mark: |
| Captioning | :heavy_check_mark: |  | :heavy_check_mark: |
| Object detection | :heavy_check_mark: |  | :heavy_check_mark: |
| Key frame detection | :heavy_check_mark: |  | :heavy_check_mark: |
| Scene detection | :heavy_check_mark: |  | :heavy_check_mark: |
| Shot detection | :heavy_check_mark: |  | :heavy_check_mark: |

## Supported input formats and codecs

### Video formats

- AVI (.avi)
- FLV (with H.264 and AAC codecs) (.flv)
- Matroska/WebM (.mkv)
- MPEG2-TS
- MP4 (.mp4, .m4a, .m4v)/ISMV (.isma, .ismv)
- MXF (.mxf)
- QuickTime (.mov)
- WAVE/WAV (.wav)
- Webm
- Windows Media Video (WMV)/ASF (.wmv, .asf)

### Video codecs

- Apple ProRes 422
- Apple ProRes 422 HQ
- Apple ProRes 422 LT
- Apple ProRes 4444
- Apple ProRes 4444 XQ
- Apple ProRes Proxy
- AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra
- Digital video (DV) (in AVI files)
- DVCPro/DVCProHD (in MXF container)
- HEVC/H.265
- MPEG-1
- MPEG-2 (up to 422 Profile and High Level; including variants such as Sony XDCAM, Sony XDCAM HD, Sony XDCAM IMX, CableLabs®, and D10)
- MPEG-4 Part 2
- Sony XAVC / XAVC S (in MXF container)
- VC-1/WMV9
- VP8/9

### Audio codecs

- AAC (AAC-LC, AAC-HE, and AAC-HEv2)
- FLAC
- MP3 (MPEG-1 Audio Layer 3)
- MPEG Layer 2
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

## Limitations

-   Up to 2-GB media file size in storage. Manage the quality (how it affects indexing results) to size ratio accordingly.
-   Video error messages aren't stored due to memory limitations.

## Next steps

- [Try Azure Video Indexer enabled by Arc](azure-video-indexer-enabled-by-arc-tutorial.md)
- **TO DO** **Link to API goes here.**
