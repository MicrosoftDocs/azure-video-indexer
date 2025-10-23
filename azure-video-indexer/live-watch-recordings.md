---
title: Watch live video recordings in Azure AI Video Indexer
description: Learn how to watch live video recordings from your cameras using Azure AI Video Indexer.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 09/29/2025
ms.service: azure-video-indexer
ms.topic: how-to
# customer intent: As an Azure Video Indexer user, I want to watch live video recordings from my cameras so that I can monitor activities that happened in real-time.
---

# Watch live video recordings- Preview

The live video player allows you to watch live video recordings from your cameras. You can view the last 60 minutes of live streaming per camera. To view recordings beyond 60 minutes, go to the recording files of the camera. For more information, see [Watch live video recordings](#watch-live-video-recordings).

## Live video player controls

- The live player displays the last 60 minutes live streaming per camera. To view beyond 60 minutes, go to the recording files of this camera. For more information, see [Watch live video recordings](#watch-live-video-recordings).
- **Bounding box** - You can choose to display the bounding box on top of the live stream player. When a new object is detected, the bounding box that marks the object is highlighted in blue for 2 seconds, then turns to black. You can display the bounding box for a selected subset of the insights included in the camera preset.
- **Insights Timeline** – On the right side of the screen, you can view the timeline of detections, each with a unique ID and confidence score. Select **View** located in the upper right corner of the insight timeline to change the insights display in the timeline.
- **Counter** – The counter in the video insights timeline shows the number of objects of each type in the frame. To alter the display, select **View** located in the upper right corner of the insight timeline and select **Show counters for AI insights**.

## Video on demand (VOD) recordings considerations

- Understand the retention policy of your camera. It can set your recorded files to get automatically deleted. You can adjust the detections retention policy separately from the video in the API if you want to keep insights longer.
- VOD only reflects the AIs that run on the Live camera during the recording time. Currently, you can't apply presets on VOD data retroactively.
- You can tag a video file.
- You can see in the VOD gallery if the file includes detection.
- The time of the video is UTC. Each video is from UTC 12 AM until 12 AM the next day. The created VOD files are 24 hours duration.
- You can only delete a video after the recording ends.
- The video appears in the VOD gallery after a 10-minute delay.

## Watch live video recordings

1. From the Camera, -\> select the **Recordings** tab. Recordings from the camera are shown.  
    :::image type="content" source="./media/live-watch-recordings/recordings-tab.png" border="true" alt-text="Screenshot of the Recordings tab." lightbox="./media/live-watch-recordings/recordings-tab.png" :::
2. From the extension page, go to the **Media files** tab. All recordings from all cameras in the extension are shown.  
    :::image type="content" source="./media/live-watch-recordings/media-files-tab.png" border="true" alt-text="Screenshot of the Media files tab." lightbox="./media/live-watch-recordings/media-files-tab.png" :::

### Upload a video file

In the **Media files** tab, you can select **Upload** to upload an external video file to index. You can't apply the previously mentioned live AI presets to an uploaded media file. The supported presets for uploaded files are:

| **Model** | **Basic video** | **Basic audio** | **Basic video and audio** |
|-----------|-----------------|-----------------|---------------------------|
| [Transcription](transcription-translation-lid-insight.md) | | ✔ | ✔ |
| [Translation](transcription-translation-lid-insight.md) | | ✔ | ✔ |
| [Captioning](view-closed-captions.md) | | ✔ | ✔ |
| [Key frame detection](scene-shot-keyframe-detection-insight.md) | ✔ | | ✔ |
| [Object detection](object-detection-insight.md) | ✔ | | ✔ |
| [Scene detection](scene-shot-keyframe-detection-insight.md) | ✔ | | ✔ |
| [Shot detection](scene-shot-keyframe-detection-insight.md) | ✔ | | ✔ |
| [Summarization](text-summarization-overview.md) | ✔ | ✔ | ✔ |

For more information about the presets available for uploaded videos, see [Supported AI presets](arc/azure-video-indexer-enabled-by-arc-overview.md#supported-ai-presets).

## Related content

- [Live video analysis in Azure AI Video Indexer](live-analysis.md)
- [Manage live analysis cameras](live-manage-camera.md)
- [Search using Edge RAG](live-search-edge-rag.md)