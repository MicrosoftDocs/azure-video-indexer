---
title: Azure AI Video Indexer enabled by Arc troubleshooting guide  
description: Use this guide to troubleshoot issues with Azure AI Video Indexer enabled by Arc.
ms.topic: conceptual
ms.service: azure-video-indexer
ms.date: 11/08/2023
ms.author: inhenkel
author: IngridAtMicrosoft
---

# Azure Video Indexer enabled by Arc troubleshooting guide

Use this guide to troubleshoot issues with [!INCLUDE [variable-edge-product-name](includes/variable-edge-product-name.md)] ([!INCLUDE [variable-edge-product-acronym](includes/variable-edge-product-acronym.md)]).


## The extension was installed successfully, but Video Indexer portal fails to access the extension.
There are multiple reasons that might cause interactions between the Video Indexer portal and the Video Indexer extension, most are network related, e.g. connectivity issues, certificate validation issues and more. Continue reading to determine which issue may be related to accessing the extension.
 
## The playback has buffering delays when streaming from Video Indexer extension.
This behavior is to be expected. Media is streamed from the VM using network streaming. You can either: 

1. Encode your video to MP4/H264 and AAC audio before indexing, to make network streaming supported across most of the devices/browsers/OS.
1. Implement your own streaming server endpoint that does the encoding beforehand or use just-in-time (JIT) encoding.

For example, you could use [ffmpeg](https://ffmpeg.org/) and [Shaka Packager](https://github.com/shaka-project/shaka-packager) to do the encoding preprocessing and the packaging of the encoded file that will allow streaming of HLS/DASH protocols. Using this method the streamable files can be placed in the storage and the streaming endpoint will just serve the files. 
