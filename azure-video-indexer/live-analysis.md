---
title: Azure AI Video Indexer live analysis overview - Preview
description: Overview of live analysis capabilities in Azure AI Video Indexer, including real-time video indexing and insights.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 09/29/2025
ms.service: azure-video-indexer
ms.topic: concept-article
# customer intent: As a user of Azure AI Video Indexer, I want to understand the live analysis capabilities, including real-time video indexing and insights, so that I can utilize these features for live events and broadcasts.
---

# Live video analysis in Azure AI Video Indexer - Preview

Azure AI Video Indexer enabled by Arc (VI), as part of an adaptive cloud approach, introduces live video analysis. It enables you to extract real time insights from your live video footage, allowing immediate detection and action. VI Live Video Analysis offers out-of-the-box insights for your live stream, and the ability to create custom object detection insights using open vocabulary technology. You can view live insights directly on top of your video stream, with bounding boxes highlighting detected objects. You can also save streams and insights as files, upload, and index external media files. With Azure AI Video Indexer, you can generate concise summaries for segments of your recorded video footage, helping you quickly catch up on key
events without watching the entire video.

The service is easy to evaluate and integrate. Use the web portal or REST API to add Azure AI Video Indexer to your workflows and systems.

> [!IMPORTANT]
> To deploy the Azure AI Live Video Indexer extension, get your Azure subscription ID approved in advance. You can sign up at [Azure AI Video Indexer Enabled by Arc - Live Analysis Early Access Program](https://aka.ms/vi-live-register).

> [!NOTE]
> You don't pay extra for Live Video Analysis while it’s in preview.

## What can I do with Live Analysis?

You can integrate the VI Live Analysis with camera live streaming to use AI-based detection from different locations. This service analyzes live videos, turning raw footage into actionable insights.

Here's a diagram showing the Live Analysis workflow.

:::image type="content" source="./media/live-analysis/workflow-diagram.svg" alt-text="Diagram showing the Live Analysis workflow." border="false" lightbox="./media/live-analysis/workflow-diagram.svg":::

## Customer scenarios and use cases

- **Retail** - You can use Live Analysis to analyze video footage to help optimize store layouts and improve customer experience and safety. With Live Analysis you can monitor the number of customers in checkout lines in real time, helping retailers to act immediately to optimize staffing and reduce wait times.

- **Manufacturing -** You can use Live Analysis to help ensure quality control and worker safety through video analysis. For example, workers who aren’t wearing protective gear, which requires real-time detection of critical events and locating specific moments in video streams.

- **Modern Safety -** You can use Azure AI Video Indexer to detect and identify security and safety issues before they cause a risk.

## Limitations

The following limitations apply to the Live Analysis feature:

### Camera limitations

- Only static cameras are supported. PTZ cameras aren’t supported.
- Cameras must support RTCP sender reports.
- Only continuous video streaming is supported. Motion-triggered video isn’t supported.
- Frame rate should be between 28-32 FPS. All cameras connected to the same extension should have the same FPS.
- The minimum supported resolution is 640 x 480 pixels. The recommended resolution for optimal performance is 1,280 x 720 pixels.
- When using ultra-high-resolution videos (frame width equal to or greater than 3,840 pixels, or frame height equal to or greater than 2,160 pixels), the system automatically uses a solution that detects small objects and covers the whole frame. However, the recorded video is saved in a lower resolution, which is Full HD (1920 x 1080 pixels) while keeping the aspect ratio. The system can't accept videos with ultra-high resolution and videos with lower resolutions on the same extension.
- Color should be RGB.
- Fisheye lenses aren’t supported.

### Detection limitations 

- Only objects larger than 35 x 35 pixels get detected.
- The detector might not detect objects in dark areas and in bad weather conditions. Extreme weather conditions can reduce results quality. For example, heavy rain and fog.
- Occlusions might reduce results quality and cause fragmentation in object tracking.
- The detector can miss or misclassify objects when viewed from an unusual point of view or extreme angles.
- The confidence score of the detection as appears in the UI represents its first appearance. Along the track, the confidence can change, and is only shown in the API.

## Prerequisites

Before you begin, review the following prerequisites to ensure that you meet them.

- You must have an **Azure AI Video Indexer** account. For more information, see the [Create Video Indexer account](create-account.md) tutorial.
- You must have a running **Kubernetes (K8s) cluster connected to Azure Arc**. For more information, see [Connect an existing Kubernetes cluster](/azure/azure-arc/kubernetes/quickstart-connect-cluster?tabs=azure-cli#connect-an-existing-kubernetes-cluster).
  - The cluster has the following requirements:
    - Read-write-many (RWX) storage class.
    - The ingress controller must allow outside clients to connect to the application.
    - At least one NVIDIA GPU enabled node in the cluster.
  - Requirements for supported Kubernetes (K8s) distributions include:
    - AKS on Azure Local enabled by Arc.
    - K8s on a Linux machine.
    - AKS on cloud.
- Make sure you have a valid **RTSP stream**. You need the RTSP URL.
- Optionally, you can have an **Azure IoT for Operations extension** deployed to an Azure Arc Kubernetes cluster. The installation of both AIO and VI extensions must be in the same cluster.
- You must have the latest version of Azure CLI. However, you can skip if you're using Azure cloud shell.
- As noted previously, your **Azure subscription ID** must already be approved. If not already approved, you can sign up at [Application for Azure AI Video Indexer Enabled by Arc - Live Video Analysis](https://aka.ms/vi-live-register).

> [!NOTE]
> We recommend enabling automatic version upgrade for your Arc-enabled Kubernetes cluster extension, so that you always have the latest security patches and new capabilities. For more information, see [Deploy and manage an Azure Arc-enabled Kubernetes cluster extension](/azure/azure-arc/kubernetes/extensions#optional-parameters).

## Hardware requirements

Here’s a table showing hardware requirements.

Minimum:

| **VM count** | **CPU (per node)** | **RAM (per node)** | **Storage** | **GPU**    |
|--------------|-----------------------|-----------------------|-------------|------------|
| 1            | 32 cores              | 64 GB                 | 200 GB      |            |
| 1            | 16 cores              | 64 GB                 | 200 GB      | NVIDIA A10 |

Recommended

| **VM count** | **CPU (per node)** | **RAM (per node)** | **Storage** | **GPU**            |
|--------------|-----------------------|-----------------------|-------------|--------------------|
| 2            | 32 cores              | 64 GB                 | 200 GB      |                    |
| 1            | 16 cores              | 64 GB                 | 200 GB      | NVIDIA A100 / H100 |

**The number of supported cameras** in one extension depends on the GPU used and the capabilities running on the camera, as detailed here:

| **Scenario \ GPU**                   | **A2** | **A10** | **V100** | **A100** | **H100** |
|--------------------------------------|--------|---------|----------|----------|----------|
| **Streaming + Recording + Insights** | 1 to 4 | 6       | 2        | 8        | 11       |
| **Streaming + Insights**             | 1 to 4 | 7       | 2        | 11       | 12       |
| **Insights Only**                    | 1 to 4 | 7       | 2        | 16       | 16       |
| **Hard Limit**                       | 4      | 8       | 4        | 16       | 16       |

*Using ultra resolution might cause a reduction in the number of supported cameras per GPU.*

- Supported GPUs are NVIDIA A2, A10, V100, A100, H100.
- The minimum required shared storage is 50 GB for one camera per day. This estimation is based on the scenario where both recordings and insights are saved.
- We recommend using NVIDIA H100 GPU in your virtual machines (VM).
- To upload video media files to the Live extension, add another virtual machine (VM) without a GPU, as specified in [Minimum hardware requirements for VI enabled by Arc](arc/azure-video-indexer-enabled-by-arc-overview.md#minimum-hardware-requirements).
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

- [Manage live analysis extensions](live-extension.md)