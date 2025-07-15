---
title: Troubleshoot Azure AI Video Indexer enabled by Arc
description: Troubleshoot common issues with Azure AI Video Indexer enabled by Arc, including connectivity, streaming, and encoding problems.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/09/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: troubleshooting-general
# customer intent: As a user of Azure AI Video Indexer enabled by Arc, I want to troubleshoot common issues related to connectivity, streaming, and encoding so that I can resolve them quickly.
---

# Troubleshoot Azure AI Video Indexer enabled by Arc (preview)

Use this guide to troubleshoot issues with Azure AI Video Indexer enabled by Arc.

## Possible errors

If you encounter an error while using Azure AI Video Indexer enabled by Arc, check the following issues:

*The extension was installed successfully, but Video Indexer portal fails to access the extension.*

There are many reasons that might cause interactions between the Video Indexer portal and the Video Indexer extension, most are network related. For example, connectivity issues and certificate validation issues. Continue reading to determine which issue might be related to accessing the extension.

*The playback has buffering delays when streaming from Video Indexer extension.*

This behavior is expected. Media is streamed from the virtual machine (VM) using network streaming. You can either:

- Encode your video to MP4/H264 and AAC audio before indexing, to make network streaming supported across most of the devices/browsers/OS.
- Implement your own streaming server endpoint that does the encoding beforehand or use just-in-time (JIT) encoding.

For example, you could use [ffmpeg](https://ffmpeg.org/) and [Shaka Packager](https://github.com/shaka-project/shaka-packager) to do the encoding preprocessing and the packaging of the encoded file that allows streaming of HLS/DASH protocols. When you use this method, the streamable files can be placed in the storage and the streaming endpoint just serve the files.

## Related content

- [What is Azure AI Video Indexer enabled by Arc?](azure-video-indexer-enabled-by-arc-overview.md)