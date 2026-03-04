---
title: Live AI insights catalog in Azure AI Video Indexer
description: Learn how AI insights work for live stream video, how they appear in the AI insights catalog, and when to use built-in and custom insights.
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 03/04/2026
ai-usage: ai-assisted
ms.service: azure-video-indexer
ms.topic: concept-article
appliesto: 
- Azure AI Video Indexer enabled by Azure Arc
# customer intent: As an Azure user, I want to understand live video AI insights, how they appear in the AI insights catalog, and how to use built-in or custom insights for my cameras.
---

# Live AI insights catalog for Azure AI Video Indexer enabled by Azure Arc - Preview

Live AI insights detect people, vehicles, or custom objects and situations in live camera streams. They run in your Azure Arc edge environment so you can act on detections right away. Unlike uploaded file analysis, real-time AI insights process a live stream and return detections continuously, not a completed index after file processing. You manage these insights in the AI insights catalog.

## The AI insights catalog

The AI insights catalog under **Model customizations** is the central place in the VI portal where you review available insights and build presets. 

Go to [Azure AI Video Indexer](https://www.videoindexer.ai/) to view the AI insights catalog to see all available insights.

:::image type="content" source="./media/live-ai-insights-catalog/ai-insights-catalog.png" border="true" alt-text="Screenshot of the AI insights catalog page." lightbox="./media/live-ai-insights-catalog/ai-insights-catalog.png" :::

Use the **Environment** filter to choose the scope you need: 

For Cloud-based Azure AI Video Indexer deployments:

- Cloud 

For Azure AI Video Indexer enabled by Azure Arc: 

- Live video stream - enabled by Arc
- Media uploads - enabled by Arc

This article focuses on **Live video stream - enabled by Arc**, which shows the real-time insights you can apply to cameras.

## Types of live AI insights

There are two types of real-time AI insights: built-in detection for people and vehicles and custom insights for objects and situations.

### Built-in insights for people and vehicle detection

Built-in live insights detect people and common vehicle types such as cars, vans, and trucks. The detection runs automatically on live streams when you include it in a preset. It draws bounding boxes, shows real-time counts, and assigns a per-camera track ID based on visual features and location, not biometric data. When an object leaves the frame and returns, it receives a new ID.

You don't need to configure or train this insight. Enable it in a preset. Use it for occupancy counts, traffic flow, and general site oversight.

Here's an example of a live stream with people and vehicle detection:

:::image type="content" source="./media/live-ai-insights-catalog/people-vehicle-detection.png" border="true" alt-text="Screenshot of a live stream with people and vehicle detection." lightbox="./media/live-ai-insights-catalog/people-vehicle-detection.png" :::

To use these built-in detections:

1. Create a preset and select **People** and **Vehicle**.
1. Apply the preset to the camera.
1. Monitor the live stream for counts, boxes, and tracking.

### Custom insights

Custom insights let you detect objects or situations that go beyond built-in people and vehicle detection. Define what you need with text descriptions and optional example images, then refine with negative examples if needed. Choose **object** insights for specific items and **situation** insights for conditions across the frame. Use them for safety checks, operational exceptions, or site-specific monitoring. For more information, see [Custom insights in the live AI Insights catalog](live-custom-insights-overview.md).

To use a custom insight,

1. Create a custom insight in the AI insights catalog.
1. Add text descriptions and optional example images.
1. Include the custom insight in a preset.
1. Apply the preset to the camera.




## High-level workflow: From detection to deployment

Follow these steps to set up live AI insights for your cameras:

1. **Identify your need** - Decide what to monitor, like occupancy, safety hazards, equipment checks, and whether to use built-in detection for people or vehicles, or create custom insights.
2. **Access the AI insights catalog** - Go to the VI portal and filter by **Environment** > **Live video stream - enabled by Arc** to view available insights.
3. **Configure your insight** - For built-in insights, no configuration is needed. For custom insights, define what you want to detect using text descriptions and/or example images.
4. **Create a preset** - Bundle your selected insights into a preset (for example, people detection + hard hat detection + crowding alert).
5. **Apply preset to camera** - Link the preset to one or more camera streams.
6. **Monitor in real-time** - View live detections with bounding boxes, counts, and tracking on the camera stream.

## Limitations

The following limitations apply to all real-time AI insights (people, vehicle, and custom):

- The object tracker is limited to 150 concurrent tracks per stream.
- The confidence of the track as shown in the UI reflects the first occurrence of the track.
- Small objects might not get detected (smaller than 35 x 35 pixels).
- The detector might miss objects in darker areas and severe weather conditions.
- To best detect and track objects, they should be fully visible (no occlusions), with good lighting.
- Large crowds can get underestimated by the model and might not detect all persons.
- The tracker assigns a different ID to the same object after it exits and reenters the camera's view.
- Occlusions might reduce results quality and cause fragmentation in object tracking.
- The detector might misclassify objects observed from steep angles.

## Related content

- [Custom insights in the real-time AI Insights catalog](live-custom-insights-overview.md)
- [Create custom insights in the live AI Insights catalog](live-custom-insights-create.md)
- [Create a preset](live-manage-camera.md#create-a-preset)
- [Apply a preset to a camera](live-manage-camera.md#apply-a-preset-to-a-camera)


