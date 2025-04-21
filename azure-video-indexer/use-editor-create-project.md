---
title: Use the Azure AI Video Indexer editor to create projects and add video clips
description: This article demonstrates how to use the Azure AI Video Indexer editor to create projects and add video clips.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/09/2024
ms.service: azure-video-indexer
ms.topic: article
---

# Add video clips to your projects

The [Azure AI Video Indexer](https://www.videoindexer.ai/) website enables you to use your video's deep insights to: find the right media content, locate the parts that you’re interested in, and use the results to create an entirely new project. 

Once created, the project can be rendered and downloaded from Azure AI Video Indexer and be used in your own editing applications or downstream workflows.

Some scenarios where you might find this feature useful are: 

* Creating movie highlights for trailers.
* Using old clips of videos in news casts.
* Creating shorter content for social media.

This article shows how to create a project and add selected clips from the videos to the project. 

## Create new project and manage videos

1. Browse to the [Azure AI Video Indexer](https://www.videoindexer.ai/) website and sign in.
1. Select the **Projects** tab. If you created projects before, you see all of your other projects here.
1. Select **Create new project**.  
    :::image type="content" source="./media/use-editor-create-project/new-project.png" border="true" alt-text="Screenshot showing how to create a new project." lightbox="./media/use-editor-create-project/new-project.png" :::
    
1. Give your project a name by clicking on the pencil icon. Replace the text that says "Untitled project" with your project name and select on the check.
    :::image type="content" source="./media/use-editor-create-project/new-project-edit-name.png" border="true" alt-text="Screenshot showing where to select the pencil symbol." lightbox="./media/use-editor-create-project/new-project-edit-name.png" :::

### Add videos to the project

> [!NOTE]
> Currently, projects can only contain videos indexed in the same language.
> Once you select a video in one language, you can't add the videos in your account that are in a different language, the videos that have other languages are grayed out/disabled.

1. Add videos that you want to work with in this project by selecting **Add videos**.

    You see all the videos in your account and a search box that says *Search for text, keywords, or visual content*. You can search for videos that have a specified person, label, brand, keyword, or occurrence in the transcript and optical character recognition (OCR).
    
    For example, in the following image, look for videos that mention *custom vision* in transcript only. Use **Filter** if you want to filter your search results.
    
    :::image type="content" source="./media/use-editor-create-project/custom-vision.png" border="true" alt-text="Screenshot showing a search for videos that mention custom vision." lightbox="./media/use-editor-create-project/custom-vision.png" :::
1. Select **Add** to add videos to the project.
1. Next, you see all of the videos you chose. They're the videos from which you're going to select clips for your project.

    You can rearrange the order of the videos by dragging and dropping or by selecting the list menu button and selecting **Move down** or **Move up**. From the list menu, you can also remove the video from the project. 
    
    You can add more videos to the project at any time by selecting **Add videos**. You can also add multiple occurrences of the same video to your project. Do so if you want to show a clip from one video and then a clip from another and then another clip from the first video. 

### Select clips for use in your project

If you select on the downward arrow on the right side of each video, you open up the insights in the video based on time stamps (clips of the video). 

1. To create queries for specific clips, use the search box that says *Search in transcript, visual text, people, and labels*.
1. Select **View Insights** to customize which insights you want to see and which you don't want to see. 
    :::image type="content" source="./media/use-editor-create-project/search-try-cognitive-services.png" border="true" alt-text="Screenshot showing a search for videos that say Try Azure AI services." lightbox="./media/use-editor-create-project/search-try-cognitive-services.png" :::
1. Add filters to further specify details on what scenes you're looking for by selecting **Filter options**.

    You can add multiple filters. 
1. Once you're happy with your results, select the clips you want to add to this project by selecting the segment you want to add. You can unselect this clip by clicking on the segment again.
    
    Add all segments of a video (or, all that were returned after your search) by clicking on the list menu option next to the video and selecting **Select all**. 

As you're selecting and ordering your clips, you can preview the video in the player on the right side of the page. 

> [!IMPORTANT]
> Remember to save your project when you make changes by selecting **Save project** at the top of the page. 

### Render and download the project

> [!NOTE]
> For Azure AI Video Indexer paid accounts, rendering your project has encoding costs. Azure AI Video Indexer trial accounts are limited to 5 hours of rendering.

1. Once you're done, make sure that your project was saved. You can now render the project. Select **Render**. A popup box appears informing you that Azure AI Video Indexer started to render a file and that a download link gets sent by email. Select **Continue**. 
    :::image type="content" source="./media/use-editor-create-project/render-download.png" border="true" alt-text="Screenshot that shows Azure AI Video Indexer with the option to Render and download your project." lightbox="./media/use-editor-create-project/render-download.png" :::

    You also see a notification that the project is getting rendered on top of the page. When rendering is complete, you get a new notification that the project was successfully rendered. To download the project, select the notification. It downloads the project in MP4 format.
1. You can access saved projects from the **Projects** tab. 

    If you select this project, you see all the insights and the timeline of this project. If you select **Video editor**, you can continue making edits to this project. Edits include adding or removing videos and clips or renaming the project.
    
## Create a project from your video

You can create a new project directly from a video in your account. 

1. Go to the **Library** tab of the Azure AI Video Indexer website.
1. Open the video that you want to use to create your project. On the insights and timeline page, select the **Video editor** button.

    It takes you to the same page that you used to create a new project. Unlike the new project, you see the timestamped insights segments of the video, that you started editing previously.

## See also

[Azure AI Video Indexer overview](video-indexer-overview.md)

