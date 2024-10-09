---
title:  Quickstart - Try the Azure AI Video Indexer web portal
description: This article shows you how to get started with Azure AI Video Indexer (VI) by using the web portal. You're encouraged to experience indexing a video with the web portal before trying the API.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.collection: ce-skilling-ai-copilot
ms.date: 10/09/2024
ms.service: azure-video-indexer
ms.topic: conceptual
---

# Quickstart: Try the Azure AI Video Indexer (VI) web portal

This article shows you how to get started with Azure AI Video Indexer by using the web portal. You're encouraged to experience indexing a video with the web portal before trying the API.

## Prerequisites

Create or find an MP4 video.

The video should be about 5 minutes in duration. It's suggested that they contain:

-   People speaking
-   Some nonspeaking noises
-   Objects such as coffee cups
-   A couple of different scenes like an indoor scene followed by an outdoor scene

These suggestions are so that you can see a varied set of results after the video is indexed. They aren’t all required.

## Get a trial account

Go to the [web portal](https://www.videoindexer.ai/) and sign in with an Entra account, a personal Microsoft account, or a Google account. You're automatically assigned a trial account.

## Upload a video

Upload and index the video using the default settings. The activity of indexing a video is called a "job."

On the home page of the web portal:

1.  Select the **Upload** button. The upload screen appears.
2.  Select **Browse for files**.
3.  Select the video, then select **Open**.
4.  The **video name** field is auto populated, but you can change it if you want to.
5.  Leave the rest of the settings the way they are except for the source language.
6.  Select the source language from the **Source language** drop-down menu.
7.  Select **Review + upload**. The review screen appears.
8.  Select the **rights certification** checkbox, then select **Upload + index**. The video starts uploading. You can close the screen by selecting **Run in background**.
9.  If you closed the uploading window, select the **notification** (bell) icon to check on the status of the upload.

## View the timeline and insights

The timeline and Insights are the resulting information returned by the service after indexing the video.

While your video is uploading, view some of the sample videos.

### View the timeline

1.  Select the **Timeline** tab. The video transcript appears.
2.  Scan the transcript of the spoken audio of the video to get an idea of what was covered in the video.

### View the insights

1.  Select the **Samples** tab.
2.  Select any one of the videos from the Samples library.
3.  Select **View** from the menu.
4.  Select **Monitoring** to deselect most of the insights.
5.  Uncheck the remaining insight checkboxes. The insights area of the screen should be empty.
6.  Select and unselect the checkboxes one at a time to see the resulting insights.

## View your video timeline and insights

1.  Select **Library.** Your indexed videos are located here. If your video is still uploading, it's represented by a thumbnail with the percentage of the video upload indicated.
2.  If the video indexing is complete, select **your video** to see the insights.
3.  Compare the insights you received to the ones that you viewed in the Samples library.

## View the JSON

You can access the API JSON response of your indexing job.

1.  Select **Download**.
2.  Select **Insights (JSON)**. The JSON file opens in a new browser window or tab.
