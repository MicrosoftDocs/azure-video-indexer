---
title: Edit speakers in the Azure AI Video Indexer website
description: The article demonstrates how to edit speakers with the Azure AI Video Indexer website.
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
appliesto:
    - Azure AI Video Indexer enabled by Azure Arc
    - Cloud-based Azure AI Video Indexer
---

# Edit speakers with the Azure AI Video Indexer website

Azure AI Video Indexer identifies each speaker in a video and attributes each transcribed line to a speaker. The speakers are given a unique identity such as `Speaker #1` and `Speaker #2`. To provide clarity and enrich the transcript quality, you might want to replace the assigned identity with each speaker's actual name. To edit speakers' names, use the edit actions as described in the article. 

The article demonstrates how to edit speakers with the [Azure AI Video Indexer website](https://www.videoindexer.ai/). The same editing operations are possible with an API. To use API, call [update video index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Video-Index).

> [!NOTE]
> The addition or editing of a speaker name is applied throughout the transcript of the video but isn't applied to other videos in your Azure AI Video Indexer account.

## Start editing

1. Sign in to the [Azure AI Video Indexer website](https://www.videoindexer.ai/).
2. Select a video.
3. Select the **Timeline** tab.
4. Choose to view speakers.


:::image type="content" source="./media/edit-speakers-website/view-speakers.png" border="true" alt-text="Screenshot showing how to view speakers on the Timeline tab." lightbox="./media/edit-speakers-website/view-speakers.png" :::

## Add a new speaker

This action allows you to add new speakers that Azure AI Video Indexer didn't identify. To add a new speaker from the website for the selected video, do the following steps: 

1. Select the edit mode.
    :::image type="content" alt-text="Screenshot showing where to select the the Edit symbol." source="./media/edit-speakers-website/edit.png":::
1. Go to the speakers drop down menu above the transcript line you wish to assign a new speaker to.
1. Select **Assign a new speaker**.
    :::image type="content" source="./media/edit-speakers-website/assign-new.png" border="true" alt-text="Screenshot showing how to assign a new speaker." lightbox="./media/edit-speakers-website/assign-new.png" :::
1. Add the name of the speaker you would like to assign.
1. Press a checkmark to save.

> [!NOTE]
> Speaker names should be unique across the speakers in the current video.
 
## Rename an existing speaker

This action allows renaming an existing speaker that Azure AI Video Indexer identified. The update applies to all speakers identified by this name.
 
To rename a speaker from the website for the selected video, do the following steps: 

1. Select the edit mode.
1. Go to the transcript line where the speaker you wish to rename appears.
1. Select **Rename selected speaker**.
    :::image type="content" source="./media/edit-speakers-website/rename.png" border="true" alt-text="Screenshot showing how to rename a selected speaker." lightbox="./media/edit-speakers-website/rename.png" :::
   This action updates speakers by this name.
1. Select the checkmark symbol to save.

## Assign a speaker to a transcript line

This action allows assigning a speaker to a specific transcript line with a wrong assignment. To assign a speaker to a transcript line from the website, do the following steps: 

1. Go to the transcript line you want to assign a different speaker to. 
1. Above what you want to assign, select a speaker from the speakers list.
 
    The update only applies to the currently selected transcript line.

If the speaker you wish to assign doesn't appear on the list, you can either **Assign a new speaker** or **Rename an existing speaker** as described previously.

## Limitations

When you add a new speaker or renaming a speaker, the new name should be unique.
