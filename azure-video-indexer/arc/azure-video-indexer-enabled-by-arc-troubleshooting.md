---
title: Azure AI Video Indexer enabled by Arc troubleshooting guide  
description: Use this guide to troubleshoot issues with Azure AI Video Indexer enabled by Arc.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 05/30/2025
ms.service: azure-video-indexer
ms.topic: conceptual
---

# Azure AI Video Indexer enabled by Arc (preview) troubleshooting guide

Use this guide to troubleshoot issues with Azure AI Video Indexer enabled by Arc.

## Possible errors

If you encounter an error while using Azure AI Video Indexer enabled by Arc, check the following:

*The extension was installed successfully, but Video Indexer portal fails to access the extension.*

There are many reasons that might cause interactions between the Video Indexer portal and the Video Indexer extension, most are network related. For example, connectivity issues and certificate validation issues. Continue reading to determine which issue might be related to accessing the extension.

*The playback has buffering delays when streaming from Video Indexer extension.*

This behavior is expected. Media is streamed from the VM using network streaming. You can either: 

- Encode your video to MP4/H264 and AAC audio before indexing, to make network streaming supported across most of the devices/browsers/OS.
- Implement your own streaming server endpoint that does the encoding beforehand or use just-in-time (JIT) encoding.

For example, you could use [ffmpeg](https://ffmpeg.org/) and [Shaka Packager](https://github.com/shaka-project/shaka-packager) to do the encoding preprocessing and the packaging of the encoded file that allows streaming of HLS/DASH protocols. When you use this method, the streamable files can be placed in the storage and the streaming endpoint just serve the files. 
