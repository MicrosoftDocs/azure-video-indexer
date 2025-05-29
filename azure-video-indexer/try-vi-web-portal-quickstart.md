---
title:  Quickstart - Try the Azure AI Video Indexer web portal
description: This article shows you how to get started with Azure AI Video Indexer (VI) by using the web portal. You're encouraged to experience indexing a video with the web portal before trying the API.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 05/19/2025
ms.service: azure-video-indexer
ms.topic: conceptual
---

# Quickstart: Try the Azure AI Video Indexer (VI) web portal

This article shows you how to get started with Azure AI Video Indexer by using the web portal. Try indexing a video with the web portal before you use the API.

## Prerequisites

Create or find an MP4 video.

Use a video that's about 5 minutes long. We suggest it has:

- People speaking
- Some nonspeaking noises
- Objects such as coffee cups
- A couple of different scenes like an indoor scene followed by an outdoor scene

These suggestions help you see various results after indexing. You don't need to include all of them.

## Get a trial account

Go to the [web portal](https://www.videoindexer.ai/) and sign in with a Microsoft Entra ID account, a personal Microsoft account, or a Google account. The portal assigns you a trial account automatically.

## Upload a video

Upload and index the video using the default settings. The activity of indexing a video is called a "job."

On the home page of the web portal:

1. Select the **Upload** button. The upload screen appears.  
  :::image type="content" source="./media/try-vi-web-portal-quickstart/library-upload.png" border="true" alt-text="Screenshot showing the Upload option on the Library tab." lightbox="./media/try-vi-web-portal-quickstart/library-upload.png" :::
2. Select **Browse for files**.
3. Select the video, then select **Open**.
4. The **File name** field fills in automatically, but you can change it.
5. Leave the other settings as they are, except for the video source language.
6. Select the source language from the **Video source language** list.
7. Select **Review + upload**. You see the review screen.
8. Select the **rights certification** box, then select **Upload + index**. The video starts uploading. Select **Run in background** to close the screen.
9. If you close the uploading window, select the **notification** (bell) symbol to check the upload status.

## View Timeline and Insights

The **Timeline** and **Insights** tabs show information from the service after indexing.

While your video uploads and indexes, view some sample videos.

### View the timeline

1. Select the video and then select the **Timeline** tab. The video transcript appears.
2. Scan the transcript to see what the video covers.  
    :::image type="content" source="./media/try-vi-web-portal-quickstart/timeline-transcript.png" border="true" alt-text="Screenshot showing spoken words on the Timeline tab." lightbox="./media/try-vi-web-portal-quickstart/timeline-transcript.png" :::
3. Select **Azure AI Video Indexer** above the left navigation bar to exit and return to the home page.

### View the insights

1. On the home page, select the **Samples** tab.
2. Select any one of the videos from the Samples library. The video starts playing and the **Insights** tab appears.
3. The insights are grouped into categories like **People**, **Topics**, **Labels**, and **Named entities**.  
  :::image type="content" source="./media/try-vi-web-portal-quickstart/insights-details.png" border="true" alt-text="Screenshot showing details on the Insights tab." lightbox="./media/try-vi-web-portal-quickstart/insights-details.png" :::
4. Select **Azure AI Video Indexer** above the left navigation bar to exit and return to the home page.

## View your video timeline and insights

1. Select the **Library** tab. Your indexed videos appear there. If your video is still uploading, you see a thumbnail with the upload percentage.
2. When indexing finishes, select your video to see the insights.
3. Compare the insights shown to the ones that you viewed in the Samples library.

## View the JSON

Access the API JSON response for your indexing job.

1. In the upper right, select the **Download** symbol.
2. Select **Insights (JSON)**. The JSON file opens in a new browser window or tab.  
  :::image type="content" source="./media/try-vi-web-portal-quickstart/download-insights-json.png" border="true" alt-text="Screenshot showing where to download JSON insights." lightbox="./media/try-vi-web-portal-quickstart/download-insights-json.png" :::
