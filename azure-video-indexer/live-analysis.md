---
title: Azure AI Video Indexer real-time analysis overview - Preview
description: Overview of real-time analysis capabilities in Azure AI Video Indexer, including real-time video indexing and insights.
appliesto:
- Azure AI Video Indexer enabled by Azure Arc
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 12/09/2025
ms.service: azure-video-indexer
ms.topic: concept-article
# customer intent: As a user of Azure AI Video Indexer, I want to understand the real-time analysis capabilities, including real-time video indexing and insights, so that I can utilize these features for live events and broadcasts.
---

# Real-time video analysis in Azure AI Video Indexer - Preview

Azure AI Video Indexer enabled by Arc (VI), as part of an adaptive cloud approach, introduces real-time video analysis. It enables you to extract real-time insights from your live video footage, allowing immediate detection and action at the edge. VI real-time video analysis offers out-of-the-box insights and the ability to define custom AI insights to identify specific objects or states that are tailored for your specific needs. You can view real-time insights directly on top of your video stream, with bounding boxes highlighting detected objects. You can also save streams and insights as files. You can upload and index external media files. With Azure AI Video Indexer, you can generate concise summaries for segments of your recorded video footage, helping you quickly catch up on key events without watching the entire video.

The service is easy to evaluate and integrate. Use the web portal or REST API to add Azure AI Video Indexer to your workflows and systems.

- You don't pay extra for real-time video analysis while it's in preview.
- Real-time analysis was validated on Azure Local but is compatible with any Kubernetes infrastructure.

> [!IMPORTANT]
> To deploy the Azure AI real-time video indexer extension, get your Azure subscription ID approved in advance. You can sign up at [Azure AI Video Indexer Enabled by Arc - real-time analysis early access program](https://aka.ms/vi-live-register).

## What can I do with real-time analysis?

You can integrate the VI real-time analysis with camera real-time streaming to use AI-based detection from different locations. This service analyzes live videos, turning raw footage into actionable insights.

## Customer scenarios and use cases

- **Retail** - Optimize store layouts and improve customer experience and safety. With real-time analysis you can monitor the number of customers in checkout lines in real time, helping retailers to act immediately to optimize staffing and reduce wait times.

- **Manufacturing -** Ensure quality control and worker safety through video analysis. For example, workers who aren't wearing protective gear, which requires real-time detection of critical events and locating specific moments in video streams.

- **Modern Safety -** Detect and identify security and safety issues before they cause a risk.

## Limitations

The following limitations apply to the real-time analysis feature:

### Camera limitations

- Only static cameras are supported. PTZ cameras aren't supported.
- Cameras must support RTCP sender reports.
- Only continuous video streaming is supported. Motion-triggered video isn't supported.
- Frame rate should be between 28-32 FPS. All cameras connected to the same extension should have the same FPS.
- The minimum supported resolution is 640 x 480 pixels. The recommended resolution for optimal performance is 1,280 x 720 pixels.
- When you use ultra-high-resolution videos (frame width equal to or greater than 3,840 pixels, or frame height equal to or greater than 2,160 pixels), the system automatically uses a solution that detects small objects and covers the whole frame. However, the recorded video is saved in a lower resolution, which is Full HD (1920 x 1,080 pixels) while keeping the aspect ratio. The system can't accept videos with ultra-high resolution and videos with lower resolutions on the same extension.
- Color should be RGB.
- Fisheye lenses aren't supported.

### Detection limitations 

- The system detects only objects larger than 35 x 35 pixels.
- The detector might not detect objects in dark areas and in bad weather conditions. Extreme weather conditions can reduce results quality. For example, heavy rain and fog.
- Occlusions might reduce results quality and cause fragmentation in object tracking.
- The detector can miss or misclassify objects when viewed from an unusual point of view or extreme angles.
- The confidence score of the detection as appears in the UI represents its first appearance. Along the track, the confidence can change, and is only shown in the API.

## Hardware requirements

Here's a table that shows the hardware requirements.

Minimum:

| **VM count** | **CPU (per node)** | **RAM (per node)** | **Storage** | **GPU**    |
|--------------|-----------------------|-----------------------|-------------|------------|
| 1            | 32 cores              | 64 GB                 | 200 GB      |            |
| 1            | 16 cores              | 64 GB                 | 200 GB      | NVIDIA A2 |

Recommended

| **VM count** | **CPU (per node)** | **RAM (per node)** | **Storage** | **GPU**            |
|--------------|-----------------------|-----------------------|-------------|--------------------|
| 2            | 32 cores              | 64 GB                 | 200 GB      |                    |
| 1            | 16 cores              | 64 GB                 | 200 GB      | NVIDIA A100 / H100 |

**The number of supported cameras** in one extension depends on the GPU used and the capabilities running on the camera, as detailed in the following table:

| **Scenario \ GPU**                   | **A2** | **A10** | **V100** | **A100** | **H100** |
|--------------------------------------|--------|---------|----------|----------|----------|
| **Streaming + Recording + Insights** | 1 to 4 | 6       | 2        | 8        | 11       |
| **Streaming + Insights**             | 1 to 4 | 7       | 2        | 11       | 12       |
| **Insights Only**                    | 1 to 4 | 7       | 2        | 16       | 16       |
| **Hard Limit**                       | 4      | 8       | 4        | 16       | 16       |

*Using ultra resolution might reduce the number of supported cameras per GPU.*

- Supported GPUs are NVIDIA A2, A10, V100, A100, and H100.
- The minimum required shared storage is 50 GB for one camera per day. This estimation is based on the scenario where both recordings and insights are saved.
- To upload video media files to the live extension, add another virtual machine (VM) without a GPU, as specified in [Minimum hardware requirements for VI enabled by Arc](arc/azure-video-indexer-enabled-by-arc-overview.md#minimum-hardware-requirements).
- Using event summary for recorded media files requires an extra VM with GPU.

### Minimum software requirements

| **Component**    | **Minimum requirements**                    |
|------------------|---------------------------------------------|
| Operating system | Ubuntu 20.04 LTS or any Linux compatible OS |
| Kubernetes       | 1.29                                        |
| Azure CLI        | 2.64.0                                      |
| CUDA             | 12.6 on the VM                              |

> [!NOTE]
> The code that accompanies this document is available in the shared documentation folder.

You can see which **Azure regions** Azure AI Video Indexer is available on the [regions page](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/table).

## Related content

- [Manage real-time analysis extensions](live-extension.md)
